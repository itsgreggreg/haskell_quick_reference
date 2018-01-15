# Haskell Quick Reference
 - Haskell home page : https://www.haskell.org/
 - API search : https://www.haskell.org/hoogle/
 - 5 minute haskell introduction : https://www.tryhaskell.org/
 - Try Haskell online : https://glot.io/new/haskell , https://repl.it/languages/haskell
 - Online Repl : https://repl.it/languages/haskell
 - Style guide : https://github.com/tibbe/haskell-style-guide/blob/master/haskell-style.md
 
### Tools
 - Code Formatter : https://github.com/commercialhaskell/hindent
 - Code linter : https://github.com/ndmitchell/hlint
 - All in 1 platform : https://docs.haskellstack.org

# Primitive Data Types
## Numbers
 - Written literally
 - All Integers are of type `Num` when written literally
 - `Num`s can be coerced into any Integer or Float type
 - All Floats are of type `Fractional` when written literally
 - `Fractional`s cannot be coerced to Integrs
```haskell
> :t 1
1 :: Num t => t
> :t 1.5
1.5 :: Fractional t => t
> 10 == (10 :: Integer)
True
> 10 == 10.0
True
> 10.0 == (10 :: Integer)
error
```
 
### Integers
 - Written literally as a series of didgits
 - `Int` for machine integers
 - `Integer` for arbitrary precision
 - Use `Integer` unless you know you need `Int`
 
```haskell
> a = 10 :: Integer
> b = 3 :: Integer
> a / b               -- Connot use / to divide integers
error
> div a b             -- div for integer division
3
> rem a b             -- rem is modulus
1
> div a (3 :: Int)    -- Cannot mix int types
error
> :t fromIntegral a   -- Convert an Int(egral) type to a Num type
fromIntegral a :: Num b => b
```
#### Int
 - Implementations vary, guaranteed to be at least 30 bits.
```Haskell
> 9223372036854775807 :: Int
=> 9223372036854775807
> 9223372036854775808 :: Int
<interactive>:81:1: warning: [-Woverflowed-literals]
    Literal 9223372036854775808 is out of the Int range -9223372036854775808..9223372036854775807
```
#### Integer
 - Can hold values up to the memory limit of your machine
```haskell
> 9223372036854775808 :: Integer
=> 9223372036854775808
```
## Floats
 - `Double`	for Double-precision floating point.
 - `Float`	for Single-precision floating point. Often used when interfacing with C.
 - Use `Double` unless you know you need `Float`
 
## Char
 - TODO Encoding
## List
## String
 - A __List__ of __Characters__
 - TODO overloading strings
 
 - There is no string interpolation.
 - But formatting is built into the standard library
http://hackage.haskell.org/package/base-4.2.0.1/docs/Text-Printf.html
```haskell
> let a = [1,2,3,4]
> Text.Printf.printf "the length of %s is %d\n" (show a) (length a)
> elem 1 [2,3,4]
False
> elem 1 [1,2,3]
True
```

# Types
## Creating types
### Alias an Eixisting type
 - Creates merely an `alias` for an existing type.
 - Can make code more readable.
 - Can be used interchangeably with what is being aliased. Compiler don't care.
```haskell
--    ┌ Age is simply an alias for Int, they can be used interchangeably
--    ⇣
type Age = Int
```
From the standard lib:
```haskell
type String = [Char] 
-- "String" is an alias for "List of Characters"
```

### New Simple Type
 - Creates a `brand new` type.
 - It is common to name the `Value Constructor` the same as the `Type Name`
```haskell
--       ┌ Type Name
--       ⇣
newtype Age = 
  Age Int
-- ↑   └ What you must pass in to construct this type
-- └ Value Constructor

-- A function called "Age" that takes one "Int" now exists and it produces the value "Age some-int" 
-- which has a type of "Age"
```

 - Can take multiple paramaters
```haskell
newtype Coordinates = 
  Coordinates Int Int
--            ↑    └ Paramater 2
--            └ Paramater 1

-- the function "Coordinates" now requires 2 paramaters an "Int" and another "Int" in
-- order to produce the value "Coordinates some-int some-int" of type "Coordinates"
```

### Tagged Union
- Simply a Type with multiple `Value Constructors`
- It is common to name the `Value Constructors` differently than the `Type Name`

```haskell
--    ┌ Type Name
--    ⇣
data Pet 
  = Hamster Age 
  | Fish Age
--   ↑
--   └ "Tag" -or- "Type constructor"

-- Now the functions "Hamster" and "Fish" exist and they produce a value with the type of "Pet"
```
From the standard lib:
```haskell
data Bool
  = True
  | False
```

### Record Type
 - Simply a type who's value is a composite of many fields.
 
```haskell
data Person = Person 
  { name :: String
  , age :: Age
  }
```

## Type Variables
 - All of our types above are __concrete__ -or-  __monomorphic__.
 - To make a type definition __polymorphic__ simply add a __variable__.
 
### tagged union
```haskell
--         ┌ Type Variable
--         ⇣
data Maybe a
  = Nothing
  | Just a
--       ↑
--       └ The constructor "Just" can be passed a value of any type to produce a value of type "Maybe"
```

## Type Classes
 
