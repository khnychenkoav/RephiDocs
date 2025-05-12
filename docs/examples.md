# Примеры

## Факториал

```re
let rec fact n =
    if n == 0 then 1 else n * fact (n-1)

5 |> fact |> println
```

## Map+Filter

```re
[1..10) |> map (_ * 3) |> filter (> 15) |> println
```

## File I/O

```re
writeFile 1 123
readFile 1 |> println
```

