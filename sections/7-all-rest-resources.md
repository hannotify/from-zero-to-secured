<!-- .slide: data-background="img/background/binary-code.jpg" data-background-color="black" data-background-opacity="0.2" -->

## All REST Resources

let's create REST resources
for **drivers**, **races** and **race results**
so we can connect them to the frontend later!

<https://pxhere.com/en/photo/1458897> <!-- .element: class="attribution" -->

---

## On Entities & Data Transfer Objects

We didn't re-use our entities in the REST layer, because:

* we don't want the REST layer to know about the persistence layer; <!-- .element: class="fragment" -->
  * REST clients shouldn't <!-- .element: class="fragment" --> be able to discover *anything* about the internals of our app; 
  * What if we would want to move away from persistence in the future? <!-- .element: class="fragment" -->
* again, a class should have only one reason to change; <!-- .element: class="fragment" -->

---

### Implementing Data Transfer Objects

DTOs are flat data structures that contain no business logic.
This <!-- .element: class="fragment fade-in-then-semi-out" --> makes a *Java Record* the ideal way to implement a DTO. 

---

## On CDI Scopes for REST Resources

By default, Jakarta REST root resource classes are managed in the request scope, so no annotations are required for specifying the scope.

<small class="fragment">(but there is no harm in defining them anyway)</small>

<small><a href="https://jakarta.ee/learn/docs/jakartaee-tutorial/current/websvcs/rest-advanced/rest-advanced.html#_integrating_jakarta_rest_with_jakarta_enterprise_beans_technology_and_cdi">https://jakarta.ee/learn/docs/jakartaee-tutorial/current/websvcs/rest-advanced/rest-advanced.html#_integrating_jakarta_rest_with_jakarta_enterprise_beans_technology_and_cdi</a>
</small>
