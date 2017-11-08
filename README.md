# Haskell Quick Reference
 - Haskell home page : https://www.haskell.org/
 - API search : https://www.haskell.org/hoogle/
 - 5 minute haskell introduction : https://www.tryhaskell.org/
 - Try Haskell online : https://glot.io/new/haskell , https://repl.it/languages/haskell
 - Online Repl : https://repl.it/languages/haskell
 - Style guide : https://github.com/tibbe/haskell-style-guide/blob/master/haskell-style.md
 
### Tools
 - Code linter : https://github.com/ndmitchell/hlint
 - All in 1 platform : https://docs.haskellstack.org

# Primitive Data Types
## Numbers
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
 - For Functions to be __polymorphic__ we must have an understanding of how they will work on different __types__.
 - Type Classes are used for just such a purpose.
 
### Class

### Instance

# Syntax
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

# Repl
 - Start by running `ghci`
 - If you're using Stack, start by running `stack ghci` or `stack repl`
 
 ## Useful Commands
  - `:help` -or- `:h` : Print a list of repl commands
  - `:type some-value` -or- `:t some-value` : Display type information for a value
```haskell
> :t Nothing
Nothing :: Maybe a

> :t (round 1.5)
(round 1.5) :: Integral b => b
```

# More Fun Stuff
 - Literate Haskell : https://wiki.haskell.org/Literate_programming
