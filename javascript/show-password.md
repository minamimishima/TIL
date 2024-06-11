## パスワードの表示・非表示を切り替える
### 方法
- JavaScript作成
```
function showUserPassword() {
  let user_password = document.getElementById("user_password");
  let user_password_btn = document.getElementById("user_password_btn");

  if(user_password) {
    user_password_btn.addEventListener('click', (e) => {
      e.preventDefault();
      if (user_password.type === "password") {
        user_password.type = "text";
        user_password_btn.innerHTML = "<i class='bi bi-eye-slash-fill' aria-label='パスワードを非表示'></i>";
      } else {
        user_password.type = "password";
        user_password_btn.innerHTML = "<i class='bi bi-eye-fill' aria-label='パスワードを表示'></i>";
      }
    });
  };
};

document.addEventListener('DOMContentLoaded', function() {
  showUserPassword();
});

document.addEventListener('turbo:render', function() {
  showUserPassword();
});
```
最初は`DOMContentLoaded`を`turbo:load`にしていたが`turbo:render`と競合して無効になってしまった  
`turbo:render`はエラーでrenderされても表示・非表示ボタンを有効にするため  
<br>
  
- フォームのレイアウト崩れを防ぐため`field_with_errors`の設定

Railsはバリデーションエラーがあったフォームを`<div class="field_with_errors"></div>`で囲む  
これが原因でレイアウトが崩れることがあるので、エラーが出てもdivで囲まないよう設定  
  
config/application.rbに下記を追記
```
config.action_view.field_error_proc = Proc.new { |html_tag, instance| html_tag }
```

### メモ
- `e.preventDefault();`  
>フォームが持つデフォルトの動作とは、フォームの内容を指定したURLへ送信するという動作です。 ここではform要素に送信先が指定されていないため、現在のURLに対してフォームの内容を送信します。 しかしこの動作は邪魔になるため、event.preventDefaultメソッドを呼び出すことで、このデフォルトの動作をキャンセルしています。  

### 参考
- [Rails アプリケーションの設定項目](https://railsguides.jp/configuring.html#config-action-view-field-error-proc)
- [Rails の入力フォームのエラー表示のカスタマイズ](https://tech.actindi.net/2021/09/13/143437)
- [Event: preventDefault() メソッド](https://developer.mozilla.org/ja/docs/Web/API/Event/preventDefault)
- [JavaScript Primer](https://jsprimer.net/use-case/todoapp/form-event/#input-to-console)
