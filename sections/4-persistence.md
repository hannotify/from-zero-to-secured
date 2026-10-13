<!-- .slide: data-background="img/background/binary-code.jpg" data-background-color="black" data-background-opacity="0.2" -->

## Persistence

let's create a few **entities**
and some **repositories**  

<https://pxhere.com/en/photo/1458897> <!-- .element: class="attribution" -->

---

<!-- Omitted in 45-minute version. -->
<!-- .slide: data-visibility="hidden" -->

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

<!-- Omitted in 45-minute version. -->
<!-- .slide: data-visibility="hidden" -->

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

### Using Jakarta Data 1.0 

<small>(part of the Jakarta EE 11 spec, supported by OpenLiberty `v26.0.0.5` and up)</small>

<pre><code class="java" data-line-numbers data-trim>
@Repository
public interface UserRepository extends CrudRepository&lt;User, UUID&gt; {
    @Find
    public Optional&lt;User&gt; findByUsernameAndPassword(String username, String password) {
}
</code></pre>

<small class="fragment">...making use of:</small>

* CRUD <!-- .element: class="fragment" --> methods from the `CrudRepository` interface 
* find methods <!-- .element: class="fragment" -->

---

### Methods in the CrudRepository interface

```java
S save(S entity);
List<S> saveAll(List<S> entities);
Optional<T> findById(@By(ID) K id);
Stream<T> findAll();
Page<T> findAll(PageRequest pageRequest, Order<T> sortBy);
void deleteById(@By(ID) K id);
void delete(T entity);
void deleteAll(List<? extends T> entities);
S insert(S entity);
List<S> insertAll(List<S> entities);
S update(S entity);
List<S> updateAll(List<S> entities);
```

<br/>
<p class="fragment fade-in-then-semi-out">Your Jakarta Data implementation will generate appropriate implementations of these methods at runtime.</p>

---

### Find Methods

* The find method's parameters and return type are used to generate the query statement <!-- .element: class="fragment fade-in-then-semi-out" -->
* Every method parameter <!-- .element: class="fragment fade-in-then-semi-out" --> should have a matching entity attribute, or have an `@Param` annotation to define a custom database column name
* Attributes should match by name and type <!-- .element: class="fragment fade-in-then-semi-out" -->

> <!-- .element: class="fragment" --> In contrast to other frameworks (like Spring Data), the method name doesn't have to follow any pattern. 