## インスタンスの値を変更したときのテスト
### やりたいこと
- インスタンスの値が更新できていることをテストしたい

### 方法
- `expect(user.reload.name)`のように記述する  

- 実際のシステムスペックの記述
```
it "自分のプロフィールを編集する" do
  user = create(:user, name: "元の名前", profile: "元のプロフィール")
  login_as(user, :scope => :user)
  visit user_path(user)
  click_on "プロフィール編集"
  fill_in "名前", with: "新しい名前"
  fill_in "プロフィール", with: "新しいプロフィール"
  click_on "変更"
  aggregate_failures do
    expect(user.reload.name).to eq "新しい名前"  #この部分！
    expect(user.reload.profile).to eq "新しいプロフィール"
  end
end
```

最初は下のように記述していてテストが通らなかった
```
expect(user.name).to eq "新しい名前"
```

- `save_and_open_page`で確認すると変更できてるのになぜ？  

すでに読み込まれたインスタンスの値は更新されないので明示的にreloadする必要がある


### 参考
- [rspecでupdateのテストを通せない初心者が疑うべきこと](https://qiita.com/ry_2718/items/3ffdf7c24857fc5724c2)
