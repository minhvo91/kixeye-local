# Deploying KIXEYE Test Application on MacOS using  Docker-compose

This project is using docker-compose to:
- Deploying KIXEYE Test Application on local MacOS machine

The requirement of application is: https://github.com/Kixeye/testapp/blob/master/README.md

## How to use

1. **Clone this repo to your machine**
```
Mac-Pro:~ minhvo$ git clone https://github.com/minhvo91/kixeye-local.git
```

2. **Create log file and set the owner to it**
```
Mac-Pro:~ minhvo$ sudo touch /var/log/testapp.log
Mac-Pro:~ minhvo$ sudo chown minhvo: /var/log/testapp.log
```
3. **Run docker-compose to deploy testapp application**
```
Mac-Pro:~ minhvo$ cd kixeye-local
Mac-Pro:kixeye-local minhvo$  nohup docker-compose up >> /var/log/testapp.log & 
[1] 1771
```

4. **Check the app if it is up and running correctly**
```
Mac-Pro:kixeye-local minhvo$  curl http://localhost:8080/leaderboard
[{"userId":3,"score":-602093007},{"userId":4,"score":-355135759}]
```

5. **Checking the log**
```
Mac-Pro:kixeye-local minhvo$ tail -n100 /var/log/testapp.log 
Starting testapp_redis.local_1 ... done
Starting testapp_app_1         ... done
Attaching to testapp_redis.local_1, testapp_app_1
redis.local_1  | 1:C 17 Apr 2019 03:08:28.580 # oO0OoO0OoO0Oo Redis is starting oO0OoO0OoO0Oo
redis.local_1  | 1:C 17 Apr 2019 03:08:28.580 # Redis version=5.0.4, bits=64, commit=00000000, modified=0, pid=1, just started
redis.local_1  | 1:C 17 Apr 2019 03:08:28.580 # Configuration loaded
redis.local_1  | 1:M 17 Apr 2019 03:08:28.583 * Running mode=standalone, port=6379.
redis.local_1  | 1:M 17 Apr 2019 03:08:28.583 # WARNING: The TCP backlog setting of 511 cannot be enforced because /proc/sys/net/core/somaxconn is set to the lower value of 128.
redis.local_1  | 1:M 17 Apr 2019 03:08:28.583 # Server initialized
redis.local_1  | 1:M 17 Apr 2019 03:08:28.583 # WARNING you have Transparent Huge Pages (THP) support enabled in your kernel. This will create latency and memory usage issues with Redis. To fix this issue run the command 'echo never > /sys/kernel/mm/transparent_hugepage/enabled' as root, and add it to your /etc/rc.local in order to retain the setting after a reboot. Redis must be restarted after THP is disabled.
redis.local_1  | 1:M 17 Apr 2019 03:08:28.583 * DB loaded from disk: 0.000 seconds
redis.local_1  | 1:M 17 Apr 2019 03:08:28.583 * Ready to accept connections
app_1          | 03:08:30 [leaderboard-akka.actor.default-dispatcher-4] INFO  akka.event.slf4j.Slf4jLogger - Slf4jLogger started
app_1          | 03:08:30 [main] INFO  kixeye.testapp.Redis$ - generated scores: List((-1.953091954E9,1), (4.06409498E8,2), (9.58435101E8,3), (-1.206122703E9,4))
app_1          | 03:08:30 [leaderboard-akka.actor.default-dispatcher-4] INFO  kixeye.testapp.Main$ - Loaded data into Redis
app_1          | 03:08:30 [Main-akka.actor.default-dispatcher-3] INFO  akka.event.slf4j.Slf4jLogger - Slf4jLogger started
app_1          | 03:08:54 [Main-akka.actor.default-dispatcher-4] TRACE kixeye.testapp.routes.Leaderboard - HTTP request for leaderboard
app_1          | 03:08:54 [leaderboard-akka.actor.default-dispatcher-2] DEBUG kixeye.testapp.RequestHandler - getting leaderboard from redis
app_1          | 03:08:54 [scala-execution-context-global-24] DEBUG kixeye.testapp.RequestHandler - got leaderboard: List(LeaderboardEntry(1,-1953091954), LeaderboardEntry(4,-1206122703))
app_1          | 03:08:54 [Main-akka.actor.default-dispatcher-4] DEBUG kixeye.testapp.routes.Leaderboard - Got status response List(LeaderboardEntry(1,-1953091954), LeaderboardEntry(4,-1206122703)) for HTTP leaderboard request
app_1          | 03:08:59 [Main-akka.actor.default-dispatcher-2] TRACE kixeye.testapp.routes.Leaderboard - HTTP request for leaderboard
app_1          | 03:08:59 [leaderboard-akka.actor.default-dispatcher-3] DEBUG kixeye.testapp.RequestHandler - getting leaderboard from redis
app_1          | 03:08:59 [scala-execution-context-global-24] DEBUG kixeye.testapp.RequestHandler - got leaderboard: List(LeaderboardEntry(1,-1953091954), LeaderboardEntry(4,-1206122703))
app_1          | 03:08:59 [Main-akka.actor.default-dispatcher-2] DEBUG kixeye.testapp.routes.Leaderboard - Got status response List(LeaderboardEntry(1,-1953091954), LeaderboardEntry(4,-1206122703)) for HTTP leaderboard request
```



