## コミットメッセージの修正
### やりたいこと
- 2つ以上前のコミットメッセージの修正

### 方法
- `git rebase -i HEAD~3`  
修正したいコミットまでの数を入れる

- viエディタが開くので`i`で入力モードに切り替え、修正したいコミットの`pick`を`edit`に変更  

- `Esc`でコマンドモードに切り替え`:wq!`で上書き保存・終了  
<br>

**この時点で`edit`を指定したコミットまで状況が戻っている！**  
<br>

- コミットを修正
```
git commit --amend -m "修正後のメッセージ"
git rebase --continue
```  

複数のコミットをeditにしていた場合は`git rebase --continue`を実行すると次のコミットに移るので、再度`git commit --amend`で修正

### 参考
- [Gitのコミットメッセージを後から変更する方法をわかりやすく書いてみた](https://www.granfairs.com/blog/entry-3159/)
