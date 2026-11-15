# Measured results

Same fresh Python task, max reasoning, three failing tests. All runs passed 3/3.

| Config | Model | Input | Output | Wall time |
|---|---|---:|---:|---:|
| Before | DeepSeek | 65,962 | 650 | not recorded |
| NuriRouter disabled | DeepSeek | 60,571 | 672 | 9.27s |
| NuriRouter disabled | Kimi K3.1 Pro | 57,839 | 622 | 35.27s |

Removing NuriRouter cut DeepSeek input 8.2% with equal test quality. Caveman generic proxy: 0% reduction; not used.
