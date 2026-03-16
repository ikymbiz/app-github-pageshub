提供されたHTMLソースコードを分析し、プロジェクトの魅力を最大限に伝える高品質な `README.md` を作成しました。

このアプリは、単一のHTMLファイルにIndexedDB、Web Worker、PWA機能などを詰め込んだ非常に高度でモダンな作りになっているため、技術的なハイライトも盛り込んだ構成にしています。

---

```markdown
# 🐙 My GitHub Pages Hub

[![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat-square&logo=html5&logoColor=white)](#)
[![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat-square&logo=javascript&logoColor=black)](#)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-38B2AC?style=flat-square&logo=tailwind-css&logoColor=white)](#)
[![PWA](https://img.shields.io/badge/PWA-5A0FC8?style=flat-square&logo=pwa&logoColor=white)](#)

自身の（またはお気に入りの）**GitHub Pages を一元管理・監視するためのローカルファーストな PWA ツール** です。
1つの HTML ファイルのみで構成されながら、Web Worker を用いた非同期通信、IndexedDB によるローカルデータ管理、GitHub API との高度な連携機能を実現しています。

## ✨ 主な機能

- 🔍 **自動検出 & 一括同期**
  - GitHub PAT (Personal Access Token) を設定することで、あなたのアカウント内の有効な GitHub Pages を自動で検出し、一覧に追加します。
- 📖 **Readme アプリ内プレビュー**
  - リポジトリに遷移することなく、アプリ内で `README.md` をレンダリングして表示します（Marked.js & DOMPurify 採用による安全な表示）。
- ⚡ **UI をブロックしないバックグラウンド処理**
  - 大量のリポジトリ情報の取得や同期は **Web Worker** で処理されるため、同期中も画面がフリーズしません。
- 💾 **ローカルファースト & データ保護**
  - データはすべてブラウザの **IndexedDB** に保存されます。外部サーバーへのデータ送信はありません。
  - **5世代の自動バックアップ機能** を備え、いつでも過去の状態に復元可能です。
  - JSON形式でのエクスポート/インポートに対応しています。
- 📱 **モバイル最適化 & PWA対応**
  - ボトムナビゲーションやスワイプを意識したモバイルファーストなデザイン（Tailwind CSS）。
  - マニフェストファイルを動的生成し、スマートフォン等にアプリとしてインストール可能です（PWA）。
- 🔋 **省電力・通信量削減**
  - GitHub API の `If-Modified-Since` ヘッダーを利用し、更新がない場合は通信を行わない（HTTP 304）エコな設計です。
  - 同期中は **Wake Lock API** を使用し、デバイスのスリープを防止します。

## 🚀 使い方

### 1. 起動方法
このプロジェクトはサーバーを必要としない完全なフロントエンドアプリです。
`index.html` をブラウザで開くだけですぐに使用できます。
（※ GitHub Pages等でホスティングすると、別端末からもアクセスでき、PWAとしてインストールしやすくなります）

### 2. GitHub PAT の設定（推奨）
APIのレートリミット（利用制限）を回避し、自動検出機能を有効にするために、GitHub PATの設定を推奨します。

1. 画面右上の ⚙️（歯車アイコン）をクリックして設定を開きます。
2. **API Key (PAT)** セクションに、GitHubで発行した PAT を入力し「保存」を押します。
   - ※ 必要なスコープ: 自身のプライベートリポジトリのPagesも検出したい場合は `repo` スコープが必要です。公開リポジトリのみであればスコープ無し（または `public_repo`）でも機能します。

### 3. ページの追加
- **自動追加**: ボトムナビゲーションの「一括同期」ボタンを押すと、PATを利用してあなたのリポジトリからPagesを自動検索して追加します。
- **手動追加**: 中央の青い「＋」ボタンから、任意の GitHub Pages URL を入力して管理することも可能です。

## 🛠 技術スタック

- **UI / スタイリング**
  - HTML5 / Vanilla JavaScript
  - [Tailwind CSS](https://tailwindcss.com/) (CDN) + Typography plugin
  - [FontAwesome 6](https://fontawesome.com/) (アイコン)
- **Markdown レンダリング**
  - [Marked.js](https://marked.js.org/) (Markdown パース)
  - [DOMPurify](https://github.com/cure53/DOMPurify) (XSS サニタイズ)
- **Web API**
  - `IndexedDB` (ローカルデータベース / Promiseラッパー実装)
  - `Web Workers API` (インライン Blob として単一ファイル内に実装)
  - `Wake Lock API` (同期中の画面消灯防止)
  - 動的 `Manifest` 生成 (PWA対応)

## 💡 アーキテクチャのハイライト

このプロジェクトは、**「完全なシングルファイル構成」**でありながら高度な機能を持つよう設計されています。

1. **インライン Web Worker**
   通常、Web Workerは別ファイル（例: `worker.js`）を必要としますが、本アプリでは JavaScript の文字列から `Blob` を生成し、`URL.createObjectURL()` を用いることで、1つのHTMLファイル内で完結させています。
2. **効率的なキャッシュ戦略**
   GitHub API へのリクエスト時に `lastFetch` タイムスタンプを保存し、次回リクエスト時に `If-Modified-Since` ヘッダーを付与します。これにより、不要な API リソースの消費を防ぎ、処理速度を向上させています。
3. **安全な DOM 操作**
   取得した `README.md` を HTML に変換して表示する際、悪意のあるスクリプトの実行を防ぐために `DOMPurify` を使用して必ずサニタイズ処理を行っています。

## 📄 ライセンス

このプロジェクトは [MIT ライセンス](LICENSE) のもとで公開されています。自由にカスタマイズしてご利用ください。

---
*Created with ❤️ for better GitHub Pages management.*
```

### 💡 README.md 作成のポイント
- **バッジの活用**: 視覚的に技術スタックが伝わるようにシールドバッジを配置しました。
- **機能とメリットの結びつけ**: 単に「Web Workerを使っている」と書くのではなく、「UIをブロックしないため画面がフリーズしない」というユーザーメリットに変換して記載しています。
- **アーキテクチャのハイライト**: 今回のコードの最大の特徴である「外部jsファイルを使わずにBlobでWorkerを動かしている点」や「If-Modified-SinceによるエコなAPI通信」など、開発者が読んだときに「おっ、工夫されているな」と思うポイントを特記しました。