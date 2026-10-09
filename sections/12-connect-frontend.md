<!-- .slide: data-background="img/background/binary-code.jpg" data-background-color="black" data-background-opacity="0.2" -->

## Connect Frontend

finally, let's connect **an Angular frontend**
to our Jakarta EE backend

<https://pxhere.com/en/photo/1458897> <!-- .element: class="attribution" -->

---

## On Cross-Origin Resource Sharing  <span class="fragment">(or 'CORS')</span>

<p class="fragment">
By default, <em>same-origin security policies</em> are in place. 
</p>

<p class="fragment">
They prevent so-called <em>cross-origin requests</em>. <br/>
(requests between servers on different domains)
<p>

---

### A Few Example Cross-Origin Requests

`hanno.codes --> baselone.ch` <!-- .element: class="fragment" -->

`localhost:4200 --> localhost:9080` <!-- .element: class="fragment" -->

<small class="fragment">(by default, browsers block the server response unless the server adds HTTP response headers to allow the web page to consume the data)</small>

---

### Adding the Appropriate HTTP Response Headers in OpenLiberty

```xml [1-7|4]
<cors allowCredentials="true"
    allowedHeaders="Referer, Content-Type, Accept, Authorization" 
    allowedMethods="GET, DELETE, POST, PUT, OPTIONS, HEAD" 
    allowedOrigins="http://localhost:4200" 
    domain="/gravel-trapp/api" 
    maxAge="3600"/>
```
