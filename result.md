# task1

root@1-0001:~/lab2# scripts/table.sh runs/t1-light ok_rps mean_ms p99_ms server_rps server_mean_ms server_p99_ms cpu_ms_per_req db_query_mean_ms

| step | target_rps | ok_rps | mean_ms | p99_ms | server_rps | server_mean_ms | server_p99_ms | cpu_ms_per_req | db_query_mean_ms |
|---|---|---|---|---|---|---|---|---|---|
| 1 | 0 | 0.0 | - | - | 0 | NaN | NaN | +Inf | NaN |
| 2 | 50 | 50.5 | 11.43 | 12.78 | 51.7083 | 10.7199 | 19.9 | 0.537482 | 10.3136 |
| 3 | 100 | 97.8 | 11.59 | 13.92 | 95.5 | 10.8713 | 19.9 | 0.536459 | 10.4288 |
| all | - | 74.2 | 11.54 | 13.24 | - | - | - | - | - |

# task 2

## R1

root@1-0001:~/lab2# scripts/rates.sh 388
78,155,233,272,310,349,388,427,466

root@1-0001:~/lab2# scripts/run.sh r1-pool4 -url http://127.0.0.1:8080/api/courses/1 -rates "$RATES"
== loadgen（结果写进 runs/r1-pool4/）
loadgen：GET http://127.0.0.1:8080/api/courses/1，9 个阶段 × 30s，到达过程 poisson，超时 2s，GOMAXPROCS=1
阶段 1/9：目标 78 请求/秒，已发出 2412，已成功 2410，在途 2，压测机 CPU 1%
阶段 2/9：目标 155 请求/秒，已发出 4609，已成功 4609，在途 0，压测机 CPU 3%
阶段 3/9：目标 233 请求/秒，已发出 6983，已成功 6981，在途 2，压测机 CPU 4%
阶段 4/9：目标 272 请求/秒，已发出 8289，已成功 8288，在途 1，压测机 CPU 4%
阶段 5/9：目标 310 请求/秒，已发出 9409，已成功 9407，在途 2，压测机 CPU 5%
阶段 6/9：目标 349 请求/秒，已发出 10369，已成功 10360，在途 9，压测机 CPU 5%
阶段 7/9：目标 388 请求/秒，已发出 11737，已成功 11179，在途 386，压测机 CPU 6%
阶段 8/9：目标 427 请求/秒，已发出 12702，已成功 10864，在途 435，压测机 CPU 6%
阶段 9/9：目标 466 请求/秒，已发出 13965，已成功 10857，在途 439，压测机 CPU 7%
等待在途的 439 个请求结束（最多 2s）…
step  target_rps   sent     ok  error_rate  mean_ms   p50_ms   p99_ms   max_ms  slo_good  lag_p99_ms  gen_cpu_pct  
   1          78   2412   2412      0.0000    11.56    11.48    13.56    19.55    1.0000        1.06            1  
   2         155   4609   4609      0.0000    11.93    11.67    17.85    24.82    1.0000        1.06            3  
   3         233   6983   6983      0.0000    12.68    11.83    22.76    34.62    1.0000        1.06            4  
   4         272   8289   8289      0.0000    14.51    12.22    33.68    52.44    0.9994        1.07            4  
   5         310   9409   9409      0.0000    16.97    14.11    50.07    68.42    0.9899        1.07            5  
   6         349  10369  10369      0.0000    23.00    19.16    64.47    79.43    0.9617        1.07            5  
   7         388  11737  11539      0.0169   617.82   710.35  1010.25  1014.25    0.0631        1.08            6  
   8         427  12702  11244      0.1148   999.24  1001.97  1012.00  1017.90    0.0000        1.10            6  
   9         466  13965  11245      0.1948  1003.66  1005.12  1012.27  1016.91    0.0000        1.10            7  
 all              80475  76099      0.0544   398.70    26.86  1011.47  1017.90    0.5258        1.08            5  
