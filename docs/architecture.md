# Архитектура

1. **Лексер** (`src/lexer.c`) → токены  
2. **Pratt-парсер** (`src/parser.c`) → AST  
3. **Дешугаринг** (`src/desugar.c`): списки, placeholder, let  
4. **Eval** (`src/eval.c`): Krivine-машина, thunks, memoization  
5. **Runtime** (`src/runtime.c`): примитивы IO, file-IO  
6. **REPL** (`src/repl.c`) & **batch** (`src/interpretator.c`)  

### Память

- **Bump-arena allocator**: единственный `malloc` и простой указатель.  
- Без сложного GC.

### Name table

- Блоки лексических контекстов, поддержка вложенных `let` и `let rec`.
