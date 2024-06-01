## 前のコミットを取り消し  
```
git reset --soft HEAD^
```  

## 取り消しの取り消し  
1. 操作履歴の確認  
```
git reflog
```  

1. 特定の時点までファイルを巻き戻す
```
git reser --hard HEAD@{n}
``` 

## 参考  
- [第7話 間違えて reset しちゃった？git reflogで元どおり【連載】マンガでわかるGit ～コマンド編～](https://www.r-staffing.co.jp/engineer/entry/20191227_1)
