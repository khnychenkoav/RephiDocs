---
title: Установка
---

# Установка

## Зависимости

- GCC (поддержка C17)
- make

## Сборка и запуск

```bash
git clone https://github.com/ваш-аккаунт/rephi.git
cd rephi
make
````

В итоге в корне появится бинарник `rephi`.

## Установка стандартной библиотеки

```bash
make install-stdlib DESTDIR=/usr/local
```

По умолчанию копирует `.re` файлы в

```
/usr/local/share/rephi/stdlib
```

[next: Быстрый старт](quickstart.md)
