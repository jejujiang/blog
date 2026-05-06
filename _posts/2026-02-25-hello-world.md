---
title: hello world
---

当把表当作结构体使用时，可以把索引当作成员名称使用（`a.name`等价于`a["name"]`）。

`a.x`代表的是`a["x"]`，即由字符串`"x"`索引的表；而`a[x]`则是指由变量`x`对应的值索引的表。

```lua
a = {}
x = "y"
a[x] = 10           -- 把10放在字段“y“中
a[x]       --> 10   -- 字段“y”的值
a.x        --> nil  -- 字段“x”的值（未定义）
a.y        --> 10   -- 字段“y”的值
```

所有元素都不为`nil`的数组称为序列（sequence）。

Lua语言提供里获取序列长度的操作符`#`。

使用pairs迭代器遍历表中的键值对；对于列表而言，可以使用ipairs（integer pairs）迭代器。

`type`函数的返回值永远是一个字符串。


```lua
N = 8  -- 棋盘大小

-- 检查（n，c）是否不会被攻击
function isplaceok (a, n, c)
  for i = 1, n - 1 do  -- 对于每一个已经被放置的皇后
    if (a[i] == c) or           -- 同一列？
      (a[i] - i == c - n) or    -- 同一对角线？
      (a[i] + i == c + n) then  -- 同一对角线？
      return false    -- 位置会被攻击
    end
  end
  return true  -- 不会被攻击；位置有效
end

-- 打印棋盘
function printsolution (a)
  for i = 1, N do     -- 对于每一行
    for j = 1, N do   -- 和每一列
      -- 输出“X”或“-”，外加一个空格
      io.write(a[i] == j and "X" or "-", " ")
    end
    io.write("\n")
  end
  io.write("\n")
end

-- 把从'n'到'N'的所有皇后放在棋盘'a'上
function addqueen (a, n)
  if n > N then     -- 是否所有的皇后都被放置好了？
    printsolution(a)
  else  -- 尝试着放置第n个皇后
    for c = 1, N do
      if isplaceok(a, n, c) then
        a[n] = c    --  把第n个皇后放在列'c'
        addqueen(a, n + 1)
      end
    end
  end
end

-- 运行程序
addqueen({}, 1)
```

