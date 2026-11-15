# Canary

Planner:

```sh
goose run --no-session --quiet --provider 402router --model k3.1-pro -t 'Reply exactly PLANNER_OK'
```

Worker:

```sh
goose run --no-session --quiet --provider allmodels_fast --model deepseek/deepseek-v4.1-flash-abliterated -t 'Reply exactly WORKER_OK'
```
