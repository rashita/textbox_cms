# Markdown Flat-file CMS Template

`list/` フォルダ内のMarkdownファイルを読み込んで表示する、シンプルなフラットファイルCMSです。  
サーバーサイドは不要で、静的ホスティング（GitHub Pages, Netlify等）で動きます。

**Demo**: https://rashita.github.io/textbox_cms/

## フォルダ構成

```
/
├── index.html        ← メインファイル。設定もここに書く
├── js/
│   └── marked.min.js ← Markdownパーサー（変更不要）
├── css/
│   └── style.css     ← グローバルスタイル（自由に編集）
├── image/            ← 画像ファイル置き場
├── list/
│   ├── index.md      ← トップページ
│   └── (任意の.mdファイル)
└── README.md
```

## セットアップ

1. このリポジトリをダウンロード（またはフォーク）する
2. `index.html` の設定ブロックを編集する（後述）
3. `list/` フォルダにMarkdownファイルを置く
4. ローカル確認: `http-server` や `python -m http.server 8000` 等で起動

> **注意**: `fetch()` を使うため、ファイルをブラウザで直接開く（`file://`）だけでは動きません。ローカルサーバーが必要です。

## 設定方法

`index.html` 冒頭の **設定ブロック** を書き換えます。

```javascript
// サイトが動くオリジン
const SITE_ORIGINS = [
  "https://example.com/?",    // 本番URL
  "http://localhost:8000/?"   // ローカル開発URL
];

// トップページとして使うファイル
const INDEX_FILE = "list/index.md";

// MDファイル内の <script> タグを実行する機能
// true: 有効 / false: 無効
const ENABLE_MD_SCRIPT = false;
```

あわせて以下も変更してください：

- `<title>` タグのサイト名
- `<nav>` 内の `<h1>` のサイト名
- `<meta name="description">` の説明文
- フッターの著作権表記

## 記法

### ページ間リンク

```
[[ファイル名]]
```

`list/` フォルダ内の `.md` ファイルにリンクします。拡張子は不要です。

例: `[[about]]` → `list/about.md` を開く

### Markdown

標準的なMarkdown記法が使えます（[marked.js](https://marked.js.org/) で処理）。

- 見出し `#` `##` `###`
- **太字** `**text**`
- *斜体* `*text*`
- リスト `- item`
- 引用 `> text`
- コード `` `code` `` / ` ```block``` `
- 外部リンク `[text](url)`
- 画像 `![alt](path)`

### MDファイル内スクリプト（上級）

`ENABLE_MD_SCRIPT = true` にすると、MDファイル内の `<script>` タグが実行されます。  
ページごとにインタラクティブなコンテンツを埋め込みたい場合に使います。  
信頼できるコンテンツのみ扱う環境での使用を想定しています。

## URL構造

| URL | 表示されるファイル |
|-----|--------------|
| `https://example.com/` | `list/index.md` |
| `https://example.com/?about` | `list/about.md` |
| `https://example.com/?blog/post1` | `list/blog/post1.md` |

## ブラウザ履歴

ページ遷移は History API で管理されています。ブラウザの「戻る/進む」ボタンが正しく動作します。

## ライセンス

MIT
