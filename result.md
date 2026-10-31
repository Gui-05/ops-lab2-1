root@1-0001:~/lab2# scripts/table.sh runs/t1-light ok_rps mean_ms p99_ms server_rps server_mean_ms server_p99_ms cpu_ms_per_req db_query_mean_ms

| step | target_rps | ok_rps | mean_ms | p99_ms | server_rps | server_mean_ms | server_p99_ms | cpu_ms_per_req | db_query_mean_ms |
|---|---|---|---|---|---|---|---|---|---|
| 1 | 0 | 0.0 | - | - | 0 | NaN | NaN | +Inf | NaN |
| 2 | 50 | 50.5 | 11.43 | 12.78 | 51.7083 | 10.7199 | 19.9 | 0.537482 | 10.3136 |
| 3 | 100 | 97.8 | 11.59 | 13.92 | 95.5 | 10.8713 | 19.9 | 0.536459 | 10.4288 |
| all | - | 74.2 | 11.54 | 13.24 | - | - | - | - | - |