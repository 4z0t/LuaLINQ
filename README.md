# Lua LINQ Library Documentation

A functional approach to working with collections in Lua, inspired by .NET LINQ.

## Enumerator

Enumerator provides a chainable API for collection operations. Each method returns a new Enumerator instance.

### Creation Methods

#### `EnumeratorCreate(iterator, transformer)`
- Creates a new Enumerator instance
- Parameters:
  - `iterator`: Function that iterates over collection
  - `transformer`: Optional function that transforms the input collection
- Returns: New Enumerator instance

### Transformation Methods

#### `:Select(selector)`
- Projects each element into a new form
- Parameters:
  - `selector`: Function `(value, key) -> result` or string/number key
- Returns: New Enumerator with transformed elements

#### `:Where(condition)`
- Filters elements based on a predicate
- Parameters:
  - `condition`: Function `(value, key) -> boolean`
- Returns: New Enumerator with filtered elements

#### `:Distinct()`
- Returns distinct elements from the sequence
- Returns: New Enumerator with duplicate elements removed

#### `:GroupBy(selector)`
- Groups elements by key selector
- Parameters:
  - `selector`: Function `(value, key) -> groupKey`
- Returns: New Enumerator with grouped elements

#### `:Sort(comparer)`
- Sorts elements in sequence
- Parameters:
  - `comparer`: Optional function `(left, right) -> boolean`
- Returns: New Enumerator with sorted elements

#### `:Reverse()`
- Reverses the sequence
- Returns: New Enumerator with reversed elements

#### `:AsSet()`
- Converts sequence to set (table with true values)
- Returns: New Enumerator representing set

### Terminal Operations

#### `:Execute(callback)`
- Executes callback for each element
- Parameters:
  - `callback`: Function `(value, key)`
- Returns: Function that performs the execution

#### `:ToArray()`
- Converts sequence to array
- Returns: Function that produces array

#### `:ToTable(selector)`
- Converts sequence to table
- Parameters:
  - `selector`: Optional function `(key, value) -> newKey, newValue`
- Returns: Function that produces table

#### `:Min(comparer)`
- Finds minimum element
- Parameters:
  - `comparer`: Optional function `(left, right) -> boolean`
- Returns: Function that returns minimum value

#### `:Max(comparer)`
- Finds maximum element
- Parameters:
  - `comparer`: Optional function `(left, right) -> boolean`
- Returns: Function that returns maximum value

#### `:Average()`
- Calculates average of numeric sequence
- Returns: Function that returns average value

#### `:Sum()`
- Calculates sum of numeric sequence
- Returns: Function that returns sum

#### `:Count(condition)`
- Counts elements matching condition
- Parameters:
  - `condition`: Optional function `(value, key) -> boolean`
- Returns: Function that returns count

## Enumerable

Enumerable provides similar functionality but modifies the existing instance instead of creating new ones.

### Creation Methods

#### `EnumerableCreate(t, iterator, transformer)`
- Creates new Enumerable instance
- Parameters:
  - `t`: Source table
  - `iterator`: Optional iterator function
  - `transformer`: Optional transformer function
- Returns: New Enumerable instance

### Transformation Methods

Same method names and parameters as Enumerator, but modifies current instance:
- `:Select(selector)`
- `:Where(condition)`
- `:Distinct()`
- `:GroupBy(selector)`
- `:Sort(comparer)`
- `:Reverse()`
- `:AsSet()`

### Additional Methods

#### `:Clone()`
- Creates copy of current Enumerable
- Returns: New Enumerable instance

#### `:Cache()`
- Creates new Enumerable with cached results
- Returns: New Enumerable with materialized results

### Terminal Operations

Same method names and parameters as Enumerator, but returns results directly instead of functions:
- `:Execute(callback)`
- `:ToArray()`
- `:ToTable(selector)`
- `:Min(comparer)`
- `:Max(comparer)`
- `:Average()`
- `:Sum()`
- `:Count(condition)`

## Usage Example

```lua
-- Using Enumerator
local enumerator = EnumeratorCreate(_ipairs)
    :Where(function(v) return v > 5 end)
    :Select(function(v) return v * 2 end)
    :ToArray()

local t = enumerator({1,2,3,4,5,6,7,8,9,10})

-- Using Enumerable
local result = EnumerableCreate({1,2,3,4,5,6,7,8,9,10})
    :Where(function(v) return v > 5 end)
    :Select(function(v) return v * 2 end)
    :ToArray()
```

