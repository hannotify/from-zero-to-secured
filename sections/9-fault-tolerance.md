<!-- .slide: data-background="img/background/binary-code.jpg" data-background-color="black" data-background-opacity="0.2" -->

## Fault Tolerance

let's make our championship standings more **fault-tolerant**
by applying a **timeout** and **fallback** implementation

<https://pxhere.com/en/photo/1458897> <!-- .element: class="attribution" -->

---

## On Microprofile Fault Tolerance

Fault tolerance mechanisms are easily applied through annotations:

<ul>
  <li class="fragment fade-in-then-semi-out"><code>@Timeout</code> - throws a <code>TimeoutException</code> after the specified delay, to prevent indefinite loading times</li>
  <li class="fragment fade-in-then-semi-out"><code>@Fallback</code> - reverts to a fallback implementation when a specific <code>Exception</code> occurs <br/> <small>(works well in combination with <code>@Timeout</code>)</small></li>
</ul>

---

### More MicroProfile Fault Tolerance Annotations

<ul>
  <li class="fragment fade-in-then-semi-out"><code>@Retry</code> - retries an operation when a specific <code>Exception</code> occurs</li>
  <li class="fragment fade-in-then-semi-out"><code>@Bulkhead</code> - limits the number of concurrent calls to an instance</li>
  <li class="fragment"><code>@CircuitBreaker</code> - prevents further damage by not executing functionality that is doomed to fail anyway</li>
</ul>