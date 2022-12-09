# Challenge 15

## Load balanced server

### Instructions

Based on the project we are doing, add one more parameter in the command path that allows the server to be executed in fork or cluster mode. Said parameter will be 'FORK' in the first case and 'CLUSTER' in the second, and if it is not passed, the server will start in fork mode.

- Add in the info view, the number of processors present in the server.
- Run the server (FORK and CLUSTER modes) with nodemon checking the number of processes taken by node.
- Run the server (with the appropriate parameters) using Forever, verifying its correct operation. List processes by Forever and by operating system.
- Run the server (with the appropriate parameters: FORK mode) using PM2 in its fork mode and cluster modes. List processes by PM2 and by operating system.
- Both Forever and PM2 allow listening mode, so that the update of the server code is immediately reflected in all processes.
Test the completion of fork and cluster processes where appropriate.

Configure Nginx to load balance our server as follows:

- Redirect all queries to /api/randoms to a cluster of servers listening on port 8081. The cluster will be created from node using the native module cluster.
- The rest of the queries, redirect them to an individual server listening on port 8080.
- Verify that everything works correctly.
- Then, modify the configuration so that all queries to /api/randoms are redirected to a cluster of servers managed from nginx, distributing them evenly among 4 instances listening on ports 8082, 8083, 8084 and 8085 respectively.

Include the nginx configuration file along with the project.
Also include a small document detailing the commands that must be executed by command line and the arguments that must be sent to raise all the server instances so that they support the configuration detailed in the previous points.

Example:
- pm2 start ./miservidor.js -- --port=8080 --mode=fork
- pm2 start ./miservidor.js -- --port=8081 --mode=cluster
- pm2 start ./miservidor.js -- --port=8082 --mode=fork

### Solution

It was done directly with pm2 since this parameter allows receiving if you want it to be fork mode or cluster mode.

We generate 4 clusters in 8082, 8083, 8084 and 8085

```console

┬─[joseluis@joseluisabs:~/Desktop/Backend/Entrega-15]
╰─>$ pm2 start ./src/server.js --name="ClusterEn8082" --watch -i 2  -- -p 8082

┬─[joseluis@joseluisabs:~/Desktop/Backend/Entrega-15]
╰─>$ pm2 start ./src/server.js --name="ClusterEn8083" --watch -i 2  -- -p 8083

┬─[joseluis@joseluisabs:~/Desktop/Backend/Entrega-15]
╰─>$ pm2 start ./src/server.js --name="ClusterEn8084" --watch -i 2  -- -p 8084

┬─[joseluis@joseluisabs:~/Desktop/Backend/Entrega-15]
╰─>$ pm2 start ./src/server.js --name="ClusterEn8085" --watch -i 2  -- -p 8085

```



Check the list:

```console

┬─[joseluis@joseluisabs:~/Desktop/Backend/Entrega-15]
╰─>$ pm2 list
┌─────┬──────────────────┬─────────────┬─────────┬─────────┬──────────┬────────┬──────┬───────────┬──────────┬──────────┬──────────┬──────────┐
│ id  │ name             │ namespace   │ version │ mode    │ pid      │ uptime │ ↺    │ status    │ cpu      │ mem      │ user     │ watching │
├─────┼──────────────────┼─────────────┼─────────┼─────────┼──────────┼────────┼──────┼───────────┼──────────┼──────────┼──────────┼──────────┤
│ 0   │ ClusterEn8082    │ default     │ 1.0.0   │ cluster │ 17066    │ 48s    │ 1    │ online    │ 0%       │ 70.0mb   │ JoseLuis │ enabled  │
│ 1   │ ClusterEn8082    │ default     │ 1.0.0   │ cluster │ 17072    │ 48s    │ 1    │ online    │ 0%       │ 70.2mb   │ JoseLuis │ enabled  │
│ 2   │ ClusterEn8083    │ default     │ 1.0.0   │ cluster │ 17084    │ 48s    │ 1    │ online    │ 0%       │ 69.5mb   │ JoseLuis │ enabled  │
│ 3   │ ClusterEn8083    │ default     │ 1.0.0   │ cluster │ 17078    │ 48s    │ 1    │ online    │ 0%       │ 69.6mb   │ JoseLuis │ enabled  │
│ 4   │ ClusterEn8084    │ default     │ 1.0.0   │ cluster │ 17259    │ 37s    │ 0    │ online    │ 0%       │ 70.6mb   │ JoseLuis │ enabled  │
│ 5   │ ClusterEn8084    │ default     │ 1.0.0   │ cluster │ 17266    │ 37s    │ 0    │ online    │ 0%       │ 70.7mb   │ JoseLuis │ enabled  │
│ 6   │ ClusterEn8085    │ default     │ 1.0.0   │ cluster │ 17368    │ 30s    │ 0    │ online    │ 0%       │ 70.5mb   │ JoseLuis │ enabled  │
│ 7   │ ClusterEn8085    │ default     │ 1.0.0   │ cluster │ 17375    │ 30s    │ 0    │ online    │ 0%       │ 71.1mb   │ JoseLuis │ enabled  │
└─────┴──────────────────┴─────────────┴─────────┴─────────┴──────────┴────────┴──────┴───────────┴──────────┴──────────┴──────────┴──────────┘

```
Now we just have to edit our nginx configuration file to redirect when going to /test/random to go to -> /test/randoms of the previously created servers.

We move where we have the configuration file and edit it:

```console

┬─[joseluis@joseluisabs:/etc/nginx]
╰─>$ sudo nvim nginx.conf
```


```console

events {
}

http {

    upstream backend {
        server 127.0.0.1:8082;
        server 127.0.0.1:8083;
        server 127.0.0.1:8084;
        server 127.0.0.1:8085;
    }
    server {
        listen 8080;
        location /test/random/ {
            proxy_pass http://backend/test/randoms/;
        }
    }

}

```



We check that the syntax is correct:

```console

─[joseluis@joseluisabs:/etc/nginx]
╰─>$ sudo nginx -t
nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
nginx: configuration file /etc/nginx/nginx.conf test is successful

```

We stop and turn the service back on

```console

┬─[joseluis@joseluisabs:/etc/nginx]
╰─>$ sudo service nginx stop
┬─[joseluis@joseluisabs:/etc/nginx]
╰─>$ sudo service nginx start

```

And that's it, we can access through http://localhost:8080/test/random/

We add a log when the list is generated and we can check it through **pm2 monit**

```console

┬─[joseluis@joseluisabs:/etc/nginx]
╰─>$ pm2 monit


┌─ Process List ───────────────────────┐┌──  ClusterEn8084 Logs  ────────────────────────────────────────────────────────────────────┐
│[ 0] ClusterEn8082     Mem:  69 MB    ││ ClusterEn8084 > Generated list                                                             │
│[ 1] ClusterEn8082     Mem:  71 MB    ││                                                                                            │
│[ 2] ClusterEn8083     Mem:  69 MB    ││                                                                                            │
│[ 3] ClusterEn8083     Mem:  70 MB    ││                                                                                            │
│[ 4] ClusterEn8084     Mem:  71 MB    ││                                                                                            │
│[ 5] ClusterEn8084     Mem:  70 MB    ││                                                                                            │
│[ 6] ClusterEn8085     Mem:  69 MB    ││                                                                                            │
│[ 7] ClusterEn8085     Mem:  72 MB    ││                                                                                            │
│                                      ││                                                                                            │
                                            [...]

```

