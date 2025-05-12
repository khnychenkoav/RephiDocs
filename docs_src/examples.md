---
title: Примеры
---

# Примеры использования

## Факториал + вывод
```re
let rec fact n = if n == 0 then 1 else n * fact (n-1)
5 |> fact |> println
````

## Map и Filter

```re
[1..10) |> map (_ * 3) |> filter (> 15) |> println
```

## File I/O

```re
writeFile 1 456
readFile 1 |> println
```

[prev: Стандартная библиотека](stdlib.md) 
