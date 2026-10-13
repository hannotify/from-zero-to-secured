<!-- .slide: data-background="img/background/binary-code.jpg" data-background-color="black" data-background-opacity="0.2" -->

## Calculate Championship Standings

let's calculate the **championship standings**

<https://pxhere.com/en/photo/1458897> <!-- .element: class="attribution" -->

---

## Why Did We Use a CDI Bean and not an EJB?

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

## On CDI Scopes

<table style="font-size: 70%">
  <thead>
    <tr>
      <th style="text-align: right">Annotation</th>
      <th>Lifecycle</th>
      <th>Suitable for</th> 
    </tr>
  </thead>
  <tbody>
    <tr class="fragment fade-in-then-semi-out">
      <td style="text-align: right"><code>@ApplicationScoped</code></td>
      <td>Same instance for entire application</td>
      <td>Shared resources like configuration settings or caches</td>
    </tr>
    <tr class="fragment fade-in-then-semi-out">
      <td style="text-align: right"><code>@SessionScoped</code></td>
      <td>New instance per user session</td>
      <td>User-specific data that needs to persist across multiple requests, like user preferences or shopping cart contents</td>
    </tr>
    <tr class="fragment fade-in-then-semi-out">
      <td style="text-align: right"><code>@RequestScoped</code></td>
      <td>New instance per HTTP request</td>
      <td>Request-specific data, such as form data or request parameters</td>
    <tr class="fragment">
      <td style="text-align: right"><code>@Dependent</code></td>
      <td>Depending on the lifecycle of the bean it is injected into</td>
      <td>Short-lived, non-shared beans that are used as dependencies of other beans</td>
    </tr>
  </tbody>
</table>

note:
Note that the default scope for Jakarta Data Repositories is @Dependent.
