---
title: CSA Deployment Pop Quiz
comments: true
layout: post
description: This blog guides you through some of the questions that Mr. Mortensen could ask on the pop quiz. 
courses: { csa: {week: 21} }
categories: [C1.4]
---

# Show JWT signup and/or login process

- Step 1 (Client - Login Request):
    - The client sends a login request with user credentials (username and password) to the /authenticate endpoint.
- Step 2 (JwtApiController)
    - The JwtApiController receives the login request.It authenticates the user credentials using the AuthenticationManager.
    - If authentication is successful:
      - Retrieves user details using the PersonDetailsService.
      - Generates a JWT using the JwtTokenUtil.
      - Sends the JWT as an HTTP-only secure cookie in the response.
- Step 3 (Client - Subsequent Requests:
The client includes the JWT cookie in the headers of subsequent requests.
- Step 4 (JwtRequestFilter):
    - For each incoming request, the JwtRequestFilter intercepts the request.
    - Extracts the JWT from the HTTP request headers or cookies.
    - Validates the JWT using the JwtTokenUtil.
    - If the token is valid, sets up authentication using Spring Security's SecurityContextHolder.
- Step 5 (Spring Security):
    - The application can now authorize the user based on the roles and permissions Spring Security processes the request with the authenticated user.
    associated with the JWT.
- Cookies: You can store the JWT in a cookie and send it back to the server with each request. This is a simple and widely-supported option, but it has some limitations. For example, you can’t access cookies from JavaScript on a different domain, and some users may have cookies disabled in their browser settings.
- Local storage: You can store the JWT in the browser’s local storage (localStorage) or session storage (sessionStorage). This option allows you to access the JWT from JavaScript on the same domain, but it is vulnerable to cross-site scripting (XSS) attacks, where an attacker can inject malicious code into your application and steal the JWT from the storage.
- HttpOnly cookie: You can store the JWT in an HttpOnly cookie, which is a cookie that can only be accessed by the server and not by client-side JavaScript. This option provides some protection against XSS attacks, but it is still vulnerable to other types of attacks, such as cross-site request forgery (CSRF).

# Explain a POJO and changes to a POJO 

1. POJO:
   - "Plain Old Java Object" - Java class that adheres to a set of conventions to keep its structure simple. It does not extend or implement specialized classes or interfaces, making it a plain and standard Java object.

2. POJO Characteristics:
   - Having private fields, a public no-argument constructor, getter and setter methods for its fields, and possibly additional business logic methods.

3. POJO Changes:
   - Adding, modifying, or removing fields, as well as updating methods to reflect the new structure or behavior. It's important to ensure that the changes are backward-compatible if the POJO is used in a serialized or persisted form.

# Explain security configuration rules that are required for access

- Implementation Approaches and Security Considerations
- JWTs are signed to ensure they cannot be modified in transit. Signature is a crucial aspect of JWT security.
Key Usage
- Token Issuance: When the token is issued by the authorization server, it is signed with a key.
- Token Reception: When the client receives the token, the signature is validated using the key.


```java
public class TokenReceptionExample {
    // Simulate receiving a token from the client
    private static String receiveTokenFromClient() {
        // In a real scenario, this would be received from the client (e.g., from a request header)
        return "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiAiMTIzIiwgImV4cCI6IDE2MjM5NzYzODF9.4X1lC5fU4dV1n9l02LZyGQSy5K-O5fnZM0t6eO-w2Qs";
    }
    public static void main(String[] args) {
        // Example of Token Reception
        String receivedToken = receiveTokenFromClient();
        System.out.println("Received Token: " + receivedToken);
    }
}
```

- Symmetric vs. Asymmetric Key Approaches
- Symmetric Key: A single secret key is used both to sign and validate the token.
- Asymmetric Key: Different keys are used to sign and validate the token, only the authorization server has the ability to sign it.

```java
public class SymmetricKeyValidationExample {
    // Symmetric Key for Token Signing and Validation
    private static Key symmetricKey = Keys.secretKeyFor(io.jsonwebtoken.SignatureAlgorithm.HS256);
    // Token Validation with Symmetric Key
    private static Claims validateTokenSymmetric(String token) {
        try {
            // Parse and verify the token using the symmetric key and the HS256 algorithm
            Jws<Claims> claimsJws = Jwts.parserBuilder().setSigningKey(symmetricKey).build().parseClaimsJws(token);
            return claimsJws.getBody();
        } catch (ExpiredJwtException e) {
            // Handle case where the token has expired
            System.out.println("Token has expired");
        } catch (MalformedJwtException e) {
            // Handle case where the token is invalid (e.g., tampered with)
            System.out.println("Invalid token");
        }
        return null;
    }
    public static void main(String[] args) {
        // Example of Token Validation with Symmetric Key
        String receivedToken = receiveTokenFromClient();
        Claims validatedClaims = validateTokenSymmetric(receivedToken);
        if (validatedClaims != null) {
            System.out.println("Validated Payload: " + validatedClaims);
        }
    }
}
```

- Additional Security Considerations
    - Token Scope: limit token access to specific resources or actions
    - Token Revocation: implement mechanism to revoke token if user’s access needs to be taken away
    - Token Encryption: encrypt token if it contains sensitive information that shouldn’t be visible (even if intercepted)
    - Regular Key Rotation: rotate keys regularly for security and to limit the impact of compromised key
- Implementation Approaches and Security Considerations
- JWTs are signed to ensure they cannot be modified in transit. Signature is a crucial aspect of JWT security.

Key Usage
- Token Issuance: When the token is issued by the authorization server, it is signed with a key.
- Token Reception: When the client receives the token, the signature is validated using the key.




```java
public class TokenReceptionExample {
    // Simulate receiving a token from the client
    private static String receiveTokenFromClient() {
        // In a real scenario, this would be received from the client (e.g., from a request header)
        return "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiAiMTIzIiwgImV4cCI6IDE2MjM5NzYzODF9.4X1lC5fU4dV1n9l02LZyGQSy5K-O5fnZM0t6eO-w2Qs";
    }
    public static void main(String[] args) {
        // Example of Token Reception
        String receivedToken = receiveTokenFromClient();
        System.out.println("Received Token: " + receivedToken);
    }
}
```

```java
public class SymmetricKeyValidationExample {
    // Symmetric Key for Token Signing and Validation
    private static Key symmetricKey = Keys.secretKeyFor(io.jsonwebtoken.SignatureAlgorithm.HS256);
    // Token Validation with Symmetric Key
    private static Claims validateTokenSymmetric(String token) {
        try {
            // Parse and verify the token using the symmetric key and the HS256 algorithm
            Jws<Claims> claimsJws = Jwts.parserBuilder().setSigningKey(symmetricKey).build().parseClaimsJws(token);
            return claimsJws.getBody();
        } catch (ExpiredJwtException e) {
            // Handle case where the token has expired
            System.out.println("Token has expired");
        } catch (MalformedJwtException e) {
            // Handle case where the token is invalid (e.g., tampered with)
            System.out.println("Invalid token");
        }
        return null;
    }
    public static void main(String[] args) {
        // Example of Token Validation with Symmetric Key
        String receivedToken = receiveTokenFromClient();
        Claims validatedClaims = validateTokenSymmetric(receivedToken);
        if (validatedClaims != null) {
            System.out.println("Validated Payload: " + validatedClaims);
        }
    }
}
```

# Describe docker and process for update docker application


1. Deployment steps simplified:
    - Log into AWS and create an instance then connect to it
    - Name
    - Application and OS Machine Image set to Ubuntu 22.04 64 bit x86
    - Instance Type set to Default (t2.micro)
    - Key Pair (ssh), you do not need these (unless you want to connect over ssh), so set to “Proceed without a key pair”
    - Allow SSH (you do not want to change it later), HTTPS, and HTTP. It will ask you to make or use a new ruleset. You may use ours (it does what was just stated) called ‘launch-wizard-145’.
    - Leave Configure Storage default
    - Run docker ps to see which ports you can use
    - Run git clone {your backend}
    - Navigate to it using cd in /deployments
2. Dockerfile:

```
# syntax=docker/dockerfile:1
FROM openjdk:18-alpine3.13
WORKDIR /app
RUN apk update && apk upgrade && \
    apk add --no-cache git 
COPY . /app
RUN ./mvnw package
CMD ["java", "-jar", "target/spring-0.0.1-SNAPSHOT.jar"]
EXPOSE 8---
```
docker-compose.yml
```
version: '3'
services:
  web:
    image: your_image_name
    build: .
    ports:
      - "8---:8085"
    volumes:
       - ./volumes:/volumes
    restart: unless-stopped
```
```docker-compose up -d```
```curl localhost:8—``` to check if build is successful

Route 53 setup
Go to stu.nighthawkcodingsociety.com section in Route 53
Create record with record type as A; in the value box, put in the public IPv4 address of your EC2 Instance (the one you have your website on). Everything else can remain default, and you can create your record.

```cd /etc/nginx/sites-available```

server {
    listen 80;
     listen [::]:80;
     server_name -----.stu.nighthawkcodingsociety.com ; # change server name to your domain
     location / {
         proxy_pass http://localhost:8---; # change port to yours
         if ($request_method ~* "(GET|POST|PUT|DELETE)") {
                 add_header "Access-Control-Allow-Origin"  "https://nighthawkcoders.github.io"p;
         }
         if ($request_method = OPTIONS ) {
                 add_header "Access-Control-Allow-Origin"  "https://nighthawkcoders.github.io";
                 add_header "Access-Control-Allow-Methods" "GET, POST, PUT, DELETE, OPTIONS, HEAD"; # request methods above match here
                 add_header "Access-Control-Allow-Headers" "Authorization, Origin, X-Requested-With, Content-Type, Accept";
                 return 200;
         }
     }
 }
Create symbolic link → ```cd /etc/nginx/sites-enabled``` →

```ln -s /etc/nginx/sites-available/{someuniqueprojectname} /etc/nginx/sites-enabled/```
```nginx -t```
```sudo systemctl restart nginx```
```sudo certbot --nginx```

For code updates:
```docker-compose down``` → ```git pull``` → ./mvnw clean → ```docker-compose up -d --build```
Verify using docker ps, docker-compose ps, and curl

# Describe route 53 and process for domain setup

- With Amazon Route 53 specifically (what we use on AWS), we can translate something like example.com to numeric IP addresses
- Asks a server (DNS recursive resolver) to find the unique number (IP address) linked to the website typed in (ex nytimes.com)
- Checks the website’s main category (Top Level Domain) using a master server (root nameserver) that lists all websites in each category 
- Requests the specific category server (TLD nameserver) to locate the correct unique number (IP address) 
- The category server gets the unique number and passes it to the main website server (authoritative nameserver) to confirm it’s right 
- The main website server contacts the number and waits for a correct reply to confirm it’s the right one for the website you need 
- If the unique number is right, the main website server sends it back to your internet browser 
- Your web browser receives the correct unique number and starts loading the webpage!
- AWS Route 53 allows us to take one domain and split it into multiple domains while linking them to our EC2 instances by the IP Addresses and the nginx configuration of the instances.

# Show API access code and error handling, specifically redirect on 403


Error Handling - JwtAuthenticationEntryPoint):

