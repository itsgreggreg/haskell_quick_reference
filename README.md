# Haskell Quick Reference
 - Haskell home page : https://www.haskell.org/
 - API search : https://www.haskell.org/hoogle/
 - 5 minute haskell introduction : https://www.tryhaskell.org/
 - Try Haskell online : https://glot.io/new/haskell , https://repl.it/languages/haskell
 - Style guide : https://github.com/tibbe/haskell-style-guide/blob/master/haskell-style.md
 
### Tools
 - Code linter : https://github.com/ndmitchell/hlint
 - All in 1 platform : https://docs.haskellstack.org
 
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

# Reserved Words

| | | | | | | | |
|-|-|-|-|-|-|-|-|
|as|case|class|data|default|deriving|do|else|
|family|forall|foreign|hiding|if|import|in|infix|
|infixl|infixr|instance|let|mdo|module|newtype|of|
|proc|qualified|rec|then |type|where| | |

# Reserved Symbols
| | | | | | | | |
|-|-|-|-|-|-|-|-|
| \` |'|"|-|--|-<|-<<|->|
|::|;|<-|,|=|=>|>|~|
|!|?| #| *| @| [\|, \|]| `\` | _ |
|{, }|{-, -}|\|| | | | | | |
