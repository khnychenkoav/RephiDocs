---
title: Стандартная библиотека
---

# Стандартная библиотека

Страница загружается автоматически в REPL и batch-интерпретаторе.

- **prelude.re**:
  - `pair`, `fst`, `snd`, `cons`, `nil`
  - `map`, `filter`, `Y`‑комбинатор
- **io.re**:
  - `println`, `readln`
- **file_io.re**:
  - `readFile`, `writeFile`

Примеры:
```re
let println = \x -> print x in println
let readln = readLine in readln
````

[prev: Архитектура](architecture.md) • [next: Примеры](examples.md)
