# Быстрый старт

## REPL

```bash
./rephi
rephi> 1 + 2 * 3
7
rephi> let rec fact n = if n == 0 then 1 else n * fact (n - 1) in fact 5
120
```

## Скрипт

```re
# fib.re
let rec fib n =
    if n == 0 then 0
    else if n == 1 then 1
    else fib (n-1) + fib (n-2)

# печать 10 первых фибоначчи
lazylet n = 0 + 1
force fib
```

Запустить:

```bash
./rephi fib.re
```


---
