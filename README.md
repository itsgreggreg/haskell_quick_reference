### Creating types
#### Alias an Eixisting type
 - Creates merely an `alias` for an existing type.
 - Can make code more readable.
 - Can be used interchangeably with what is being aliased. Compiler don't care.
```haskell
--    ┌ Age is simply an alias for Int, they can be used interchangeably
--    ⇣
type Age = 
  Int
```

#### Create a new type
 - Creates a `brand new` type.
```haskell
--       ┌ Type Name
--       ⇣
newtype Age = 
  Age Int
-- |   ↳ What you must pass in to construct this type
-- ↳ Value Constructor
```

#### data
 - `data` creates either a __Tagged Union__ or a __Record Type__
 
__Tagged union__:
```haskell
data Pet 
  = Hamster Age 
  | Fish Age
```
From the standard lib:
```haskell
data Bool
  = True
  | False
```

__Record Type__:
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
--          ┌ Type Variable
--          ⇣
 data Maybe a
   = Just a
   | Nothing
```

### Type Classes
#### Class

#### Instance
