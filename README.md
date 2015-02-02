# Hoersten Haskell Style Guide

In general, shorter functions and modules are preferred. If functions
are more than five lines and modules more than five functions,
consider breaking them up into smaller functions and modules.

[stylish-haskell][] is used where it has a default opinion and will be
noted in the following sections.

## Indentation

Indent four spaces, no tabs. A dangling `do` and `where` are indented
two spaces (the only exception to four spaces).

``` haskell
main =
  do
    foo
    bar x
  where
    x = 1
```

## Line Length

Loosely prefer 80 columns but readability should take precedence over
column length. Nesting more than three scopes (12 columns) should be
avoided.

## Modules

The `where` should be on the same line as the module name unless there
are exports.

```haskell
module Main where
```

A module with exports should be indented four spaces, one export per
line, aligning the `(`, `)`, and `,`, ending with a space between the
closing `)` and `where`.

```haskell
module Main
    ( foo
    , bar
    , baz
    ) where
```

Section documentation should be aligned with the export names.

```haskell
module Main
    ( -- * Section 1
      foo
    , bar

      -- * Section 2
    , baz
    ) where
```

## Imports

Imports are *always* explicit or qualified.

Use [stylish-haskell][] to organize imports. Unqualified imports are
always 11 spaces after the `import` keyword to line up with
`qualified` imports. Import lists should all be aligned to the longest
module name. Types should typically be used unqualified unless name
conflicts.

```haskell
import           Control.Applicative ((<$>))
import           System.Directory    (doesFileExist)

import           Data.Map            (Map, keys, (!))
import qualified Data.Map            as M
```

## Functions

All top level functions should have signatures and be separated by two
lines.

```haskell
import Data.List


foo :: IO ()
foo = do stuff


bar :: IO ()
bar = baz
```

## Types

Two spaces should separate all type declarations except one-line types
like `newtype`, `type`, and simple sum types. These can be packed
together with other related single-line types.

```haskell
data Z
    = A
    | B
    | C
    | deriving (Show)


data Bool = True | False deriving Show
newtype X = X { unX :: Int } deriving Show
type Y = Int
```

Longer sum types should align the `=`, `|`, and `deriving` with an
indentation of four spaces.

```haskell
data Weekdays
    = Monday
    | Tuesday
    | Wednesday
    | Thursday
    | Friday
    deriving (Show)
```

Record types should be organized by [stylish-haskell][]. This means
the type and data constructors on the same line, and the `{`, `}`, and
`,` aligned at four spaces with the `deriving` following the closing
bracket. The field types should also be aligned.

```haskell
data Point = Point
    { pointX    :: Double
    , pointName :: String
    } deriving (Show)
```

Record syntax should never be used within a sum type.

## Operators

Always space out multi-operator expressions.

```haskell
foo = x y * z * y
```

## Collections

Always follow `,` in collections with a space.

```haskell
(a, b, c)
[1, 2, 3]
[(1, 2), (3, 4), (5, 6)]
```

In record updates, do not separate field and value with spaces.

```haskell
let rec' = rec{a=1, b=2, c=3}
```

Long collections should vertically align by the `[`, `]`, and `,` at
four spaces with the `]` dangling.

```haskell
let x =
    [ 1
    , 2
    , 3
    , 4
    ]
```


[stylish-haskell]: https://github.com/jaspervdj/stylish-haskell
