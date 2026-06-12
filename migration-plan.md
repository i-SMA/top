# i-SMA 静的サイト移行計画

作成日：2026-05-19  
対象URL：https://i-sma.or.jp/top/  
移行先：isma-site/ フォルダ（新規サーバーへアップロード用）

---

## 1. 現行サイト調査結果

### サイト構成

現行サイトは **WordPress (Cocoonテーマ)** で運用されており、基本的には `/top/` を起点とする **シングルページ構成** + アンカーリンクで動作している。

| 現行URL | 内容 | 移行後URL |
|---------|------|-----------|
| https://i-sma.or.jp/top/ | トップページ（全セクション含む） | /index.html |
| https://i-sma.or.jp/aboutus/ | 社団概要 | /aboutus/index.html |
| https://i-sma.or.jp/top/#aboutus | 私たちについて（トップ内アンカー） | /index.html#aboutus |
| https://i-sma.or.jp/top/#member | 理事紹介（トップ内アンカー） | /index.html#member |
| https://i-sma.or.jp/top/#service | 活動内容（トップ内アンカー） | /index.html#service |
| https://i-sma.or.jp/top/#news | お知らせ（トップ内アンカー） | /index.html#news |
| https://i-sma.or.jp/top/#seminer | セミナー・イベント（トップ内アンカー） | /index.html#events |
| https://i-sma.or.jp/top/#contact | お問い合わせ（トップ内アンカー） | /index.html#contact |
| https://i-sma.or.jp/events/* | 各イベント個別ページ（WordPress） | /events/index.html（一覧のみ） |

### ナビゲーション

```
ヘッダー：ロゴ ｜ 私たちについて ｜ 理事紹介 ｜ 社団概要 ｜ 活動内容 ｜ お知らせ ｜ セミナーイベント ｜ お問い合わせ
フッター：同上（テキストリンク）
```

### 外部リンク（維持必須）

| 用途 | URL |
|------|-----|
| 入会申し込みフォーム | https://docs.google.com/forms/d/1Xh5hhNtlzg6HxlladOqgked1OSx1xmMe95K5OUEBrBQ/edit |

---

## 2. ページ一覧と移行方針

### index.html（トップページ）

以下のセクションをすべて1ページに含める：

