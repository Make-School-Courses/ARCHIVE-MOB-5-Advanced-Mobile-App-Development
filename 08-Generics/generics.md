# Advanced Swift - Generics, Enums, Protocols

### Objectives
- Generic functions
- Generic enums
- Protocols with associated types

## Generics
Swift standard library is made up of structs, enums, protocols and generics


## Generic Functions

```swift
func<T>()
```

Equatable
```swift
func !=<T: Equatable>(lhs: T, rhs: T) -> Bool {
    return !(lhs == rhs)
}
```

## Generic Enums


## Protocols with Associated Types
Its a way to achieve generics with protocols

```swift
protocol Animal {
    associatedType Food = String
}

struct
```

```