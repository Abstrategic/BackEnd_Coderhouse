# Challenge 16

## Loggers, Gzip and performance analysis.

### Intructions

Incorporate gzip compression into the work server project.

Check the /info route with and without compression, the difference in the number of bytes returned in one case and another.

Then implement logging (with some class view library) that records the following:

    - Route and method of all requests received by the server (info)
    - Route and method of requests to routes that do not exist on the server (warning)

Errors thrown by the message and product apis, only (error)
Consider the following criteria:
   - Log all levels to console (info, warning and error)
   - Log only warning logs to a file called warn.log
   - Send only the error logs to a file called error.log

----

Then, carry out the complete performance analysis of the server with which we have been working.

We are going to work on the '/info' route, in fork mode, adding or extracting a console.log of the collected information before returning it to the client. We will also disable the child_process of the route '/randoms'

For both conditions (with or without console.log) in path '/info' GET:

   - The profiling of the server, carrying out the test with --prof of node.js. Parse the results obtained after processing them with --prof-process.
   - We will use Artillery as a load test in the command line, emulating 50 concurrent connections with 20 requests for each one. Extract a report with        the results in a text file.

----

Then we will use Autocannon on the command line, emulating 100 concurrent connections made in a time of 20 seconds. Extract a report with the results (it can be a print screen of the console)

   - Profiling the server with node.js inspector mode --inspect. Review the time of the less performing processes on the inspection source file.
   - The flame diagram with 0x, emulating the charge with Autocannon with the same previous parameters.
  
Prepare a report in pdf format on the tests carried out, including the results of all the tests (text and images).

👉 At the end include the conclusion obtained from the analysis of the data.

### Conclusion

Without console log

```console

╰─>$ node benchmark.js
Running tests
Running 20s test @ http://localhost:3030/test/info
100 connections


┌─────────┬────────┬────────┬────────┬────────┬───────────┬──────────┬────────┐
│ Stat    │ 2.5%   │ 50%    │ 97.5%  │ 99%    │ Avg       │ Stdev    │ Max    │
├─────────┼────────┼────────┼────────┼────────┼───────────┼──────────┼────────┤
│ Latency │ 131 ms │ 160 ms │ 293 ms │ 424 ms │ 173.93 ms │ 51.78 ms │ 665 ms │
└─────────┴────────┴────────┴────────┴────────┴───────────┴──────────┴────────┘
┌───────────┬────────┬────────┬────────┬────────┬──────────┬─────────┬────────┐
│ Stat      │ 1%     │ 2.5%   │ 50%    │ 97.5%  │ Avg      │ Stdev   │ Min    │
├───────────┼────────┼────────┼────────┼────────┼──────────┼─────────┼────────┤
│ Req/Sec   │ 257    │ 257    │ 600    │ 700    │ 572.15👈 │ 113.28  │ 257    │
├───────────┼────────┼────────┼────────┼────────┼──────────┼─────────┼────────┤
│ Bytes/Sec │ 154 kB │ 154 kB │ 361 kB │ 421 kB │ 344 kB   │ 68.2 kB │ 154 kB │
└───────────┴────────┴────────┴────────┴────────┴──────────┴─────────┴────────┘

Req/Bytes counts sampled once per second.
# of samples: 20

12k requests in 20.07s, 6.88 MB read

```

The Artillery result shows (see file for full results)

```console

http.response_time:
  min: ......................................................................... 4 👈
  max: ......................................................................... 393 👈
  median: ...................................................................... 141.2 👈 
  p95: ......................................................................... 210.6 👈
  p99: ......................................................................... 308 👈

```

Benchmark with console Log

```console

╰─>$ node benchmark.js
Running tests (CON CONSOLE LOG)
Running 20s test @ http://localhost:3030/test/info
100 connections


┌─────────┬────────┬────────┬────────┬────────┬───────────┬──────────┬────────┐
│ Stat    │ 2.5%   │ 50%    │ 97.5%  │ 99%    │ Avg       │ Stdev    │ Max    │
├─────────┼────────┼────────┼────────┼────────┼───────────┼──────────┼────────┤
│ Latency │ 173 ms │ 220 ms │ 446 ms │ 562 ms │ 238.81 ms │ 70.81 ms │ 830 ms │
└─────────┴────────┴────────┴────────┴────────┴───────────┴──────────┴────────┘
┌───────────┬────────┬────────┬────────┬────────┬──────────┬─────────┬────────┐
│ Stat      │ 1%     │ 2.5%   │ 50%    │ 97.5%  │ Avg      │ Stdev   │ Min    │
├───────────┼────────┼────────┼────────┼────────┼──────────┼─────────┼────────┤
│ Req/Sec   │ 218    │ 218    │ 427    │ 540    │ 415.35👈 │ 81.88   │ 218    │
├───────────┼────────┼────────┼────────┼────────┼──────────┼─────────┼────────┤
│ Bytes/Sec │ 131 kB │ 131 kB │ 257 kB │ 325 kB │ 250 kB   │ 49.3 kB │ 131 kB │
└───────────┴────────┴────────┴────────┴────────┴──────────┴─────────┴────────┘

Req/Bytes counts sampled once per second.
# of samples: 20

8k requests in 20.07s, 5 MB read

```

The Artillery result shows (see file for full results)

```console

http.response_time:
  min: ......................................................................... 15  👈
  max: ......................................................................... 461 👈
  median: ...................................................................... 172.5 👈
  p95: ......................................................................... 228.2 👈 
  p99: ......................................................................... 376.2 👈
  
```
👈All the tests carried out indicate that in the case that we log in through the console, the response time before being sent is longer and that fewer requests can be handled at the same time.