## Enumerator

| Method                      | Description                                                                                |
| --------------------------- | ------------------------------------------------------------------------------------------ |
| `:__call(t)`                | Returns iterator and transformed table for iteration within for loop                       |
| `:Where(condition)`         | Filters elements based on a predicate                                                      |
| `:Select(selector)`         | Projects each element into a new form                                                      |
| `:Keys()`                   | Returns keys of the table                                                                  |
| `:Distinct()`               | Returns distinct elements from the sequence keeping original order                         |
| `:Foreach(func)`            | Executes a function for each element                                                       |
| `:Reverse()`                | Reverses the sequence                                                                      |
| `:GroupBy(selector)`        | Groups elements by key selector                                                            |
| `:Sort(comparer?)`          | Sorts elements in sequence                                                                 |
| `:AsSet()`                  | Returns set of elements                                                                    |
| `:Execute(func)`            | Executes a function for each element                                                       |
| `:Min(comparer?)`           | Finds minimum element                                                                      |
| `:Max(comparer?)`           | Finds maximum element                                                                      |
| `:Any(condition?)`          | Checks if any element matches condition                                                    |
| `:All(condition?)`          | Checks if all elements match condition                                                     |
| `:First(condition?)`        | Returns first element that matches condition                                               |
| `:Last(condition?)`         | Returns last element that matches condition                                                |
| `:Reduce(reducer, initial)` | Applies a function to each element and accumulates the result                              |
| `:Average()`                | Calculates average of numeric sequence                                                     |
| `:Count(condition?)`        | Counts elements matching condition                                                         |
| `:Sum()`                    | Calculates sum of numeric sequence                                                         |
| `:Contains(value)`          | Checks if sequence contains a specific value                                               |
| `:ToFunction()`             | Returns function that returns iterator and transformed table for iteration within for loop |
| `:ToIterator()`             | Returns iterator with scoped table for iteration within for loop                           |
| `:ToArray()`                | Converts sequence to array                                                                 |
| `:ToTable(selector?)`       | Converts sequence to table with optional key-value selector                                |

## Enumerable

| Method                      | Description                                                          |
| --------------------------- | -------------------------------------------------------------------- |
| `:__call()`                 | Returns iterator and transformed table for iteration within for loop |
| `:Clone()`                  | Creates copy of current Enumerable                                   |
| `:Where(condition)`         | Filters elements based on a predicate                                |
| `:Select(selector)`         | Projects each element into a new form                                |
| `:Keys()`                   | Returns keys of the table                                            |
| `:Distinct()`               | Returns distinct elements from the sequence keeping original order   |
| `:Select(selector)`         | Projects each element into a new form                                |
| `:Keys()`                   | Returns keys of the table                                            |
| `:Distinct()`               | Returns distinct elements from the sequence keeping original order   |
| `:Foreach(func)`            | Executes a function for each element                                 |
| `:Reverse()`                | Reverses the sequence                                                |
| `:GroupBy(selector)`        | Groups elements by key selector                                      |
| `:Sort(comparer?)`          | Sorts elements in sequence                                           |
| `:AsSet()`                  | Returns set of elements                                              |
| `:Execute(func)`            | Executes a function for each element                                 |
| `:Cache()`                  | Creates new Enumerable with cached table after transformation        |
| `:First(condition?)`        | Returns first element that matches condition                         |
| `:Last(condition?)`         | Returns last element that matches condition                          |
| `:Average()`                | Calculates average of numeric sequence                               |
| `:Count(condition?)`        | Counts elements matching condition                                   |
| `:Reduce(reducer, initial)` | Applies a function to each element and accumulates the result        |
| `:Sum()`                    | Calculates sum of numeric sequence                                   |
| `:Contains(value)`          | Checks if sequence contains a specific value                         |
| `:Min(comparer?)`           | Finds minimum element                                                |
| `:Max(comparer?)`           | Finds maximum element                                                |
| `:All(condition?)`          | Checks if all elements match condition                               |
| `:Any(condition?)`          | Checks if any element matches condition                              |
| `:ToArray()`                | Converts sequence to array                                           |
| `:ToTable(selector?)`       | Converts sequence to table with optional key-value selector          |