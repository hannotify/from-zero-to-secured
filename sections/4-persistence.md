<!-- .slide: data-background="img/background/binary-code.jpg" data-background-color="black" data-background-opacity="0.2" -->

## Persistence

let's create a few **entities**,
some **repositories**  
and a few **unit tests**  

<https://pxhere.com/en/photo/1458897> <!-- .element: class="attribution" -->

---

## On JPA Attribute Converters

When JPA doesn't support your data type (like the `java.time.Year` we used in Gravel Trapp), you can use an `AttributeConverter` to provide a custom mapping for it.

<pre class="fragment fade-in-then-semi-out"><code class="java" data-line-numbers data-trim>
    @Converter(autoApply = true)
    public class YearAttributeConverter implements AttributeConverter&lt;Year, Short&gt; {
        @Override
        public Short convertToDatabaseColumn(Year attribute) {
            return attribute != null ? (short) attribute.getValue() : null;
        }

        @Override
        public Year convertToEntityAttribute(Short dbData) {
            return dbData != null ? Year.of(dbData) : null;
        }
    }
</code></pre>

---

### Generic Steps to Create and Use an Attribute Converter

<ol>
  <li class="fragment fade-in-then-semi-out">Implement the <code>AttributeConverter&lt;X,Y&gt;</code> interface in a special converter class
  <li class="fragment">Annotate your converter class with <code>@Converter</code>, and either:
    <ul>
        <li class="fragment">set its <code>autoApply</code> property to <code>true</code>, or</li>
        <li class="fragment">annotate the appropriate fields of type <code>X</code> with <code>@Convert(converter = YourAttributeConverter.class)</code></li>
    </ul>
</ol>

---

### On the `@Transactional` Annotation

* declaratively controls transaction boundaries on CDI managed beans <!-- .element: class="fragment fade-in-then-semi-out" -->
* begins a new transaction or reuses an existing one, by default <!-- .element: class="fragment fade-in-then-semi-out" -->
* implemented by a Jakarta EE interceptor <!-- .element: class="fragment fade-in-then-semi-out" -->
* by default, runtime exceptions result in the transaction being rollbacked <!-- .element: class="fragment fade-in-then-semi-out" -->
* by <!-- .element: class="fragment fade-in-then-semi-out" --> setting the `rollbackOn` property, this behavior can be extended to any arbitrary exception 
* in <!-- .element: class="fragment fade-in-then-semi-out" --> contrast, `dontRollbackOn` indicates exceptions that should not rollback the transaction

---

## Why Did We Use CDI Beans and not EJBs?

For Gravel Trapp we primarily need: 

* transaction management
* dependency injection
* state management

<span class="fragment">
  <p>all of which are supported by CDI.</p>

  <small>(using `@Transactional`, `@Inject`, and `@RequestScoped`/`@ApplicationScoped`)</small>
</span>

---

## EJB Features We Didn't Need

EJBs offer many more features that we don't need in this case, like:

* concurrency management
* remote access
* interceptors
* timers
* asynchronous processing

---

### EJB vs. CDI Bean Cheat Sheet

<table style="font-size: 50%">
  <thead>
    <tr>
      <th style="text-align: right;">Feature</th>
      <th>EJB</th>
      <th>CDI Bean</th>
    </tr>
  </thead>
  <tbody>
    <tr class="fragment">
      <th style="text-align: right;">Transaction Management</th>
      <td>✅ Built-in support for declarative transaction management using annotations like <code>@TransactionAttribute</code>.</td>
      <td>✅ Requires additional annotations like <code>@Transactional</code> for declarative transaction management.</td>
    </tr>
    <tr class="fragment">
      <th style="text-align: right;">Concurrency Management</th>
      <td>✅ Built-in support for concurrency management with annotations like <code>@Lock</code> and <code>@AccessTimeout</code>.</td>
      <td>❌ No built-in concurrency management; must be handled manually or with additional libraries.</td>
    </tr>    
    <tr class="fragment">
      <th style="text-align: right;">Remote Access</th>
      <td>✅ Supports remote access via RMI, IIOP, or web services.</td>
      <td>❌ Primarily designed for local access within the same application.</td>
    </tr>
    <tr class="fragment">
      <th style="text-align: right;">Interceptors</th>
      <td>✅ Supports interceptors with <code>@AroundInvoke</code> and lifecycle callback methods.</td>
      <td>✅ Supports interceptors with <code>@Interceptor</code> and <code>@AroundInvoke</code> annotations.</td>
    </tr>
    <tr class="fragment">
      <th style="text-align: right;">Timers</th>
      <td>✅ Built-in support for scheduling tasks with <code>@Schedule</code> and <code>@Timeout</code>.</td>
      <td>❌ No built-in support for scheduling tasks; requires additional libraries or frameworks.</td>
    </tr>
    <tr class="fragment">
      <th style="text-align: right;">Dependency Injection</th>
      <td>✅ Supports dependency injection with <code>@EJB</code> and <code>@Resource</code>.</td>
      <td>✅ Supports dependency injection with <code>@Inject</code> and other CDI annotations.</td>
    </tr>
    <tr class="fragment">
      <th style="text-align: right;">State Management</th>
      <td>✅ Supports stateful and stateless session beans.</td>
      <td>✅ Primarily stateless, but can use scopes like <code>@SessionScoped</code> and <code>@ApplicationScoped</code> for state management.</td>
    </tr>
    <tr class="fragment">
      <th style="text-align: right;">Asynchronous Processing</th>
      <td>✅ Supports asynchronous method invocation with <code>@Asynchronous</code>.</td>
      <td>❌ Requires additional libraries or frameworks for asynchronous processing.</td>
    </tr>
  </tbody>
