### Creating types
 - Types being the foundation of functional programming we must be able to define our own.
 - These are all the ways we can do so in Haskell:
#### Alias an Eixisting type
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

#### New Simple Type
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

#### Tagged Union
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

#### Record Type
 - Simply a type who's value is a composite of many fields.
 
```haskell
data Person = Person 
  { name :: String
  , age :: Age
  }
```

### Type Variables
 - All of our types above are __concrete__ -or-  __monomorphic__.
 - To make a type definition __polymorphic__ simply add a __variable__.
 
#### tagged union
```haskell
--         ┌ Type Variable
--         ⇣
data Maybe a
  = Nothing
  | Just a
--       ↑
--       └ The constructor "Just" can be passed a value of any type to produce a value of type "Maybe"
```

### Type Classes
#### Class

#### Instance