### Functor
 - Generalizes function application over containers
 - `<$>` is the infix alias for `fmap`
 - `a <$ b` is the same as `const a <$> b`
 - Since Functor requires a kind of `* -> *` it _must_ only work on 1 type variable
 - for `(a, b)` it works on `b` and leaves `a` unchanged.
 - for `Either a b` it works on `b` and leaves `a` unchanged.
 
```haskell
class Functor (f :: * -> *) where
  fmap :: (a -> b) -> f a -> f b
  (<$) :: a -> f b -> f a
```

```haskell
> fmap ((*) 2) [1,2,3]
-- [2,4,6]
> (*) 2 <$> [1,2,3]
-- [2,4,6]
> fmap ((*) 2) (Just 10)
-- Just 20
> fmap ((*) 2) (Left 10)
-- Left 10
> fmap ((*) 2) (Right 10)
-- Right 20
> fmap ((*) 2) (10,10)
-- (10, 20)

> "Hello" <$ Just 10
-- Just "Hello"
> Nothing <$ [1,2,3]
-- [Nothing,Nothing,Nothing]
```

### Class
 - We define a __typeclass__ with the `class` keyword.
 
Defining our own polymorphic equality (==) function:
```haskell
class MyEq a where
    equal :: a -> a -> Bool
    
    notEqual :: a -> a -> Bool
    notEqual x y = not (equal x y)
```

### Instance
 - We define __implementations__ of the __typeclass__ with the `instance` keyword
 - Since `notEqual` has a default implementation that depends on `equal` we only have to specify `equal`
 
Implementing `equal` for `Bool`:
 ```haskell
 instance MyEq Bool where
    equal True  True  = True
    equal False False = True
    equal _     _     = False
 ```

# Syntax
## Common Infix Functions
`(.)` : Function Composition
```haskell
> :t (.)
-- (.) :: (b -> c) -> (a -> b) -> a -> c
> a = ((*) 2) . const 4
> a 123
-- 8
> a Nothing
-- 8
```

`($)` : Pipe Left
```haskell
> :t ($)
-- ($) :: (a -> b) -> a -> b
> head $ map (*2) [13, 50, 1000]
-- 26
```

## Defining Functions
### Guards
 - The first guard that evaluates to `true` is run.
 - `otherwise == true`
 - If no guards match and there are no other function heads, you will get `Exception: Non-exhaustive patterns in function myFun`
```haskell
myFilt :: (a -> Bool) -> [a] -> [a]
myFilt _ [] = []
myFilt f (x:xs)
  | f x       = x : myFilt f xs
  | otherwise = myFilt f xs
  
> myFilt even [1..10]
[2,4,6,8,10]


isFour :: (Eq a, Num a) => a -> Bool
isFour a
    | a == 4 = True
    
> isFour 4
True
> isFour 5
*** Exception: Non-exhaustive patterns in function isFour
```

## List Comprehensions
```haskell
> [ x ^ 2 | x <- [1..10]]
[1,4,9,16,25,36,49,64,81,100]
> [(x, y) | x <- [1..10], y <- [1..10], x > 7, y < 3]
[(8,1),(8,2),(9,1),(9,2),(10,1),(10,2)]
-- Remember, Strings are Lists
> [ x | x <- "This is Haskell", elem x ['A'..'Z']]
"TH"
```
## Reserved Words

| | | | | | | | |
|-|-|-|-|-|-|-|-|
|as|case|class|data|default|deriving|do|else|
|family|forall|foreign|hiding|if|import|in|infix|
|infixl|infixr|instance|let|mdo|module|newtype|of|
|proc|qualified|rec|then |type|where| | |

## Reserved Symbols
| | | | | | | | |
|-|-|-|-|-|-|-|-|
| \` |'|"|-|--|-<|-<<|->|
|::|;|<-|,|=|=>|>|~|
|!|?| #| *| @| [\|, \|]| `\` | _ |
|{, }|{-, -}|\|| | | | | | |

# Quasi Quotes
 - Enabled per file with `{-# LANGUAGE  QuasiQuotes #-}`
 - Enabled on the compiler with `-XQuasiQuotes`
 - Let you use/implement a DSL to write haskell
 - Follows format of `[functionName| some-content |]` 
 - Are context aware so you can include bindings in scope

Truncated example for producing html in haskell with Yesod:
```haskell
{-# LANGUAGE QuasiQuotes #-}
import Text.Hamlet (shamlet)

--                              ┌ Quasi Quoter called shamlet
--                              ⇣
main = putStrLn $ renderHtml [shamlet|
  <p>Hello, my name is #{name person} and I am 
    <strong> #{show $ age person}.
  |]
-- └ Close the quasi quotes
  where
    name = "Michael"
    age = 26
--   ↑
--   └ Bindings
```

# Repl
 - Start by running `ghci`
 - If you're using Stack, start by running `stack ghci` or `stack repl`
 
 ## Useful Commands
  - `:help` -or- `:h` : Print a list of repl commands
  - `:type some-value` -or- `:t some-value` : Display type information for a value
  - `:load some-module` -or- `:l some-module` : Load a module into the repl
  - `:reload` -or- `:r` : Reload all loaded modules
  - `:module` -or- `:m` : Unload all loaded modules
  
```haskell
> :t Nothing
Nothing :: Maybe a

> :t (round 1.5)
(round 1.5) :: Integral b => b
```

# More Fun Stuff
 - Literate Haskell : https://wiki.haskell.org/Literate_programming
