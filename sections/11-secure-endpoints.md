<!-- .slide: data-background="img/background/binary-code.jpg" data-background-color="black" data-background-opacity="0.2" -->

## Secure Endpoints

let's secure the 'enter race result' endpoint
using **Jakarta Security** and the **MicroProfile JWT** feature

<https://pxhere.com/en/photo/1458897> <!-- .element: class="attribution" -->

---

## On JWT Structure

Every JWT consists of three parts:

<ul>
  <li class="fragment fade-in-then-semi-out"><strong>Header:</strong> contains the type of the token and the signing algorithm used.
  <li class="fragment fade-in-then-semi-out"><strong>Payload:</strong> contains the claims, which are the statements about an entity (typically the user) and additional data.
  <li class="fragment fade-in-then-semi-out"><strong>Signature:</strong> created by taking the encoded header and payload, a secret key, and the algorithm specified in the header.
</ul>

(<https://jwt.io>)

---

## On JWT Validation Steps

<ol>
  <li class="fragment fade-in-then-semi-out"><strong>Decoding.</strong> The token is split into its three parts and <code>base64</code> decoded.
  <li class="fragment fade-in-then-semi-out"><strong>Validating the Signature.</strong> The signature is recreated using the same header, payload, algorithm and secret key. If both signatures match, the token has not been altered and so can be considered valid.
  <li class="fragment fade-in-then-semi-out"><strong>Checking Claims.</strong> The claims in the payload are checked against the values the application expects (like expiration time, issuer, audience).
</ol>

If all these steps succeed, the token is valid. <!-- .element class="fragment" -->
