# SymEnergy 法人電気 無料お見積りフォーム

低圧の法人さま向け「法人電気の開始・切替」お見積りフォームの専用サイトです。
ビルド不要・依存なしの単一HTML（ロゴ画像も埋め込み済み）で、そのまま公開できます。

## 構成

```
.
├── index.html   … サイト本体（HTML / CSS / JS すべて込み）
├── .nojekyll    … GitHub Pages で Jekyll 処理を無効化
└── README.md
```

## GitHub Pages での公開手順

1. GitHub で新しいリポジトリを作成（例：`symenergy-form`）
2. このフォルダの中身をそのままプッシュ

   ```bash
   git init
   git add .
   git commit -m "add estimate form"
   git branch -M main
   git remote add origin https://github.com/＜ユーザー名＞/symenergy-form.git
   git push -u origin main
   ```

3. リポジトリの **Settings → Pages** を開く
4. **Source: Deploy from a branch / Branch: main / フォルダ: /(root)** を選んで Save
5. 数分後、`https://＜ユーザー名＞.github.io/symenergy-form/` で公開されます

独自ドメインを使う場合は、同じ Pages 設定画面の **Custom domain** に
ドメインを入力し、DNS に CNAME を設定してください。

## カスタマイズポイント（index.html 内）

| 項目 | 場所 | 内容 |
|---|---|---|
| 送信先API | `送信先の実装ポイント` コメント（JS内） | フォームAPI等が決まったら `fetch` を有効化。送信データは `payload` オブジェクトにまとまっています |
| メールアプリ起動 | `var MAIL_LINK = "mailto:";` | 宛先・件名を指定する場合：`"mailto:info@example.co.jp?subject=" + encodeURIComponent("検針票・電気明細の送付")` |
| 外部リンク | フッター / STEP3 同意文 | 特定商取引法に基づく表記・会社概要のURL |
| お申し込みフォーム | 完了画面の `apply-box` 内リンク | 現在：`https://www.symenergy.net/apply?acd=00641aLuDv`（acd＝計測用パラメータ。変更時はここを書き換え） |
| デフォルト選択 | 各 `<input type="radio">` の `checked` | 現在：エリア=関東、法人格=株式会社、連絡方法=どちらでも |

## 現在の仕様メモ

- 送信ボタンはバリデーション通過後に完了画面へ遷移します（バックエンド未接続。内容は `console.log` に出力）
- 検針票・電気明細はフォームからは添付できません。完了メールへの返信で送ってもらう案内導線です
- サンプル書類（検針票／電気明細）はモーダルで表示され、「ご使用量」「供給地点番号」の位置をハイライトで案内します
- 完了画面には「切り替えをお決めの方」向けに、お申し込みフォーム（WEB完結）への誘導ブロックがあります。誘導はあくまで任意で、お見積り結果を待つ導線（メール確認・明細準備）と並立しています
