# JWT (JSON Web Token)

JWTs are JSON data, encoded as a string, and cryptographically signed. It's really just JSON data that you can verify came from someone you know.

- JWTs don't try to encrypt your data: they simply help you verify the author. Hence the most common use case for JWTs is authentication.
- JWTs are stateless (this is probably the single biggest reason people like using JWTs). So the server can validate this token locally without making any network requests, talking to a database, etc. -> session management is faster, you just need to run a bit of code.
- JWTs allow you to delegate authentication to a third-party server (called authentication server), though it's not always the case
- As a bonus benefit, as the webapp creator you can embed other information about the user into your JWT: user permissions, personal informati, etc.
- JWTs can be symmetrically or asymmetrically signed: they will provide the same guarantees.



"Cookies vs JWT makes no sense. You can put the JWT in a cookie if you want to.. apples and oranges."
 	
"Yeah, but when people say cookies vs JWT, what they mean is:
Cookies: a simple session ID, a random number, stored in a cookie.
JWT: a JSON object stored in local storage that specifies authorization of some user that is authenticated by public key cryptography. JWTs can be configured in many ways, but this is what people usually mean because they want their sessions to be "stateless."



## Composition

Before encoding, JWTs are composed of key-values pairs, called claims (the core of JWT).

A JWT token is composed of 3 base64'd parts separated by a dot:

- header
- payload
- signature

A JWT typically looks like the following:
xxxxx.yyyyy.zzzzz



## Cookies vs tokens

### Cookies

- old
- max 4 kB
- header: {"Set-Cookie": "session=signed(12345)"}
- can specify stuff: "HttpOnly" (no js plz), "SameSite=strict" (no X-origin cookie sharing), "secure" (SSL only)
- stateful: session info is kept on both client and server (which checks session_id sent by client with every request)

basically a stateful token

### Tokens

- new
- used for API and SPA
- stateless, the server doesn’t keep anything.

The token can be sent:

1. generally as an additional Authorization header in form of “Bearer <JWT>”
2. can also be sent in the body of a POST request
3. or as a query parameter (in the url)

Functionning

1. User enters their login credentials
2. Server verifies the credentials are correct and returns a signed token
3. This token is stored client-side, most commonly in local storage - but can be stored in session storage or a cookie as well
4. Subsequent requests to the server include this token as an additional Authorization header or through one of the other methods mentioned above
5. The server decodes the JWT and if the token is valid processes the request
6. Once a user logs out, the token is destroyed client-side, no interaction with the server is necessary


## Pros and cons of JWT

### Pros

- **Self-contained**: a token can be self-contained (hence stateless). It has all the information it needs for authentication. This is great for scalability as it frees your server from having to store session state.
- **Tokens can be generated from anywhere**: token generation is decoupled from token verification, allowing you the option to handle the signing of tokens on a separate server or even through a different company such us Auth0.
- **Fine-grained access control**: Within the token payload you can easily specify user roles and permissions as well as resources that the user can access.
- **Compact**: JSON is encoded in base64. Though bigger than a typical cookie, a JWT is typically small, so it can be sent through a URL, a POST parameter, or inside a HTTP header (in addition to faster transmission)


### Cons

- **Far bigger than a cookie**: (biggest disadvantage) A session cookie is relatively tiny compared to even the smallest JWT. The token size can grow out of control if you add many claims to it. Like cookies, each request to the server must include the JWT.
Ex:
User: abc123 in a cookie: 6 bytes, in a JWT: 304 bytes (header fields + secret)
- **Requires a library/developer code to work**: cookies are frictionless
- **Complex spec**: support varies from one library ot another
- - **Prevents CSRF but not XSS**
- **Doesn't require consent**
- **Doesn't prevent mistakes**: JWTs looks encrypted but usually aren't (just based64 encoded). Anyone can view the data inside the JWT, without a key. It also doesn't prevent bungled implementations, allowing empty algorithm for instance (tptacek: "it's a snakepit of implementation traps that create vulnerabilities")
- **Most websites will need a user db anyways**: therefore not taking advantage of the stateless benefits of a JWT.
- **Require CPU to compute cryptographic signatures**: slower
