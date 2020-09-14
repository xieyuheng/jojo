# JoJo

> Two level of compositions, one at function level, one at type level.

- `(x: T)` -- local variable.
- if a function return function, will the returned function be applied?
- `[ dup mul ] (square)`
- `[ { x: 1, y: 2 } (obj) obj.x obj.y add ] (three)`
- `[ (f) [ (x) x x f ] [ (x) x x f ] ] (Y)`

```
List : [ Type - Type ]
List = [
  (A : Type)
  @datatype {
    null : [ A List ]
    cons : [ A - A List - A List ]
  }
]

List.append : [
  @given(A : type)
  A List -
  A List -
  A List
]

@match {
  List.cons [
    (head: A) (tail: A List)
  ]
}

List.append = [
  (y: A List)
  @match {
    List.null [ y ]
    List.case [
      (head: A) (tail: A List)
      y tail List.append
      head List.cons
    ]
  }
]

List.map : [
  @given(A: type)
  @given(B: type)
  [ A - B ]  A List - B List
]

List.map = [
  (f: [ A - B ])
  (x: A List)
  x @match {
    List.null [ x ]
    List.cons [
      (head: A) (tail: A List)
      tail [f] List.map
      head f List.cons
    ]
  }
]

List.map = [
  (f: [ A - B ])
  (x: A List)
  x @match {
    List.null [ x ]
    List.cons [
      (head: A) [f] List.map
      head f List.cons
    ]
  }
]

List.map = [
  (f: [ A - B ])
  (x: A List)
  x @match {
    List.null [ x ]
    List.cons [
      swap [f] List.map f List.cons
    ]
  }
]

List.map = [
  (f) (x) x @match {
    List.null [x]
    List.cons [(head) [f] List. map head f List.cons]
  }
]

[ (f) (x) x
  [ [List.null] [x]
    [List.cons] [(head) [f] List.map head f List.cons]
  ] match
] (List.map)
```