== 按阶段查询 Prometheus
-- red.csv
step  target_rps  server_rps  server_error_rate  server_p99_ms  server_mean_ms  inflight_avg  cpu_cores  cpu_ms_per_req  cpu_wait_threads  sched_wait_p99_ms  pool_in_use_avg  pool_wait_p99_ms  db_query_mean_ms  fsync_per_s  fsync_mean_ms  fsync_p99_ms  batch_mean  goroutines_max  server_slo_good
1     78          81.25       0                  19.9           10.8161         0.92          0.0438072  0.539166        0.0392011         0.492566           0.92             1.25              10.3885           0            NaN            NaN           NaN         17              1
2     155         155.167     0                  19.9293        11.1989         1.72          0.0836039  0.5388          0.0732543         0.488635           1.68             7.79375           10.5167           0            NaN            NaN           NaN         21              1
3     233         233.417     0                  34.1453        12.0162         3.04          0.124489   0.533335        0.104915          0.491508           2.6              14.3136           10.5394           0            NaN            NaN           NaN         25              1
4     272         279.75      0                  47.4193        13.9752         4.24          0.14766    0.527828        0.129603          0.493901           3.36             29.858            10.5382           0            NaN            NaN           NaN         34              0.999404
5     310         315.125     0                  56.0291        16.6538         5.92          0.164921   0.523351        0.143918          0.498517           3.64             45.887            10.5363           0            NaN            NaN           NaN         49              0.988629
6     349         346.25      0                  88.6785        22.7491         7.92          0.178093   0.514347        0.154239          0.495758           3.48             71.5411           10.5527           0            NaN            NaN           NaN         55              0.955836
7     388         379.315     0.0166487          1898.91        683.073         266.44        0.193528   0.510203        0.176488          0.499186           4                1390              10.6184           0            NaN            NaN           NaN         836             0
8     427         420.5       0.110583           1983.27        998.545         418.12        0.206364   0.490758        0.188403          0.497779           4                1915.12           10.5905           0            NaN            NaN           NaN         940             0
9     466         469.042     0.201475           1987.35        1002.68         471.04        0.232036   0.494703        0.215358          0.708652           4                1952.8            10.571            0            NaN            NaN           NaN         1059            0
-- use.csv
step  target_rps  svc_cpu_busy  all_cpu_busy  cpu_steal  cpu_iowait  procs_running_avg  cpu_psi_some  mem_available_min_mb  swap_in_per_s  disk_w_per_s  disk_wkb_per_s  disk_w_await_ms  disk_f_per_s  disk_f_await_ms  disk_aqu_sz  disk_util
1     78          0.0615        0.0505        0          0.00025     1.6                0.043549      2157.08               0              2.95          27.2            0.898305         0.4           0.125            0.0027       0.00095
2     155         0.103         0.08          0          0.0005      1.4                0.0710931     2146.5                0              2.75          22.4            0.545455         0.4           0.125            0.00155      0.0003
3     233         0.13          0.09475       0          0           1.4                0.0997633     2144.87               0              2.75          25.6            0.563636         0.4           0.125            0.00155      0.00025
4     272         0.1675        0.12025       0          0.00025     2.2                0.120977      2150.95               0              3.25          28.4            0.553846         0.4           0                0.0018       0.00035
5     310         0.1765        0.122         0          0           2.4                0.126969      2156.9                0              2.8           26              0.553571         0.4           0                0.00155      0.0004
6     349         0.182         0.12475       0          0.00025     2.8                0.137739      2155.97               0              2.75          22.4            0.745455         0.4           0                0.002        0.0006
7     388         0.2035        0.14          0          0           2.4                0.154418      2122.69               0              2.85          23.6            0.596491         0.4           0                0.0017       0.00045
8     427         0.215         0.1465        0          0.00025     3                  0.170513      2113.8                0              1.75          20              0.571429         0.4           0                0.001        0.0003
9     466         0.2535        0.17          0          0           1.8                0.190346      2076.53               0              5.55          38.8            0.702703         0.5           0.1              0.00395      0.00075
完成：runs/r1-pool4
root@1-0001:~/lab2# scripts/table.sh runs/r1-pool4 ok_rps error_rate p99_ms server_p99_ms server_mean_ms inflight_avg cpu_ms_per_req pool_in_use_avg pool_wait_p99_ms sched_wait_p99_ms svc_cpu_busy procs_running_avg
| step | target_rps | ok_rps | error_rate | p99_ms | server_p99_ms | server_mean_ms | inflight_avg | cpu_ms_per_req | pool_in_use_avg | pool_wait_p99_ms | sched_wait_p99_ms | svc_cpu_busy | procs_running_avg |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 1 | 78 | 80.4 | 0.0000 | 13.56 | 19.9 | 10.8161 | 0.92 | 0.539166 | 0.92 | 1.25 | 0.492566 | 0.0615 | 1.6 |
| 2 | 155 | 153.6 | 0.0000 | 17.85 | 19.9293 | 11.1989 | 1.72 | 0.5388 | 1.68 | 7.79375 | 0.488635 | 0.103 | 1.4 |
| 3 | 233 | 232.8 | 0.0000 | 22.76 | 34.1453 | 12.0162 | 3.04 | 0.533335 | 2.6 | 14.3136 | 0.491508 | 0.13 | 1.4 |
| 4 | 272 | 276.3 | 0.0000 | 33.68 | 47.4193 | 13.9752 | 4.24 | 0.527828 | 3.36 | 29.858 | 0.493901 | 0.1675 | 2.2 |
| 5 | 310 | 313.6 | 0.0000 | 50.07 | 56.0291 | 16.6538 | 5.92 | 0.523351 | 3.64 | 45.887 | 0.498517 | 0.1765 | 2.4 |
| 6 | 349 | 345.6 | 0.0000 | 64.47 | 88.6785 | 22.7491 | 7.92 | 0.514347 | 3.48 | 71.5411 | 0.495758 | 0.182 | 2.8 |
| 7 | 388 | 384.6 | 0.0169 | 1010.25 | 1898.91 | 683.073 | 266.44 | 0.510203 | 4 | 1390 | 0.499186 | 0.2035 | 2.4 |
| 8 | 427 | 374.8 | 0.1148 | 1012.00 | 1983.27 | 998.545 | 418.12 | 0.490758 | 4 | 1915.12 | 0.497779 | 0.215 | 3 |
| 9 | 466 | 374.8 | 0.1948 | 1012.27 | 1987.35 | 1002.68 | 471.04 | 0.494703 | 4 | 1952.8 | 0.708652 | 0.2535 | 1.8 |
| all | - | 281.8 | 0.0544 | 1011.47 | - | - | - | - | - | - | - | - | - |

