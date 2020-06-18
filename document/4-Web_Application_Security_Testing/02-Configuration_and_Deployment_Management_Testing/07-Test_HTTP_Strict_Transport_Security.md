# Test HTTP Strict Transport Security

|ID          |
|------------|
|WSTG-CONF-07|

## Summary

Web sites define the HTTP Strict Transport Security (HSTS) header to communicate to web browsers that all traffic exchanged with the given domain (and specified subdomains) should be sent over HTTPS for a given period of time. This will help protect information from being sent over unencrypted requests.

Considering the importance of HSTS it is prudent to verify that the web site is responding with the HSTS header to ensure all data between the web browser and server is encrypted.

HTTP Strict Transport Security (HSTS) lets a web application inform the browser through the use of a response header that it should never establish a connection to the the specified domain using HTTP. Instead, all requests to the specified domain will be automatically encrypted with HTTPS. 

The HTTP strict transport security header has two directives:

- max-age: to indicate the number of seconds that the browser should automatically convert all HTTP requests to HTTPS.
- includeSubDomains: to indicate the web application’s sub-domains that must use HTTPS.

An example of the HSTS header implementation:

`Strict-Transport-Security: max-age=60000; includeSubDomains`

The use of this header by web applications must be checked to find if the following security issues could be produced:

- Attackers sniffing the network traffic and accessing the information transferred through an unencrypted channel.
- Attackers exploiting a man in the middle attack due to the acceptance of certificates that are not trusted.
- Users who mistakenly enter a HTTP address in the browser instead of HTTPS.
- Users who click a link in a web application which mistakenly uses the HTTP protocol.

## How to Test

The presence of the HSTS header can be confirmed by examining the server's response through an interception proxy or by using CURL as follows:


```bash
$ curl -s -D- https://owasp.org | grep Strict
Strict-Transport-Security: max-age=15768000
```

## References

- [OWASP HTTP Strict Transport Security](https://cheatsheetseries.owasp.org/cheatsheets/HTTP_Strict_Transport_Security_Cheat_Sheet.html)
- [OWASP Appsec Tutorial Series - Episode 4: Strict Transport Security](https://www.youtube.com/watch?v=zEV3HOuM_Vw)
- [HSTS Specification](https://tools.ietf.org/html/rfc6797)
