# JWT (Json Web Token)

## Public and Private Cryptography:

__Cryptography__ is a very good security mechanism which generate ywo keys.
- __Public Key:__ we can share it with anyone as many as we want, how many data is encrypted by this public key can be decrypted only using my private key only. 
- __Private Key:__ It is most secured key, which should not be shared

## Stateless and StateFull:
- __Stateless:__ It's state is never stored in any file or any database. (JWT is a stateless mechanism)
- __Statefull:__ It's state is stored in any file or any database.

## What is JWT?
- JWT stands for JSON Web Token. 
- It is an encrypted token which is a random collection of letters and numbers. 
-It is secure key or communication key between two resources. 
- The main function of JWT is to collect data, then encrypt it and decides on the server who can decrypt the collected data.

## Structure of a JWT:
- Ex: 
```
<span style="color: red">eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9</span>.
<span style="color: purple">eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ</span>.
<span style="color: skyblue">SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c</span>
```

- It contains three parts which are separated by the dots.
- 1. First part which is the red string, which determines that which algorithm it's using
- 2. Second part which is the purple string, which determines that which information you have
- 3. Third part which is the blue string, which is the signature which determines if there is any manipulation or not 

- If someone change any small character on this token then the whole algorithm will be changed, only works when it is in the exact same sequence

### If we Decode JWT
- After decoding jwt we got 3 components
- __1. HEADER:__ which contains which algorithm we are using and the type
```
{
  "alg": "HS256", // by default the algorithm is HS256
  "typ": "JWT"
}
```
- __2. PAYLOAD:__ which contains the information
```
{
  "_id": "1234567890", // we can get the information from the database using this id
  "name": "John Doe", // contains the name
  "iat": 1516239022 // Issued at (seconds since unix epoch)
}
```
- __3. Verify Signature:__ it contains the manipulation
```
HMACSHA256(
  base64UrlEncode(header) + "." +
  base64UrlEncode(payload),
  
your-256-bit-secret // it will generate the actual private key 

) secret base64 encoded
```

## Authentication vs Authorization:

- Authentication is the process of verifying the identity of a user.
EX: verifying usermname, email

- Authorization determines what actions a user is allowed to perform.
EX: if you are a user you are allowed to access the user dashboard, not the admin dashboard

## How do you securely store a JWT on the client-side

- It is a short lived token, so it is already secured, and if any boday can steal the jwt token the he/she can easily steal the cookies and sessions also.
- But it also have security protection mechanism:
- __1. LocalStorage:__ you can save the tokens in your local storage but there is some attacks ocuured is javascript like `XSS(Cross Site Scripting)` attack by which javascript can access your local storage and the token will be taken.
- __2. Session Storage:__ you can save the tokens in your session storage also
- __3. Cookies:__ you can save the tokens in your cookies, after you can on the flags like `httponly`, `secure`, then javascipt can not access the cookies
__But the best way to secure it by reducing the span__

## Common usecases of JWT:
- Authentication
- Authorization
- Information Exchange (payload - server to server also)

## How can you ivalidate JWT:
- After implementing each and every JWT, you got the expiry with that, Now its upto you how many times you want to excess it or reduce it
- It has another mechanism which is known as `refresh token`
- A refresh token in JWT (JSON Web Token) is a special token used to obtain a new access token once the current access token expires. Unlike access tokens, which have short lifespans for security reasons, refresh tokens have longer lifespans and can be stored securely. When the access token expires, the refresh token is sent to the authentication server to request a new access token, maintaining user sessions without requiring them to log in repeatedly. This mechanism enhances both security and user experience in token-based authentication systems.

## JWT vs SESSIONS:

- __JWT (JSON Web Token):__
    - JWT is a stateless mechanism for authentication and authorization.
    - It is an encrypted token that contains information about the user.
    - JWTs are self-contained and can be easily transmitted between systems.
    - They are typically used in stateless environments like APIs.
    - JWTs have an expiration time and can be invalidated by setting a shorter lifespan.
    - They are commonly used for single sign-on (SSO) and information exchange.

- __Sessions:__
    - Sessions are a server-side mechanism for authentication and authorization.
    - Sessions store user data on the server and issue a session ID to the client.
    - The session ID is typically stored in a cookie or passed in the request headers.
    - Sessions require server-side storage and management.
    - They can be used in stateful environments like web applications.
    - Sessions can be invalidated by destroying the session data on the server.

In summary, JWTs are suitable for stateless environments and are commonly used in APIs, while sessions are suitable for stateful environments like web applications and require server-side storage. The choice between JWTs and sessions depends on the specific requirements of the application and the desired level of security and scalability.

