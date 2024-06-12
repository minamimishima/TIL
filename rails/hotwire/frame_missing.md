## turbo:frame-missing
### やりたいこと
- Turbo Frames内のdestroy実行時のみフルリロードしたい

### 状況
- カテゴリーを削除すると、遷移先のbookmarks_pathに対応するフレームがないため`Content Missing`と表示される

### 解決策
- `turbo:frame-missing`の使用

### 方法
- JavaScriptファイルの作成
```
document.addEventListener('turbo:frame-missing', (e) => {
  const { detail: { response, visit } } = e;
  e.preventDefault();
  visit(response.url);
});
```

### 参考
- [Hotwire公式](https://turbo.hotwired.dev/reference/events#turbo%3Aframe-missing)
- [Getting a Turbo Frame Error of "Content Missing"](https://stackoverflow.com/questions/75738570/getting-a-turbo-frame-error-of-content-missing)
- [[Rails]turboとstimulusによるモーダル](https://zenn.dev/redheadchloe/articles/34e9c211981dc6)