root@1-0001:~/lab2# taskset -c "$GEN_CPUS" bin/loadgen -url http://127.0.0.1:8080/api/courses/1 \
  -rates "$(scripts/rates.sh 388 0.8)" -step 40s > /dev/null 2>&1 &
LG=$!                                  # 后台 loadgen 的进程号
sleep 10
go tool pprof -top -nodecount=15 'http://127.0.0.1:8080/debug/pprof/profile?seconds=20' | tee runs/r1-pool4/pprof-top.txt
wait "$LG"         
[1] 771965
Fetching profile over HTTP from http://127.0.0.1:8080/debug/pprof/profile?seconds=20
Saved profile in /root/pprof/pprof.enrolld.samples.cpu.001.pb.gz
File: enrolld
Build ID: 1a2e75ec36cd73b60c8824be418195bc64bb8eaf
Type: cpu
Time: 2026-10-31 16:10:29 CST
Duration: 20s, Total samples = 2.90s (14.50%)
Showing nodes accounting for 2.68s, 92.41% of 2.90s total
Dropped 66 nodes (cum <= 0.01s)
Showing top 15 nodes out of 55
      flat  flat%   sum%        cum   cum%
     2.38s 82.07% 82.07%      2.38s 82.07%  main.spin (inline)
     0.18s  6.21% 88.28%      0.18s  6.21%  internal/runtime/syscall/linux.Syscall6
     0.03s  1.03% 89.31%      0.03s  1.03%  runtime.futex
     0.02s  0.69% 90.00%      0.02s  0.69%  net/http.(*chunkWriter).writeHeader
     0.01s  0.34% 90.34%      0.02s  0.69%  encoding/json.structEncoder.encode
     0.01s  0.34% 90.69%      0.04s  1.38%  net/http.(*conn).readRequest
     0.01s  0.34% 91.03%      2.80s 96.55%  net/http.(*conn).serve
     0.01s  0.34% 91.38%      0.02s  0.69%  runtime.execute
     0.01s  0.34% 91.72%      0.06s  2.07%  runtime.findRunnable
     0.01s  0.34% 92.07%      0.03s  1.03%  runtime.netpoll
     0.01s  0.34% 92.41%      0.17s  5.86%  syscall.RawSyscall6
         0     0% 92.41%      0.06s  2.07%  bufio.(*Reader).Peek
         0     0% 92.41%      0.06s  2.07%  bufio.(*Reader).fill
         0     0% 92.41%      0.17s  5.86%  bufio.(*Writer).Flush
         0     0% 92.41%      0.03s  1.03%  encoding/json.(*Encoder).Encode
[1]+  Done                    taskset -c "$GEN_CPUS" bin/loadgen -url http://127.0.0.1:8080/api/courses/1 -rates "$(scripts/rates.sh 388 0.8)" -step 40s > /dev/null 2>&1