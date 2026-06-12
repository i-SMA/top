# i-SMA 静的サイト TODO リスト

作成日：2026-05-19

---

## 1. 画像ファイルの取得（必須・公開前）

現行WordPressサイトの wp-content/uploads/ から以下のファイルをダウンロードし、`assets/images/` に配置する必要があります。

| ダウンロード元URL | 配置先 | 用途 | 優先度 |
|----------------|-------|------|--------|
| https://i-sma.or.jp/wp-content/uploads/2025/01/A基本ロゴ.png | assets/images/logo.png | ヘッダー・フッターロゴ | 高 |
| https://i-sma.or.jp/wp-content/uploads/2024/05/toranomon_880x1080.png | assets/images/toranomon.png | トップ「私たちについて」 | 高 |
| https://i-sma.or.jp/wp-content/uploads/2024/08/isma_sa.png | assets/images/isma_sa.png | 活動内容（マッチング） | 高 |
| https://i-sma.or.jp/wp-content/uploads/2024/08/双葉マーク宝印刷-1.jpg | assets/images/logo-takarasho.jpg | 会員企業ロゴ | 中 |
| https://i-sma.or.jp/wp-content/uploads/2024/08/D-04.jpg | assets/images/logo-d04.jpg | 会員企業ロゴ | 中 |
| https://i-sma.or.jp/wp-content/uploads/2024/08/QUICK_TaglineLogo_Blue.png | assets/images/logo-quick.png | 会員企業ロゴ | 中 |
| https://i-sma.or.jp/wp-content/uploads/2026/05/勉強会スケジュール0519.png | assets/images/schedule.png | 活動内容（勉強会スケジュール）| 高 |
| https://i-sma.or.jp/wp-content/uploads/2024/05/スライド1.jpg | assets/images/news-forum2024.jpg | お知らせサムネイル | 中 |
| https://i-sma.or.jp/wp-content/uploads/2024/06/会計士協会-120x68.jpg | assets/images/news-jicpa.jpg | お知らせサムネイル | 中 |
| https://i-sma.or.jp/wp-content/uploads/2024/05/202405RIJAPAN-e1716354096508-120x68.png | assets/images/news-rijapan.png | お知らせサムネイル | 中 |
| https://i-sma.or.jp/wp-content/uploads/2025/05/第２回i-SMAフォーラム_サムネイルrev.pptx.png | assets/images/news-forum2025.png | お知らせサムネイル | 低 |
| https://i-sma.or.jp/wp-content/uploads/2024/05/topthumbnail.png | assets/images/topthumbnail.png | 社団概要ページ | 中 |

**ダウンロード方法（ブラウザから）：**
各URLをブラウザで開き、「名前を付けて保存」→ 上表の「配置先」パスに保存する。

---

## 2. お問い合わせフォームのバックエンド設定（必須・公開前）

現在 `contact/index.html` のフォームは `action="https://formspree.io/f/YOUR_FORM_ID"` というプレースホルダーになっています。

### 設定手順
1. https://formspree.io でアカウントを作成
2. 新しいフォームを作成し、受信メールアドレスを設定
3. 発行されたフォームIDで `YOUR_FORM_ID` を置き換える
4. `contact/index.html` の以下の行を更新：
   ```html
   <form id="contact-form" action="https://formspree.io/f/【取得したID】" ...>
   ```

**代替案：** Googleフォームを作成して埋め込む（外部フォームとしてリンクする形式でも可）

---

## 3. お知らせ個別記事ページ（任意・後続作業）

現在、お知らせの各記事は現行WordPressサイト（https://i-sma.or.jp/）の記事ページにリンクしています。
WordPressサイトを完全に廃止する場合は、静的サイト内に個別記事ページを作成する必要があります。

| 記事タイトル | 現在のリンク先 | 静的化が必要か |
|------------|-------------|--------------|
| i-SMA理事 山本が「第10回 サステナブル・ブランド国際会議」に登壇 | https://i-sma.or.jp/i-sma... | WordPressが残る間は不要 |
| 山本高嗣氏がi-SMA理事に就任 | https://i-sma.or.jp/... | WordPressが残る間は不要 |
| ２０２４年i-SMA フォーラムを開催致しました | https://i-sma.or.jp/... | WordPressが残る間は不要 |
| JICPA 嶋田理事を紹介 | https://i-sma.or.jp/jicpa... | WordPressが残る間は不要 |
| RI Japan 2024 鶴野理事登壇 | https://i-sma.or.jp/... | WordPressが残る間は不要 |

**対応方針：** WordPress廃止のタイミングで `news/` フォルダ配下に個別HTMLを作成する。

---

## 4. イベント個別ページ（任意・後続作業）

セミナー・イベントの各回（第1回〜第22回）についても同様に、WordPress記事ページにリンクしています。
廃止後は `events/` 配下に個別ページを作成するか、アーカイブPDFとしてまとめることを検討してください。

---

## 5. 理事・監事の顔写真（任意）

現行WordPressサイトには顔写真が掲載されていません。
写真素材が用意できた場合は以下を対応します：

1. `assets/images/directors/` に保存（例：`mizuguchi.jpg`）
2. `data/directors.json` の各人物の `"photo"` フィールドにパスを記入
3. `data/data.js` の該当エントリも同様に更新

---

## 6. 新規サーバーへのアップロード前確認

- [ ] 全画像ファイルが `assets/images/` に揃っているか
- [ ] フォームIDが正式なものに置き換えられているか
- [ ] 新サーバーのドメインに合わせて `sitemap.xml` の URL を更新したか
- [ ] `robots.txt` の Sitemap URL を更新したか
- [ ] ブラウザで各ページを開き、表示崩れがないか（PC・スマホ両方）
- [ ] 全内部リンクが正常に機能するか
- [ ] 入会申し込みGoogleフォームへのリンクが正しく動作するか

---

## 7. 旧サイトURLのリダイレクト設定（サーバー管理者へ依頼）

| 旧URL（WordPress） | 新URL（静的サイト） | .htaccess 設定 |
|------------------|-----------------|---------------|
| /top/ | / | `Redirect 301 /top/ /` |
| /top/#aboutus | /#aboutus | `Redirect 301 /top/ /` （アンカーはリダイレクト先で解決） |
| /aboutus/ | /aboutus/ | そのまま維持 |
| /events/* | /events/ | `RedirectMatch 301 ^/events/.+ /events/` |

---

_このファイルは作業進捗に合わせて随時更新してください。_
