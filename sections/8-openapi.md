<!-- .slide: data-background="img/background/binary-code.jpg" data-background-color="black" data-background-opacity="0.2" -->

## API Documentation

let's **document** our REST API
using MicroProfile OpenAPI

<https://pxhere.com/en/photo/1458897> <!-- .element: class="attribution" -->

---

<!-- Omitted in 45-minute version. -->
<!-- .slide: data-visibility="hidden" -->

### Overview of Used OpenAPI Annotations 

<table style="font-size: 75%">
	<tr>
		<th style="text-align: right">Annotation</th>
		<th>Purpose</th>
	</tr>
	<tr class="fragment fade-in-then-semi-out">
		<td style="text-align: right"><code>@APIResponse</code></td>
		<td>Describes a single response from an API operation.</td>
	</tr>	
	<tr class="fragment fade-in-then-semi-out">
		<td style="text-align: right"><code>@APIResponseSchema</code></td>
		<td>Convenient short-hand way to specify a simple response with a Java class that could otherwise be specified using <code>@APIResponse</code>.</td>
	</tr>	
	<tr class="fragment fade-in-then-semi-out">
		<td style="text-align: right"><code>@Operation</code></td>
		<td>Describes a single API operation on a path.</td>
	</tr>	
	<tr class="fragment">
		<td style="text-align: right"><code>@Parameter</code></td>
		<td>Describes a single operation parameter.</td>
	</tr>
</table>
