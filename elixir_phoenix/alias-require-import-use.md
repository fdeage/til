# Alias vs Require vs Import vs Use

## Alias

Alias the module so it can be called as Bar instead of Foo.Bar:  
`alias Foo.Bar, as: Bar`

```
defmodule Stats do
  alias Math.Yolo.List, as: Yulu
  # In the remaining module definition List expands to Math.List.
  Yulu.cos(5)
end
```

### Optional `as:`

If the final `as: List` option is omitted, the last part of the module name is aliased to itself.

### Scoping

Note that alias is lexically scoped, which allows you to set aliases inside specific functions:

```
defmodule Math do
  def plus(a, b) do
    alias Math.List
    # ...
  end

  def minus(a, b) do
    # ...
  end
end
```

-> the alias will be valid only inside the function plus/2.

### The `Elixir` prefix
All modules defined in Elixir are defined inside the main Elixir namespace. However, for convenience, you can omit `Elixir.` when referencing them.

(Basically, there is an implicit `import Elixir` on top of all Elixir modules - there is also a `import Kernel` btw)

## Require

Require the module in order to use its macros (but not its functions):
`require Foo`

```
iex> Integer.is_odd(3)
** (UndefinedFunctionError) function Integer.is_odd/1 is undefined or private. However there is a macro with the same name and arity. Be sure to require Integer if you intend to invoke this macro
iex> require Integer
Integer
iex> Integer.is_odd(3)
true
```

In Elixir, Integer.is\_odd/1 is defined as a macro so that it can be used as a guard. This means that, in order to invoke Integer.is\_odd/1, we need to first require the Integer module.

Note that like the alias directive, require is also lexically scoped.


## Import

Import functions from Foo so they can be called without the `Foo.` prefix:
`import Foo`

So it's like `alias`, but even without the module name. In order not to pollute the namespace, it is recommended to specify which with `only`:
```
iex> import List, only: [duplicate: 2]
List
iex> duplicate :ok, 3
[:ok, :ok, :ok]
```
`import` works with functions **and** macros, and it's possible to import only one group:

```import Integer, only: :macros```
or
```import Integer, only: :functions```


`import` is lexically scoped too. This means that we can import specific macros or functions inside function definitions:

```
defmodule Math do
  def some_function do
    import List, only: [duplicate: 2]
    duplicate(:ok, 10)
  end
end
```

## Use

Invokes the custom code defined in Foo as an extension point:  
`use Foo`
