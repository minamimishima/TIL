- `each_cons(n)`  
要素を重複ありでn要素ずつに区切り、ブロックに渡して繰り返し
```
例
(1..10).each_cons(3){|v| p v }
# => [1, 2, 3]
#    [2, 3, 4]
#    [3, 4, 5]
#    [4, 5, 6]
#    [5, 6, 7]
#    [6, 7, 8]
#    [7, 8, 9]
#    [8, 9, 10]
```
