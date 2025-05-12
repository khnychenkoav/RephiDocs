---
title: Быстрый старт
---

# Быстрый старт

## Интерактивный REPL

```bash
./rephi
rephi> 2 + 2
4
rephi> let rec fact n = if n == 0 then 1 else n * fact (n - 1) in fact 6
720
````

## Создание скрипта

Создайте файл `fib.re`:

```re
let rec fib n =
  if n == 0 then 0
  else if n == 1 then 1
  else fib (n-1) + fib (n-2)

# Выводим первые 10 чисел Фибоначчи
[0..10) |> map fib |> println
```

Запустите:

```bash
./rephi fib.re
```

[prev: Установка](installation.md) • [next: Синтаксис](syntax.md)
