- `max_by`
>各要素を順番にブロックに渡して実行し、その評価結果を <=> で比較して、最大であった値に対応する元の要素、もしくは最大の n 要素が降順で入った配列を返します。

```
例
a = %w(albatross dog horse)
a.max_by                    # => #<Enumerator: ["albatross", "dog", "horse"]:max_by>
a.max_by { |x| x.length }   # => "albatross"
```

### 参考
- [リファレンスマニュアル](https://docs.ruby-lang.org/ja/latest/method/Enumerable/i/max_by.html)
