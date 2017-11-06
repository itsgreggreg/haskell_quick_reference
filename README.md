### Creating types
#### Alias
```haskell
type Age = Int
```
#### New Type
```haskell
newtype Age = Age Int
```

### Algebraic Data Types
```haskell
data Pet = Hamster Age | Fish Age
```
