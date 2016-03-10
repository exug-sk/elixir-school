---
layout: page
title: Enum
category: basics
order: 3
lang: ru 
---

Набор алгоритмов для операций с коллекциями.

## Содержание

- [Enum](#enum)
  - [all?](#all)
  - [any?](#any)
  - [chunk](#chunk)
  - [chunk_by](#chunk_by)
  - [each](#each)
  - [map](#map)
  - [min](#min)
  - [max](#max)
  - [reduce](#reduce)
  - [sort](#sort)
  - [uniq](#uniq)

## Enum

Модуль `Enum` включает в себя больше ста функций для работы с коллекциями, которые описаны в предыдущем уроке.

Этот урок содержит только небольшую часть функций. Для того, чтобы увидеть полный список функций - посетите официальную документацию по [`Enum`](http://elixir-lang.org/docs/v1.0/elixir/Enum.html) . Для документации по "ленивым" операциям есть отдельная документация в модуле [`Stream`](http://elixir-lang.org/docs/v1.0/elixir/Stream.html).

### all?

При использовании `all?`, как и большей части `Enum` в целом, мы передаем функцию, которая будет применяться к элементам коллекции. В случае с `all?` если хоть один элемент коллекции не вернет `true` в качестве результата, то результатом будет `false`:

```elixir
iex> Enum.all?(["foo", "bar", "hello"], fn(s) -> String.length(s) == 3 end)
false
iex> Enum.all?(["foo", "bar", "hello"], fn(s) -> String.length(s) > 1 end)
true
```

### any?

И наоборот, `any?` вернет `true` если хотя бы один элемент в коллекции выполнится в `true`:

```elixir
iex> Enum.any?(["foo", "bar", "hello"], fn(s) -> String.length(s) == 5 end)
true
```

### chunk

Если нужно разбить коллекцию на меньшие группы, метод `chunk` - это то, что нужно:

```elixir
iex> Enum.chunk([1, 2, 3, 4, 5, 6], 2)
[[1, 2], [3, 4], [5, 6]]
```

Также есть несколько дополнительных опций, которые вы можете посмотреть в документации: [`chunk/2`](http://elixir-lang.org/docs/v1.0/elixir/Enum.html#chunk/2).

### chunk_by

Если нужно разделить коллекцию по какому-то другому признаку кроме количества, есть метод `chunk_by`:

```elixir
iex> Enum.chunk_by(["one", "two", "three", "four", "five"], fn(x) -> String.length(x) end)
[["one", "two"], ["three"], ["four", "five"]]
```

### each

Когда нужно пройти по коллекции без создания нового значения - используется метод `each`:

```elixir
iex> Enum.each(["one", "two", "three"], fn(s) -> IO.puts(s) end)
one
two
three
```

__Замечение__: Метод `each` не возвращает атом `:ok`.

### map

Когда нужно применить функцию для преобразования каждого элемента коллекции - подходит функция `map`:

```elixir
iex> Enum.map([0, 1, 2, 3], fn(x) -> x - 1 end)
[-1, 0, 1, 2]
```

### min

Функция `min` возвращает минимальное значение коллекции:

```elixir
iex> Enum.min([5, 3, 0, -1])
-1
```

### max

Функция `max` находит максимальное значение в коллекции:

```elixir
iex> Enum.max([5, 3, 0, -1])
5
```

### reduce

С помощью функции `reduce` можно обьединить все элементы коллекции в единое значение. Для этого можно передать опциональное значение-аккумулятор. Если аккумулятор не передан, то используется первое значение:

```elixir
iex> Enum.reduce([1, 2, 3], 10, fn(x, acc) -> x + acc end)
16
iex> Enum.reduce([1, 2, 3], fn(x, acc) -> x + acc end)
6
```

### sort

Сортировка коллекций реализуется не одной, а двумя функциями `sort`. Первая использует встроенный в язык механизм сравнения:

```elixir
iex> Enum.sort([5, 6, 1, 3, -1, 4])
[-1, 1, 3, 4, 5, 6]

iex> Enum.sort([:foo, "bar", Enum, -1, 4])
[-1, 4, Enum, :foo, "bar"]
```

Вторая позволяет передать собственную функцию для сравнения элементов:

```elixir
# with our function
iex> Enum.sort([%{:val => 4}, %{:val => 1}], fn(x, y) -> x[:val] > y[:val] end)
[%{val: 4}, %{val: 1}]

# without
iex> Enum.sort([%{:count => 4}, %{:count => 1}])
[%{count: 1}, %{count: 4}]
```

### uniq

Для удаления дубликатов из коллекции используется функция `uniq`:

```elixir
iex> Enum.uniq([1, 2, 2, 3, 3, 3, 4, 4, 4, 4])
[1, 2, 3, 4]
```