| セクション | 移行方針 |
|-----------|---------|
| ヒーロー | 英語タイトル + 日本語名 + 入会CTAボタン |
| 私たちについて (#aboutus) | 画像 + キャッチコピー + 説明文 + 社団概要リンク |
| 活動内容 (#service) | 勉強会・交流会 / 専門家マッチング の2カード |
| 理事および監事 (#member) | directors.json から動的生成 |
| 会員企業・幹事会社 | 3社ロゴ |
| お知らせ (#news) | news.json から最新5件表示、一覧リンク |
| セミナー・イベント (#events) | events.json から直近4件 + 過去イベント、一覧リンク |
| お問い合わせCTA (#contact) | フォーム（Formspree連携 または mailto fallback） |

### aboutus/index.html（社団概要）

| 項目 | 内容 |
|------|------|
| 法人名 | 一般社団法人 サステナビリティマネジメント＆アシュアランス機構 |
| 英名 | Institute of Sustainability Management and Assurance |
| 略称 | i-SMA（アイスマ） |
| 所在地 | 東京都渋谷区恵比寿西2丁目4番8号 ウィンド恵比寿ビル8階 |
| 代表理事 | 水口 剛 |
| 設立日 | 2024年4月22日（地球の日） |
| 事業内容 | ネットワーク構築支援 / 研修・勉強会開催 / 保証・認証支援および紹介 / コンサルティング先紹介 |

### news/index.html（お知らせ一覧）

news.json から全件表示。個別記事はWordPressの既存URLを外部リンクとして維持。

### events/index.html（セミナー・イベント一覧）

events.json から全件表示（予定・済み分類）。

### contact/index.html（お問い合わせ）

フォームフィールド：名前 / メールアドレス / 電話番号 / お問い合わせ種別 / メッセージ

---

## 3. 必要アセット一覧

### 画像（wp-contentからダウンロードまたは差し替えが必要）

| 現行ファイル名 | 用途 | 移行後パス | 備考 |
|--------------|------|-----------|------|
| A基本ロゴ.png | ヘッダーロゴ | assets/images/logo.png | 必須 |
| toranomon_880x1080.png | Aboutセクション | assets/images/toranomon.png | 必須 |
| isma_sa.png | 活動内容（マッチング） | assets/images/isma_sa.png | 必須 |
| 双葉マーク宝印刷-1.jpg | 会員企業ロゴ | assets/images/logo-takarasho.jpg | 必須 |
| D-04.jpg | 会員企業ロゴ | assets/images/logo-d04.jpg | 必須 |
| QUICK_TaglineLogo_Blue.png | 会員企業ロゴ | assets/images/logo-quick.png | 必須 |
| 勉強会スケジュール0519.png | 活動内容（勉強会スケジュール） | assets/images/schedule.png | 要更新（日付入り） |
| B日本語.png | 不明 | assets/images/b-japanese.png | 用途確認が必要 |
| スライド1.jpg | お知らせサムネイル | assets/images/news-forum2024.jpg | |
| 会計士協会-120x68.jpg | お知らせサムネイル | assets/images/news-jicpa.jpg | |
| 202405RIJAPAN-e1716354096508-120x68.png | お知らせサムネイル | assets/images/news-rijapan.png | |
| 第２回i-SMAフォーラム_サムネイルrev.pptx.png | お知らせサムネイル | assets/images/news-forum2025.png | |
| topthumbnail.png | 社団概要 | assets/images/topthumbnail.png | |
| feature-icon-1.svg | 活動内容アイコン | assets/images/icon-study.svg | 外部CDN→ローカル化 |
| feature-icon-2.svg | 活動内容アイコン | assets/images/icon-matching.svg | 外部CDN→ローカル化 |

**重要：** 理事・監事の顔写真は現行サイトに存在しない（テキストのみの表示）。

### JavaScriptライブラリ

| ライブラリ | 用途 | 方針 |
|-----------|------|------|
| なし（現行はjQuery/WPプラグイン） | DOM操作 | バニラJSで実装 |

### フォント・アイコン

| リソース | 方針 |
|---------|------|
| フォント | Google Fonts（Noto Sans JP）CDN利用 |
| アイコン | Font Awesome CDN または SVGインライン |

---

## 4. JSONデータ設計

### data/news.json

```json
[
  {
    "id": 1,
    "date": "2026-02-06",
    "title": "i-SMA理事 山本が「第10回 サステナブル・ブランド国際会議」に登壇いたします",
    "url": "https://i-sma.or.jp/i-sma%e7%90%86%e4%ba%8b-%e5%b1%b1%e6%9c%ac...",
    "thumbnail": "assets/images/news-placeholder.png",
    "category": "お知らせ"
  }
]
```

### data/events.json

```json
[
  {
    "id": 22,
    "date": "2026-08-31",
    "title": "第22回 i-SMA勉強会 8月",
    "format": "オンライン",
    "time": "18:30〜20:00",
    "url": "https://i-sma.or.jp/events/...",
    "status": "upcoming"
  }
]
```

### data/directors.json

```json
[
  {
    "role": "理事長",
    "name": "水口 剛",
    "name_en": "Takeshi Mizuguchi",
    "affiliation": "公立大学法人 高崎経済大学 学長",
    "qualifications": [],
    "photo": "assets/images/directors/placeholder.png"
  }
]
```

---

## 5. お問い合わせフォームの方針

WordPressのContact Form 7はWordPress依存のため使用不可。以下の方法を検討：

| 方法 | メリット | デメリット |
|------|---------|-----------|
| Formspree | 静的サイトから直接POST可能、無料枠あり | 月50件制限（無料） |
| Google フォーム埋め込み | 無料、管理が簡単 | デザインのカスタマイズ限定的 |
| mailto: リンク | 実装不要 | メールクライアント依存 |

**推奨：Formspree**（action="https://formspree.io/f/YOUR_FORM_ID"）  
**要確認：** フォームIDはFormspreeアカウント作成後に発行。先方での確認が必要。

暫定対応として、現行サイトのGoogle入会フォームへのリンクをCTAに配置する。

---

## 6. リダイレクト設定案

新サーバーへの移行後、旧URLから新URLへのリダイレクトが必要な場合：

| 旧URL | 新URL | 方法 |
|-------|-------|------|
| /top/ | / | .htaccess Redirect |
| /aboutus/ | /aboutus/ | そのまま維持 |
| /top/#news | /#news | .htaccess Redirect |
| /events/* | /events/ | .htaccess RewriteRule |

---

## 7. 作業計画

| ステップ | 作業内容 | ファイル |
|---------|---------|---------|
| 1 | ディレクトリ構成作成 | isma-site/ 全体 |
| 2 | 共通CSS作成 | assets/css/style.css |
| 3 | JSONデータ作成 | data/news.json, events.json, directors.json |
| 4 | トップページ作成 | index.html |
| 5 | 社団概要ページ作成 | aboutus/index.html |
| 6 | お知らせ一覧ページ作成 | news/index.html |
| 7 | セミナー・イベント一覧ページ作成 | events/index.html |
| 8 | お問い合わせページ作成 | contact/index.html |
| 9 | JavaScript（動的表示）作成 | assets/js/main.js |
| 10 | sitemap.xml / robots.txt 作成 | ルート |
| 11 | リンク・表示確認 | 全ページ |

---

## 8. 確認が必要な事項（人間確認）

- [ ] 理事・監事の写真素材（現行サイトに写真なし→提供が必要か確認）
- [ ] 「B日本語.png」の用途（サイト内での表示箇所が不明）
- [ ] お問い合わせフォームのバックエンド（Formspreeアカウント作成、またはGoogleフォーム利用の方針確認）
- [ ] 勉強会スケジュール画像（`勉強会スケジュール0519.png`）の更新頻度と提供方法
- [ ] 新サーバーのドメイン・URLルール（`/top/` を廃止してルートに移行するか確認）
- [ ] 入会申し込みGoogleフォームのURLが最新か確認
- [ ] イベント個別ページ（WordPress）へのリンクを維持するか、一覧ページのみとするか確認
- [ ] .htaccess リダイレクト設定をサーバー管理者に依頼するか確認

---

## 9. 公開前チェックリスト

- [ ] 全ページのtitleタグ・meta description・OGP設定
- [ ] h1/h2/h3の階層確認
- [ ] スマートフォン表示（320px〜768px）
- [ ] 内部リンク切れなし
- [ ] 外部リンク（Googleフォーム）の動作確認
- [ ] 画像の表示確認（alt属性設定含む）
- [ ] sitemap.xml のURL確認
- [ ] robots.txt の設定確認
- [ ] JSONデータの読み込み確認（ローカルサーバーで要確認）

---

## 10. ディレクトリ構成（最終形）

```
isma-site/
├── index.html
├── aboutus/
│   └── index.html
├── news/
│   └── index.html
├── events/
│   └── index.html
├── contact/
│   └── index.html
├── assets/
│   ├── css/
│   │   └── style.css
│   ├── js/
│   │   └── main.js
│   └── images/
│       ├── logo.png
│       ├── toranomon.png
│       ├── isma_sa.png
│       ├── schedule.png
│       ├── logo-takarasho.jpg
│       ├── logo-d04.jpg
│       ├── logo-quick.png
│       ├── icon-study.svg
│       ├── icon-matching.svg
│       ├── news-forum2024.jpg
│       ├── news-jicpa.jpg
│       ├── news-rijapan.png
│       ├── news-forum2025.png
│       └── directors/
│           └── (理事写真 - 未入手)
├── data/
│   ├── news.json
│   ├── events.json
│   └── directors.json
├── sitemap.xml
└── robots.txt
```
