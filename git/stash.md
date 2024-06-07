## 未コミットのファイルの一時退避
- スタッシュを保存
```
git stash save "stash message"
```
<br>

- 過去に保存したスタッシュのリストを確認
```
git stash list

stash@{0}: WIP on validation-duration#75: 54056d8 Update README.md
```
<br>

- スタッシュリストの一番上の変更を適用
```
git stash apply
```
<br>

- スタッシュ名を指定して適用
```
git stash apply stash@{0}
```
<br>

- スタッシュの削除
```
git stash drop stash@{0}
```
退避した作業を適用してもスタッシュはそのまま残っている
<br>

- スタッシュを適用すると同時に削除
```
git stash pop stash@{0}
```
<br>

### 参考
[【git stash】コミットはせずに変更を退避したいとき](https://qiita.com/chihiro/items/f373873d5c2dfbd03250)
