## シーケンスを使ってユニークなデータを生成する

### やりたいこと
- create_listで作成されるテストデータの値をすべてユニークにしたい  
（uniqueness: { scope: :bookmark_id }になっているため）
```
create_list(:timestamp, 10, bookmark: bookmark)
```

### 方法
- spec/factories/timestamps.rb
```
FactoryBot.define do
  factory :timestamp do
    hour { 0 }
    sequence(:minute) { |n| n }
    sequence(:second) { |n| n }
    sequence(:start_time) { |n| 0 + n.to_i * 60 + n.to_i }
  end
end
```
sequenceを使うことで新しいオブジェクトを作成するたびにカウンタの値が1ずつ増える

### 参考
- everyday Rails RSpecによるRailsテスト入門
