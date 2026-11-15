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
