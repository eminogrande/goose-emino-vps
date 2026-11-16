# Measured results

Same fresh Python task, max reasoning, three failing tests. All runs passed 3/3.

| Config | Model | Input | Output | Wall time |
|---|---|---:|---:|---:|
| Before | DeepSeek | 65,962 | 650 | not recorded |
| NuriRouter disabled | DeepSeek | 60,571 | 672 | 9.27s |
| NuriRouter disabled | Kimi K3.1 Pro | 57,839 | 622 | 35.27s |

Removing NuriRouter cut DeepSeek input 8.2% with equal test quality. Caveman generic proxy: 0% reduction; not used.

## Complex repo + full Caveman recovery

Real itsdangerous repo; injected digest bug; 297 tests; DeepSeek Max. Both fixed source and passed 297/297.

| Setup | Input | Output | Wall time | Caveman reduction |
|---|---:|---:|---:|---:|
| Plain minimal Goose | 117,017 | 1,292 | 16.86s | — |
| Full Caveman proxy + recovery MCP | 120,954 | 1,395 | 18.61s | 0% |

Full Caveman was slower and used more tokens on this task. Temporary integration removed; minimal config restored.

## Flask multi-file regression

Real Flask repo; JSON and session regressions across two files; DeepSeek Max. Both passed 494/494.

| Setup | Input | Output | Wall time | Caveman reduction |
|---|---:|---:|---:|---:|
| Plain minimal Goose | 109,362 | 1,897 | 22.95s | — |
| Full Caveman proxy + recovery MCP | 175,224 | 2,765 | 37.00s | 0% |

Plain Goose used 37.6% fewer input tokens and was 38.0% faster. Temporary integration removed; minimal config restored.

## Minimal system-prompt experiment

Same Flask multi-file regression and DeepSeek Max. Both restored source exactly to upstream and passed 494/494. Kimi review therefore had no source diff to reject.

| Prompt | Input | Output | Wall time |
|---|---:|---:|---:|
| Default | 109,362 | 1,897 | 22.95s |
| Minimal custom | 131,994 | 1,216 | 30.50s |

Minimal prompt lost: 20.7% more input and 32.9% slower. Default prompt restored.

## Prompt-rule A/B: three repeated runs

Same Flask task, DeepSeek Max. Every run passed 494/494. Exact upstream restore also checked because tests missed two seeded regressions.

| Rules | Avg input | Avg output | Avg time | Full fixes |
|---|---:|---:|---:|---:|
| ADHD only | 98,865 | 1,367 | 25.0s | 1/3 |
| Caveman + ADHD | 113,503 | 1,501 | 28.9s | 2/3 |

Core and Caveman-only single runs also passed and fully restored, but were slower (30.36s and 29.23s). Caveman + ADHD kept for better full-fix rate; ADHD-only was cheaper but less reliable. Results are task-specific, not universal proof.

## Pi comparison and durable status

Same Flask regressions, DeepSeek Max, Caveman+ADHD. Pi fully restored source and passed 494/494: 6,688 input, 935 output, 27.54s. Goose Caveman+ADHD three-run average: 113,503 input, 1,501 output, 28.9s, 2/3 full fixes. Pi won input tokens decisively on this run.

Pi-durable 1.5.2 crash harness attempted with SQLite and forced process exit. Recovery did not complete: custom model wiring returned `Unknown provider: undefined`. Durable recovery is not verified; article durability claims remain author-reported.

## Multi-repo Goose vs Pi

Same DeepSeek Max and Caveman+ADHD. Clean isolated Pi config. All runs restored source exactly and passed full checks.

| Task | Harness | Input | Output | Time |
|---|---|---:|---:|---:|
| Jinja, 911 tests | Goose | 112,047 | 1,742 | 29.51s |
| Jinja, 911 tests | Pi | 7,354 | 1,081 | 33.67s |
| path-to-regexp, npm test/lint/build/size | Goose | 343,431 | 2,190 | 64.48s |
| path-to-regexp, npm test/lint/build/size | Pi | 16,003 | 537 | 31.75s |

Pi used 93.4% fewer input tokens on Jinja and 95.3% fewer on JavaScript. Goose was 12.4% faster on Jinja; Pi was 50.8% faster on JavaScript. Results are single runs per task.

Pi-durable recovery remains unverified after stopping a configuration debug spiral (`Provider is not configured: allmodels`). No durability claim is made.

## Pi-durable recovery passed

Pi-durable 1.5.2 + SQLite + DeepSeek Max. First process forcibly exited with code 42 during the model request. A new process reopened the same SQLite storage and completed requestId `crash-canary-1` with status `done`. Transcript contained exactly `DURABLE_RECOVERED` at max reasoning. Earlier setup errors were fixed; recovery is now verified locally.

## Local durable coding agent

Minimal Pi-durable CLI prototype used SQLite, CodingTools, NodeExecutionEnv and DeepSeek Max. Canary returned `LOCAL_DURABLE_OK`. On Flask regressions it restored all source exactly and passed 494/494 in 103.63s. This proves local coding and recovery; it is not yet the fast production configuration.

## Clean Pi vs user's full Pi

Same installed Pi 1.5.0 binary, Flask task, DeepSeek Max. Full Pi used existing extensions, skills, MCP and context customizations.

| Pi config | Input | Output | Time | Quality |
|---|---:|---:|---:|---|
| Clean | 6,688 | 935 | 27.54s | Exact restore; 494/494 |
| Full user config | 21,826 | 1,553 | 38.84s | 494/494 but missed two regressions and changed an unrelated property |

Clean config won this run. Full config was restored after the benchmark.
