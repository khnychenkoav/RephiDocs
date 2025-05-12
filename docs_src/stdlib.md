

# Стандартная библиотека Rephi

При инициализации REPL или batch-интерпретатора автоматически вызывается функция `load_stdlib`, которая последовательно загружает модули из папки `rephi_stdlib/`:

1. **prelude.re** — основные функции над парами и списками
2. **io.re**     — обёртки для `print` и `readln`
3. **file\_io.re**— чтение и запись файлов

Модули подключаются в следующем порядке:

```c
void load_stdlib(name_table *nt) {
    static const char *modules[] = {
        "rephi_stdlib/prelude.re",
        "rephi_stdlib/io.re",
        "rephi_stdlib/file_io.re",
        NULL
    };
    // для каждого модуля: читать файл, построчно парсить, eval, добавлять в name_table
}
```

---

## 1. prelude.re

Модуль `prelude.re` определяет основные структуры данных: пары и списки, а также шаблонную реализацию функций высшего порядка.

```re
# prelude.re

let pair = \a -> \b -> \f -> f a b in pair
let fst  = \p -> p (\a b -> a) in fst
let snd  = \p -> p (\a b -> b) in snd

let cons = \h -> \t -> \c -> \n -> c h (t c n) in cons
let nil  = \c -> \n -> n in nil

let head = \xs -> xs (\h _ -> h) nil in head
let tail = \xs -> fst (xs (\h p -> pair (snd p) (cons h (snd p))) (pair nil nil)) in tail
let pop  = \l -> tail (tail l) in pop

let isnil = \xs -> xs (\h _ -> 0) 1 in isnil

let Y    = \f -> (\x -> f (\v -> x x v)) (\x -> f (\v -> x x v)) in Y

# Многопараметричные функции через Y-комбинатор
let rec map = \f -> \xs -> if isnil xs then nil else cons (f (head xs)) (map f (tail xs)) in map
```

* **pair**: упаковка двух значений, принимает `a`, `b`, затем функцию `f`, применяет её к `a b`.
* **fst**, **snd**: получение первого и второго элемента пары.
* **cons**, **nil**: построение и пустой список (Church-encoded список).
* **head**, **tail**, **pop**: получение первого элемента, разворот списка (через `|>`) и извлечение первого элемента (возвращает список без первого элемента).
* **isnil**: проверка на пустой список (возвращает `1` для пустого, `0` — иначе).
* **Y**‑комбинатор: реализация рекурсии поверх чистых лямбд.
* **map**: рекурсивная функция для применения `f` ко всем элементам списка.

### Пример использования prelude.re в REPL

```repl
rephi> [1,2,3,4] |> map (\x -> x * 2) |> head
2

rephi> head ([10,20,30])
10

rephi> [1,2,3]|>tail|>head
3

rephi> pop [1,2,3] |> head
2

rephi> isnil []
1

rephi> isnil [0]
0
```

---

## 2. io.re

Модуль `io.re` предоставляет удобный синтаксис для печати и чтения строк.

```re
# io.re
let println = \x -> print x in println
let readln = readLine in readln
```

* **println**: принимает значение `Int` или результат любых функций, вызывает `print` (C-реализация из `runtime.c`) и возвращает аргумент.
* **readln**: обёртка над `readLine` (C-реализация возвращает длину считанной строки).

### Примеры

```repl
rephi> println 42
42

rephi> readln 0 #обязательно требует нуль-заглушку (в качестве заглушки может выступать любое число)
#ввод пользователя
1233
4
```

---

## 3. file\_io.re

Модуль `file_io.re` позволяет читать и записывать файлы по "именам" в виде числовых дескрипторов.

```re
# file_io.re
let readfl = readFile in readfl
let writefl = writeFile in writefl
```

* **readfl**: обёртка над `readFile` из `runtime.c`, принимает `Int` (имя файла), возвращает длину в байтах.
* **writefl**: обёртка над `writeFile`, двухфазная функция: сначала принимает `Int` (имя файла), затем — `Int` (содержимое), возвращает статус (1 — успех).

### Пример чтения/записи

```bash
# из REPL
rephi> writefl 100 12345
1
rephi> readfl 100
5

# проверка контента
$ cat 100
12345
```

---