If the JWT is missing, invalid, or expired, and the request requires authentication, the JwtAuthenticationEntryPoint handles the authentication failure.
Responds with an HTTP 401 (Unauthorized) status.


# Describe managing CORS policies through Nginx and Java

Cross origin resource sharing, or cors, is something that configures security for requests with additional headers and can restrict what kind of requests and where the requests come from.

SecurityConfig.java:

```java
               .authorizeHttpRequests(auth -> auth // set which endpoints need authentication
					.requestMatchers("/authenticate").permitAll() // okay
					.requestMatchers("/mvc/person/update/**", "/mvc/person/delete/**").authenticated() // needs auth
					.requestMatchers("/api/person/**").authenticated() // needs auth
					.requestMatchers("/**").permitAll() // everything except for the specified above does not need auth
				)
				// support cors
				.cors(Customizer.withDefaults())
				.headers(headers -> headers
					.addHeaderWriter(new StaticHeadersWriter("Access-Control-Allow-Credentials", "true")) // headers
					.addHeaderWriter(new StaticHeadersWriter("Access-Control-Allow-ExposedHeaders", "*", "Authorization")) // allow exposed headers
					.addHeaderWriter(new StaticHeadersWriter("Access-Control-Allow-Headers", "Content-Type", "Authorization", "x-csrf-token")) // more headers
					.addHeaderWriter(new StaticHeadersWriter("Access-Control-Allow-MaxAge", "600")) // Time for headers until they expire
					.addHeaderWriter(new StaticHeadersWriter("Access-Control-Allow-Methods", "POST", "GET", "OPTIONS", "HEAD")) // Methods that can go to the server
					.addHeaderWriter(new StaticHeadersWriter("Access-Control-Allow-Origin", "https://nighthawkcoders.github.io", "http://localhost:4000", "*")) // Locations that can send and receive requests to the backend
				)
```


# Describe reverse proxy of server_name to proxy_pass

The nginx block above is the configuration that links nginx to your docker process using a reverse proxy to forward the configured domain to the configured port. For CORS Headers, there are two modes: simple requests and preflighted requests. Simple requests are requests that have no implications and are not dangerous for the user or for the server, or simple data. Preflighted requests handle more complex and sensitive data, where the browser first sends a request through the OPTIONS method, and then the server responds to determine if the request is safe to proceed.

There are two directives to this example: server_name and proxy_pass.

server_name basically links the domain name to nginx for the server configuration. proxy_pass will then forward the requests made to the server with the “tag” for the domain name to the proxy_pass, which is the address for the localhost backend server corresponding to the domain name with server_name.







