---
title: hello world
---

When using a table as a structure, you can treat indices as member names (e.g., `a.name` is equivalent to `a["name"]`).

`a.x` represents `a["x"]`, i.e., the table indexed by the string `"x"`, while `a[x]` refers to the table indexed by the value of the variable `x`.

```lua
a = {}
x = "y"
a[x] = 10           -- put 10 in field "y"
a[x]       --> 10   -- value of field "y"
a.x        --> nil  -- value of field "x" (undefined)
a.y        --> 10   -- value of field "y"
```

An array with no `nil` elements is called a sequence.

Lua provides the length operator `#` for obtaining the length of a sequence.

Use the `pairs` iterator to traverse key-value pairs in a table; for lists, you can use `ipairs` (integer pairs) iterator.

The return value of the `type` functions is always a string.

```lua
N = 8  -- board size

-- Check whether position (n, c) is not under attack
function isplaceok (a, n, c)
  for i = 1, n - 1 do  -- for each queen already placed
    if (a[i] == c) or           -- same column?
      (a[i] - i == c - n) or    -- same diagonal?
      (a[i] + i == c + n) then  -- same diagonal?
      return false    -- position would be attacked
    end
  end
  return true  -- no attack: position is vaild
end

-- Print a chessboard
function printsolution (a)
  for i = 1, N do     -- for each row
    for j = 1, N do   -- and each column
      -- output "X" or "-", plus a space
      io.write(a[i] == j and "X" or "-", " ")
    end
    io.write("\n")
  end
  io.write("\n")
end

-- Place queens from 'n' to 'N' on board 'a'
function addqueen (a, n)
  if n > N then     -- all queens placed?
    printsolution(a)
  else  -- try to place the n-th queen
    for c = 1, N do
      if isplaceok(a, n, c) then
        a[n] = c    --  place the n-th queen in column
        addqueen(a, n + 1)
      end
    end
  end
end

-- Run the program
addqueen({}, 1)
```

