<!-- .slide: data-background="img/background/binary-code.jpg" data-background-color="black" data-background-opacity="0.2" -->

## Calculate Championship Standings

let's calculate the **championship standings**

<https://pxhere.com/en/photo/1458897> <!-- .element: class="attribution" -->

---

## On CDI Scopes

<table style="font-size: 75%">
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
    </tr>
    <tr class="fragment">
      <td style="text-align: right"><code>@Dependent</code></td>
      <td>Depending on the lifecycle of the bean it is injected into</td>
      <td>Short-lived, non-shared beans that are used as dependencies of other beans</td>
    </tr>
  </tbody>
</table>
