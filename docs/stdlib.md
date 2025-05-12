# Стандартная библиотека

Загружается автоматически в REPL и batch.

- **prelude.re**: `pair`, `fst`, `snd`, `cons`, `nil`, `map`, `filter`, `Y`-комбинатор.  
- **io.re**: `println`, `readln`.  
- **file_io.re**: `readFile`, `writeFile`.

```re
let println = \x -> print x in println
let readln = readLine in readln
```