</table>

---

## On Generic JPA Repositories

For Gravel Trapp we created a generic `Repository<E,ID>` class:

<pre class="fragment fade-in-then-semi-out"><code class="java" data-line-numbers data-trim>
@Transactional
public abstract class Repository&lt;E,ID&gt; {
    @PersistenceContext(unitName = "gravel-trapp")
    protected EntityManager em;
    private final Class&lt;E&gt; entityClass;

    public Repository() {
        this.entityClass = entityClass();
    }

    protected abstract Class&lt;E&gt; entityClass();

    public SequencedCollection&lt;E&gt; findAll() {
        return em.createQuery("SELECT e FROM %s e".formatted(entityClass.getSimpleName()), entityClass).getResultList();
    }

    public Optional&lt;E&gt; findById(ID id) {
        return Optional.ofNullable(em.find(entityClass, id));
    }

    public void create(E entity) {
        em.persist(entity);
    }

    public E update(E entity) {
        return em.merge(entity);
    }

    public void deleteById(ID id) {
        var entity = findById(id)
                .orElseThrow(() -> new IllegalArgumentException("Invalid %sId: %s".formatted(entityClass, id)));
        delete(entity);
    }

    public void delete(E entity) {
        em.remove(entity);
    }

    public void deleteAll() {
        var query = em.createQuery("DELETE FROM %s e".formatted(entityClass.getSimpleName()));
        query.executeUpdate();
    }
}
</code></pre>

---

...and per entity a concrete `EntityRepository` class:

<pre class="fragment fade-in-then-semi-out"><code class="java" data-line-numbers data-trim>
@RequestScoped
public class UserRepository extends Repository&lt;User, UUID> {
    @Override
    protected Class&lt;User&gt; entityClass() {
        return User.class;
    }

    public UserDto findByUsernameAndPassword(String username, String password) {
        return UserMapper.fromEntity(em.createQuery(
                        """
                        SELECT u 
                        FROM User u 
                        WHERE u.username = :username AND u.password = :password
                        """, User.class)
                .setParameter("username", username)
                .setParameter("password", PasswordUtil.digest(password))
                .getSingleResult());
    }
}
</code></pre>

---

### Using Jakarta Data 1.0 

<small>(will be a part of Jakarta EE 11, scheduled for release later in 2025)</small>

<pre><code class="java" data-line-numbers data-trim>
@Repository
public interface UserRepository extends CrudRepository&lt;User, UUID&gt; {
    public Optional&lt;User&gt; findByUsernameAndPassword(String username, String password) {
}
</code></pre>

<small class="fragment">...making use of:</small>

* CRUD <!-- .element: class="fragment" --> methods from the `CrudRepository` interface 
* find methods <!-- .element: class="fragment" -->

---

### Methods in the CrudRepository interface

```java
<S extends T> S save(S entity)
<S extends T> List<S> saveAll(List<S> entities);
Optional<T> findById(@By(ID) K id)
Stream<T> findAll()
Page<T> findAll(PageRequest pageRequest, Order<T> sortBy)
void deleteById(@By(ID) K id)
void delete(T entity)
void deleteAll(List<? extends T> entities)
<S extends T> S insert(S entity)
<S extends T> List<S> insertAll(List<S> entities)
<S extends T> S update(S entity)
<S extends T> List<S> updateAll(List<S> entities)
```

<br/>
<p class="fragment fade-in-then-semi-out">Your Jakarta Data implementation will generate appropriate implementations of these methods at runtime.</p>

---

### Find Methods

* The find method's parameters and return type are used to generate the query statement <!-- .element: class="fragment fade-in-then-semi-out" -->
* Every method parameter <!-- .element: class="fragment fade-in-then-semi-out" --> should have a matching entity attribute, or have a `@Param` annotation attached to it to define a custom database column name
* These attributes should match by name and type <!-- .element: class="fragment fade-in-then-semi-out" -->

> <!-- .element: class="fragment" --> In contrast to other frameworks (like Spring Data), the method name doesn't have to follow any pattern. 