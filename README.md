# generics

This package shows an implementation outlook of proposed generics APIs

```go
import "changkun.de/x/generics"
```

Related issues: 

- [golang/go#45458](https://golang.org/issue/45458)
- [golang/go#47319](https://golang.org/issue/47319)
- [golang/go#45955](https://golang.org/issue/45955)
- [golang/go#47203](https://golang.org/issue/47203)
- [golang/go#47331](https://golang.org/issue/47331)
- [golang/go#47330](https://golang.org/issue/47330)

## `constraints`

```go
// Package constraints defines a set of useful constraints to be used with type parameters.
package constraints

type Signed interface { ... }
type Unsigned interface { ... }
type Integer interface { ... }
type Float interface { ... }
type Complex interface { ... }
type Ordered interface { ... }
type Slice[Elem any] interface { []Elem }
```

## `slices`

```go
// Package slices defines various functions useful with slices of any type.
// Unless otherwise specified, these functions all apply to the elements
// of a slice at index 0 <= i < len(s).
package slices

import "constraints"

func Equal[T comparable](s1, s2 []T) bool
func EqualFunc[T1, T2 any](s1 []T1, s2 []T2, eq func(T1, T2) bool) bool
func Compare[T constraints.Ordered](s1, s2 []T) int
func CompareFunc[T any](s1, s2 []T, cmp func(T, T) int) int
func Index[T comparable](s []T, v T) int
func IndexFunc[T any](s []T, f func(T) bool) int
func Contains[T comparable](s []T, v T) bool
func Insert[S constraints.Slice[T], T any](s S, i int, v ...T) S
func Delete[S constraints.Slice[T], T any](s S, i, j int) S
func Clone[S constraints.Slice[T], T any](s S) S
func Compact[S constraints.Slice[T], T comparable](s S) S
func CompactFunc[S constraints.Slice[T], T any](s S, cmp func(T, T) bool) S
func Grow[S constraints.Slice[T], T any](s S, n int) S
func Clip[S constraints.Slice[T], T any](s S) S
```

## `maps`

```go
// Package maps defines various functions useful with maps of any type.
package maps

func Keys[K comparable, V any](m map[K]V) []K
func Values[K comparable, V any](m map[K]V) []V
func Equal[K, V comparable](m1, m2 map[K]V) bool
func EqualFunc[K comparable, V1, V2 any](m1 map[K]V1, m2 map[K]V2, cmp func(V1, V2) bool) bool
func Clear[K comparable, V any](m map[K]V)
func Clone[K comparable, V any](m map[K]V) map[K]V
func Add[K comparable, V any](dst, src map[K]V)
func Filter[K comparable, V any](m map[K]V, keep func(K, V) bool)
```

## `container/set`

```go
// Package set defines a Set type that holds a set of elements.
package set

type Set[Elem comparable] struct { ... }
func (s *Set[Elem]) Add(v ...Elem)
func (s *Set[Elem]) AddSet(s2 Set[Elem])
func (s *Set[Elem]) Remove(v ...Elem)
func (s *Set[Elem]) RemoveSet(s2 Set[Elem])
func (s *Set[Elem]) Has(v Elem) bool
func (s *Set[Elem]) HasAny(s2 Set[Elem]) bool
func (s *Set[Elem]) HasAll(s2 Set[Elem]) bool
func (s *Set[Elem]) Values() []Elem
func (s *Set[Elem]) Equal(s2 Set[Elem]) bool
func (s *Set[Elem]) Clear()
func (s *Set[Elem]) Clone() Set[Elem]
func (s *Set[Elem]) Filter(keep func(Elem) bool)
func (s *Set[Elem]) Len() int
func (s *Set[Elem]) Do(f func(Elem) bool)

func Of[Elem comparable](v ...Elem) Set[Elem]
func Union[Elem comparable](s1, s2 Set[Elem]) Set[Elem]
func Intersection[Elem comparable](s1, s2 Set[Elem]) Set[Elem]
func Difference[Elem comparable](s1, s2 Set[Elem]) Set[Elem]
```

## License 

Copyright &copy; 2021 [Changkun Ou](https://changkun.de), release under BSD 3-Clause License