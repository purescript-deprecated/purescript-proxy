# Module Documentation

## Module Type.Proxy


The `Proxy` type and values are for situations where type information is
required for an input to determine the type of an output, but where it is
not possible or convenient to provide a _value_ for the input.

A hypothetical example: if you have a class that is used to handle the
result of an AJAX request, you may want to use this information to set the
expected content type of the request, so you might have a class something
like this:

``` purescript
class AjaxResponse a where
  responseType :: a -> ResponseType
  fromResponse :: Foreign -> a
```

The problem here is `responseType` requires a value of type `a`, but we
won't have a value of that type until the request has been completed. The
solution is to use a `Proxy` type instead:

``` purescript
class AjaxResponse a where
  responseType :: Proxy a -> ResponseType
  fromResponse :: Foreign -> a
```

We can now call `responseType (Proxy :: Proxy SomeContentType)` to produce
a `ResponseType` for `SomeContentType` without having to construct some
empty version of `SomeContentType` first.

#### `Proxy`

``` purescript
data Proxy a
  = Proxy 
```

Value proxy for kind `*` types.

#### `Proxy2`

``` purescript
data Proxy2 (a :: * -> *)
  = Proxy2 
```

Value proxy for kind `* -> *` types.

#### `Proxy3`

``` purescript
data Proxy3 (a :: * -> * -> *)
  = Proxy3 
```

Value proxy for kind `* -> * -> *` types.



