# localtunnel

This Docker container mimics ngrok or localtunnel, but without having their restrictions (timeouts, rate limits). With the help of certbot, TLS connections are also possible. 

This Docker container is configured so that all incoming requests on port 80 and 443 are forwarded to 8080 using nginx. When using

```
ssh -i ./id_rsa -R 8080:localhost:8080 development@example.org -p 8085
```

a domain can be accessed via TLS to data served from a local machine. This is only suitable for development purposes (e.g. Microsoft Teams Apps).
