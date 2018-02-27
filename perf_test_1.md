```
Timeout is 5 seconds.
Proxied service responds exponentially slow to beyond 5 seconds. 
```
### Application.yml
```
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

Server Software:        
Server Hostname:        localhost
Server Port:            8080

Document Path:          /theme/
Document Length:        7 bytes

Concurrency Level:      200
Time taken for tests:   530.610 seconds
Complete requests:      10000
Failed requests:        0
Total transferred:      5170000 bytes
HTML transferred:       70000 bytes
Requests per second:    18.85 [#/sec] (mean)
Time per request:       10612.198 [ms] (mean)
Time per request:       53.061 [ms] (mean, across all concurrent requests)
Transfer rate:          9.52 [Kbytes/sec] received

Connection Times (ms)
              min  mean[+/-sd] median   max
Connect:        0    7  82.0      0     998
Processing:   813 10502 716.1  10553   11990
Waiting:      806 10502 716.1  10553   11990
Total:        816 10509 716.0  10554   12868

Percentage of the requests served within a certain time (ms)
  50%  10554
  66%  10603
  75%  10642
  80%  10667
  90%  10743
  95%  10849
  98%  11009
  99%  11177
 100%  12868 (longest request)
```
