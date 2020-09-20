# JoJo

> Two level of compositions, one at function level, one at type level.

- `(x: T)` -- local variable.
- if a function return function, will the returned function be applied?
- `[ dup mul ] (square)`
- `[ { x: 1, y: 2 } (obj) obj.x obj.y add ] (three)`
- `[ (f) [ (x) x x f ] [ (x) x x f ] ] (Y)`

## List

``` jojo
@ty List [ Type - Type ]
@fn List [ (A) @datatype {
    null [ A List ]
    cons [ A - A List - A List ]
  }
]

@ty List.append [ A List - A List - A List ]
@fn List.append [ (y) @match {
    List.null [ y ]
    List.cons [ (head) (tail) y tail List.append head List.cons ]
  }
]

@ty List.map [ [ A - B ] - A List - B List ]
@fn List.map [ (f) (x) x @match {
    List.null [ x ]
    List.cons [ (head) [f] List.map head f List.cons ]
  }
]
```
