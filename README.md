# 拍品検索アプリ（Google Sheets連携版）

## これは何？
Google Sheets のデータをそのまま読み込んで表示する、**サーバー不要**の1枚の Web ページです。
GitHub Pages で公開すれば、Mac を起動しっぱなしにする必要も、同じ WiFi に接続する必要もなくなり、
**インターネットさえあればどこからでも**（外出先の4G/5Gでも）iPhone から使えます。

画像表示は今回のバージョンには含まれていません（テキスト情報のみ）。

---

## 事前準備：Google Sheet を公開設定にする

1. Google Sheet を開く
2. 右上の「共有」ボタン → 「一般的なアクセス」を **「リンクを知っている全員」** に変更（閲覧者でOK）
3. これで誰でも（ログインなしで）このシートのデータを読み取れるようになります
   ※ 編集権限を与えるわけではないので、データを書き換えられる心配はありません

---

## STEP 1: コードの設定を自分のシートに合わせる

`index.html` をテキストエディタ（メモ帳や TextEdit でOK）で開き、
`<script>` タグの中にある以下の部分を自分の Google Sheet に合わせて書き換えます：

```javascript
const SPREADSHEET_ID = '1Z5kHRR3kX6Nl5iqZZUf-u-kBKk79BINzTHqz2GZZrp0';
const SHEET_NAME = 'Sheet2';
```

- `SPREADSHEET_ID`：Google Sheet の URL の中の長い英数字部分
  例：`https://docs.google.com/spreadsheets/d/【ここの部分】/edit?usp=sharing`
- `SHEET_NAME`：データが入っている**シート（タブ）の名前**。Google Sheet 画面の下部にあるタブ名を確認してください
  （今回いただいたリンクでは `Sheet2` というタブに入っているようでしたので、これをデフォルト値にしています。
  違っていたら実際のタブ名に書き換えてください）

書き換えたら保存します。

---

## STEP 2: GitHub にアップロードする（コマンド不要・ブラウザだけでOK）

1. https://github.com にアクセスしてログイン（アカウントがなければ無料登録）
2. 右上の「+」→「New repository」をクリック
3. Repository name に好きな名前を入力（例：`auction-lookup`）→ **Public** を選択 → 「Create repository」
4. 作成されたリポジトリのページで「uploading an existing file」というリンクをクリック
   （または画面上部の「Add file」→「Upload files」）
5. `index.html` ファイルをドラッグ＆ドロップ
6. 下にスクロールして「Commit changes」ボタンをクリック

これでアップロード完了です。

---

## STEP 3: GitHub Pages を有効にして公開する

1. リポジトリ画面の上部メニューから「Settings」をクリック
2. 左メニューの「Pages」をクリック
3. 「Build and deployment」の「Source」を **「Deploy from a branch」** に設定
4. 「Branch」を **「main」**、フォルダは **「/ (root)」** を選択 → 「Save」
5. 1〜2分待つと、ページ上部に
   `Your site is live at https://（あなたのユーザー名）.github.io/（リポジトリ名）/`
   というURLが表示されます

このURLを iPhone の Safari で開けば、どこからでも（WiFiでも4Gでも）拍品検索ができます。
「共有」→「ホーム画面に追加」しておくと、アプリのように使えて便利です。

---

## データを更新したいとき

Google Sheet に新しい行を追加・編集して保存するだけでOKです。
アプリ側は何もする必要はありません。ページを開くたびに最新のデータを自動で読み込みます
（右上の🔄ボタンでいつでも手動更新も可能です）。

---

## よくある質問

**Q: ページを開いたら「数据加载失败」と出る**
A: 主な原因は次の3つです。
1. Google Sheet の共有設定が「リンクを知っている全員」になっていない → 上の事前準備を確認
2. `SHEET_NAME` がタブの実際の名前と違う → Google Sheet 下部のタブ名を確認して修正
3. 表のヘッダー行の文字が「拍卖号」「拍品编号」などと完全に一致していない → 表記ゆれ（全角/半角、スペース等）を確認

**Q: リポジトリは Public にしないとダメ？**
A: GitHub Pages を無料プランで使う場合は Public 公開が必要です。中身は拍品リストのテキストデータのみで、
画像や個人情報は含まれていませんが、気になる場合は「オークション番号」などの機微な情報を
別カラムに分けて非公開にする運用も検討してください。

**Q: 前のバージョン（Mac で起動するタイプ）とはどちらを使えばいい？**
A: 今後は基本的にこちらの Google Sheets 連携版がおすすめです。Mac を毎回起動する必要がなく、
WiFi の接続トラブルも起きません。画像表示が必要になったら、その時にまた対応します。
