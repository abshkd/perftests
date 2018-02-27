```
Using Edgware.SR2 Not any better.

ribbon:
    okhttp:
        enabled: true
    eureka:
        enabled: true
# See http://cloud.spring.io/spring-cloud-netflix/spring-cloud-netflix.html
zuul: # those values must be configured depending on the application specific needs
    host:
        max-total-connections: 500
        max-per-route-connections: 400
    routes:
        theme:
            path: /theme/**
            url: http://localhost/
# See https://github.com/Netflix/Hystrix/wiki/Configuration
hystrix:
    command:
        default:
            execution:
                isolation:
                    thread:
                        timeoutInMilliseconds: 5000
```

### benchmark

```
ab -n 10000 -c 200 http://localhost:8080/theme/

Benchmarking localhost (be patient)
Completed 1000 requests
Completed 2000 requests
Completed 3000 requests
Completed 4000 requests
Completed 5000 requests
Completed 6000 requests
Completed 7000 requests
Completed 8000 requests
Completed 9000 requests
Completed 10000 requests
Finished 10000 requests


Server Software:        
Server Hostname:        localhost
Server Port:            8080

Document Path:          /theme/
Document Length:        7 bytes

Concurrency Level:      200
Time taken for tests:   596.003 seconds
Complete requests:      10000
Failed requests:        0
Total transferred:      5170000 bytes
HTML transferred:       70000 bytes
Requests per second:    16.78 [#/sec] (mean)
Time per request:       11920.065 [ms] (mean)
Time per request:       59.600 [ms] (mean, across all concurrent requests)
Transfer rate:          8.47 [Kbytes/sec] received

Connection Times (ms)
              min  mean[+/-sd] median   max
Connect:        0    0   0.4      0       4
Processing:   495 11816 1698.9  11183   15805
Waiting:      485 11816 1698.9  11183   15805
Total:        498 11816 1698.8  11183   15805

Percentage of the requests served within a certain time (ms)
  50%  11183
  66%  11684
  75%  12896
  80%  13922
  90%  14347
  95%  14615
  98%  14876
  99%  15105
 100%  15805 (longest request)
```
