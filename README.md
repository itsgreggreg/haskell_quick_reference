### Creating types
#### type
 - Creates merely an `alias` for an existing type.
 - Can make code more readable
```haskell
type Age = 
  Int
```
#### newtype
 - Creates a `brand new` type.
```haskell
newtype Age = 
  Age Int
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
            ┌ Type Variable
--          ⇣
 data Maybe a
   = Just a
   | Nothing
```

### Type Classes
#### Class

#### Instance
