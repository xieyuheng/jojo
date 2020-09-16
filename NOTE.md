# syntax

- `(x: T)` -- local variable.

- be able to use json easily
  - `[ { x: 1, y: 2 } (obj) obj.x obj.y add ] (three)`

- non recursive local function
  - `[ dup mul ] (square)`
  - `[ (f) [ (x) x x f ] [ (x) x x f ] ] (Y)`

# semantic

- if a function return function,
  the returned function will not be be applied implicitly.
