---
layout: post
title: Understanding OPTIONS Requests in HTTP
published-on: '2023-03-28'
categories: HTTP, CORS, Web Development
image: images/http2.png
---

When we talk about HTTP requests, most people think about the well-known methods such as GET, POST, PUT, DELETE, etc. However, there's another method that is also essential in some cases: the OPTIONS method. In this article, we'll explore what an OPTIONS request is, how it works, how it has evolved throughout the years, and its usage for Cross-Origin Resource Sharing (CORS).

## What is an OPTIONS Request?

The OPTIONS method is an HTTP method used to retrieve information about the communication options available for a resource. It's a "meta" method, which means it doesn't request the resource itself but rather its metadata. It is used to determine the communication options available for a resource before sending a request for it. An OPTIONS request can be sent to any resource, but it's most commonly used with CORS.

## How it Works

An OPTIONS request works similarly to other HTTP requests, but instead of requesting a resource, it requests metadata about the resource. The request includes an HTTP header called `Access-Control-Request-Method`, which specifies the HTTP method that will be used for the actual request if the server allows it. The server then responds with an HTTP header called `Access-Control-Allow-Methods`, which lists the HTTP methods that the server allows for that resource. If the server doesn't allow the requested method, it will respond with an error.

## Evolution of OPTIONS Request

The OPTIONS method was first introduced in HTTP/1.1 as part of the CORS specification. In HTTP/1.0, the same functionality was achieved by using the `GET` method with an asterisk `*` as the resource URL. In HTTP/1.1, the `OPTIONS` method was introduced to provide a more standardized way of retrieving the available communication options for a resource. With the introduction of HTTP/2 and later HTTP/3, the OPTIONS method has remained essentially the same.

## Caching

By default, an OPTIONS request is not cached, and each request results in a round trip to the server. However, the server can send a `Cache-Control` header to indicate that the response can be cached for a certain period. If the response is cached, subsequent requests for the same resource can be served from the cache, reducing network traffic and improving performance.

## Usage for CORS

Cross-Origin Resource Sharing (CORS) is a security feature implemented by web browsers that restricts resources on a web page from being requested from another domain. When a web page tries to request a resource from a different domain, the browser sends an OPTIONS request to the server to determine if the server allows the request. If the server allows the request, the browser sends the actual request to the server. This mechanism prevents malicious scripts from accessing sensitive data on other domains.

Here's an example of how an OPTIONS request can be used for CORS:

Suppose a web page hosted on `https://www.example.com` wants to request a resource from `https://api.example.com`. The browser will first send an OPTIONS request to `https://api.example.com` with the `Access-Control-Request-Method` header set to the HTTP method that the web page wants to use (e.g., GET). If the server allows the request, it responds with the `Access-Control-Allow-Methods` header set to a list of HTTP methods that are allowed for that resource. The browser then sends the actual request to the server, and if the server allows it, it responds with the requested resource.

```
<!-- Request -->
OPTIONS /resource HTTP/1.1
Host: api.example.com
Access-Control-Request-Method: GET
Origin: https://www.example.com

<!-- Response -->
HTTP/1.1 200 OK
Access-Control-Allow-Methods: GET, POST, PUT, DELETE
Access-Control-Allow-Origin: https://www.example.com
Cache-Control: max-age=3600
```

In this example, the OPTIONS request is sent to `https://api.example.com/resource\` with the `Access-Control-Request-Method` header set to `GET`. The server responds with the `Access-Control-Allow-Methods` header set to `GET, POST, PUT, DELETE`, indicating that these HTTP methods are allowed for the requested resource. The `Access-Control-Allow-Origin` header is also set to `https://www.example.com\`, indicating that requests from that domain are allowed. Finally, the `Cache-Control` header is set to indicate that the response can be cached for 3600 seconds.

## Conclusion
In conclusion, the OPTIONS method is an HTTP method used to retrieve information about the communication options available for a resource. It is most commonly used with CORS to determine if a web page is allowed to request a resource from a different domain. The OPTIONS method has evolved from using the `GET` method with an asterisk `*` in HTTP/1.0 to a standardized method in HTTP/1.1 and later versions. While an OPTIONS request is not cached by default, servers can send a `Cache-Control` header to indicate that the response can be cached for a certain period.





