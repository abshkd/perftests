Here we see improvement with timeouts being specified for zuul. Default is 10 seconds.

```
ribbon:
    okhttp:
        enabled: true
    eureka:
        enabled: true
zuul: 
    host:
        max-total-connections: 5000
        max-per-route-connections: 4000
        socket-timeout-millis: 1000
        connect-timeout-millis: 250
        time-to-live: 500
```

```
ab -n 10000 -c 100 http://localhost:8080/store/
This is ApacheBench, Version 2.3 <$Revision: 1706008 $>
Copyright 1996 Adam Twiss, Zeus Technology Ltd, http://www.zeustech.net/
Licensed to The Apache Software Foundation, http://www.apache.org/

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

Document Path:          /store/
Document Length:        255 bytes

Concurrency Level:      100
Time taken for tests:   115.280 seconds
Complete requests:      10000
Failed requests:        9822
   (Connect: 0, Receive: 0, Length: 9822, Exceptions: 0)
Non-2xx responses:      178
Total transferred:      35932166 bytes
HTML transferred:       29914092 bytes
Requests per second:    86.75 [#/sec] (mean)
Time per request:       1152.795 [ms] (mean)
Time per request:       11.528 [ms] (mean, across all concurrent requests)
Transfer rate:          304.39 [Kbytes/sec] received

Connection Times (ms)
              min  mean[+/-sd] median   max
Connect:        0    0   0.3      0      23
Processing:   940 1146 164.9   1202    2526
Waiting:      940 1145 164.9   1202    2526
Total:        940 1146 165.0   1202    2527

Percentage of the requests served within a certain time (ms)
  50%   1202
  66%   1235
  75%   1247
  80%   1255
  90%   1275
  95%   1299
  98%   1416
  99%   1908
 100%   2527 (longest request)

```
