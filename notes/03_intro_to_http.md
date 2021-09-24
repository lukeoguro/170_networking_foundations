# Intro to HTTP

## What to focus on

* Develop a clear understanding of the role of HTTP
  * HTTP works in combination with different technologies
* Break things down into individual components
  * Ensure clarity by breaking down concepts like HTTP and URLs into specific components

## The application layer

* The Application layer is the topmost layer, but it is important to note that this is note the application itself
* Instead, it is a set of protocols that provide communication to applications
* It focuses on the structure of the message and the data it should contain
* Protocols of the Application layer includes FTP for file transfer, SMTP for email, and HTTP for web

## Web

* The web is a service that can be accessed via the internet
* It is a vast information system that can be navigated via URL (Uniform Resource Locator)
* The web was created along HTML, URIs, and HTTP:
  * HTML (Hypertext Markup Language) is how the resource should be structured
  * URI (Uniform Resource Identifier) is the string of characters that identify the particular resource
  * HTTP (Hypertext Transfer Protocol) is the et of rules in which the resources are transferred

## HTTP

* HTTP is a system of rules that serve as a link between applications and the transfer of hypertext documents
* In HTTP, a client makes a request to a server and waits for the response
* It is referred to as the request response protocol
* A DNS (Domain Name System) maps the URL to IP address
  * It is a distributed database that translates domain names to IP addresses
  * Stored in DNS servers
* HTTP is a stateless protocol
  * Request/response pairs are completely independent from the previous one
  * This makes HTTP resilient, but also difficult to build stateful applications
* URL (Uniform Resource Locator) is a subset of URI, and has many components:
  * Scheme — `http`, `ftp`, `mailto` — not protocol
  * Host — `www.example.com` — where resource is hosted
  * Port — `:88` — only used when default isn't used (optional, default `80` for `http`, default `443` for `https`)
  * Path — `/home/` — where the local resource is located (optional)
  * Query string — `?item=book` — made up of query parameters (optional)
    * Have maximum length
    * Visible in URL so only for `GET` requests
    * Spaces and special characters like `&` cannot be used
    * Any characters outside the standard 128-character ASCII character set must be encoded
* HTTP request method is the verbs that tell the server what action to perform
  * Most common HTTP requests are `GET` and `POST`
  * `GET` should only retrieve content from the server (read only)
    * Browsers automatically pull referenced resources, while an HTTP tool will not
    * Required parts are in the request-line are HTTP method, path, version; host is required in the header; all other headers and body are optional
  * `POST` changes values that are stored on the server (typically by submitting data)
    * `Content-Type` header should be `application/x-www-form-urlencoded`
    * Message body is important
* HTTP responses rae the raw data returned by the server
  * Status code is required; headers, and message body is optional
* HTTP makes stateful web applications with sessions, cookies, and AJAX
  * Sessions
    * A unique token is called the session identifier (session id)
    * Server must check if a request contains a session identifier, whether it's still valid, retrieve session data
    * Session data is stored on the server
  * Cookies
    * Cookies contain session information (uses `set-cookie` in response headers)
  * AJAX
    * Stands for Asynchronous JavaScript and XML
    * Allows browsers to issue requests and process responses without a full page refresh
    * Asynchronously means page doesn't refresh
    * `callback` is piece of logic that can be passed on to some function after a certain event has happened
* Security measures:
  * Secure HTTP (HTTPS) makes sure every request/response is encrypted
    * TLS is used for encryption
  * Same-origin policy restricts interactions between resources from different origins (i.e., different scheme, port, or host)
    * What is restricted is typically API requests
    * CORS (cross-origin resource sharing) allows interactions that would typically be restricted
* Security threats:
  * Session hijacking when the session id is accessed
    * Resetting sessions each time a successful login is made
    * Expiration time on sessions
    * Using HTTPS to prevent access to session identifiers
  * Cross-site Scripting (XSS) when users can input HTML/JS directly onto the site
    * Without sanitization of input, browser will interpret the HTML and JS and execute it
    * You can sanitize user input
    * Escape all user input when displaying it (replace HTML character with a combination of ASCII characters)
* Some more details:
  * Client server consists of 3 main pieces: web server, application server, and data store
    * Web server handles static assets, application server handles more complicated requests, and data stores are relational databases that retrieve or create data
  * HTTP actually relies on TCP/IP connection most of the time
  * URL is a subset of URI that includes the network location of the resource
  * Web content is now created dynamically, and isn't necessary a path to a physical file
