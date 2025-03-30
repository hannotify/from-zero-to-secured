<!-- .slide: data-background="img/background/binary-code.jpg" data-background-color="black" data-background-opacity="0.2" -->

## Use REST to Access Championship Standings

let's run a **database**,
configure **JTA persistence**
and access the championship standings through **REST**

<https://pxhere.com/en/photo/1458897> <!-- .element: class="attribution" -->

---

## Why Constructor Injection Instead of Field Injection?

**Constructor injection:**

* allows us to inject mocks; <!-- .element: class="fragment fade-in-then-semi-out" -->
* helps us to stick <!-- .element: class="fragment" --> to the single-responsibility principle (from `SOLID`);
    * a constructor with 10+ arguments will certainly stand out as a code smell; <!-- .element: class="fragment" -->
    * a class with 10+ fields: not so much. <!-- .element: class="fragment" -->

---

## Why Constructor Injection Instead of Field Injection?

**Field injection**

* ...tightly couples your class to the injection framework, because there is no other way to populate your class; <!-- .element: class="fragment" -->
  * in contrast to constructor injection. <!-- .element: class="fragment" -->

---

### Quarkus ❤️ Constructor Injection

A framework like *Quarkus* allows you to mark your dependency field as `final`, because it generates the mandatory no-args constructor for you.

<pre><code class="java" data-line-numbers data-trim>
@ApplicationScoped
public class MyCoolService {
    private final SimpleProcessor processor;

    // no default constructor needed - Quarkus will generate it.

    @Inject
    MyCoolService(SimpleProcessor processor) {
        this.processor = processor;
    }
}
</code></pre>

<small>(<a href="https://quarkus.io/guides/cdi-reference#simplified-constructor-injection">https://quarkus.io/guides/cdi-reference#simplified-constructor-injection</a>)</small>