# Bless Lab 血糖値安定アドバイザー — Netlify デプロイ手順

このフォルダ（`netlify-site/`）の中身が、Netlifyに載せる公開ファイル一式です。

```
netlify-site/
├── index.html      … アプリ本体（1ファイル完結）
├── netlify.toml    … キャッシュ制御などの設定
├── _headers        … キャッシュ制御のフォールバック
└── README.md       … この手順書
```

---

## 方法A：新しいGitHubリポジトリ経由で連携（推奨・自動更新）

一度つないでおけば、GitHubに変更を push するたびにNetlifyが自動で再公開します。

1. **新しいGitHubリポジトリを作成**
   - GitHubで「New repository」→ 例：`blesslab-app`（Public/Privateどちらでも可）

2. **このフォルダの中身をリポジトリの直下に置く**
   - `index.html` / `netlify.toml` / `_headers` を**リポジトリのルート**に置く
   - （`netlify-site/` というフォルダごとではなく、**中身**をルートへ）

3. **Netlifyと連携**
   - Netlify（https://app.netlify.com）にログイン
   - 「Add new site」→「Import an existing project」→ GitHubを選択
   - 作成したリポジトリを選ぶ
   - Build設定：
     - **Build command：空欄でOK**（ビルド不要）
     - **Publish directory：`.`（ルート）**
   - 「Deploy site」

4. 数十秒で `https://ランダム名.netlify.app` が発行されます。
   - サイト名は Netlify の Site settings → Change site name で変更可能
   - 独自ドメインも Domain settings から設定できます

5. 以降は、GitHubにpushするだけで自動更新されます。

---

## 方法B：ドラッグ&ドロップ（一番手軽・お試し向き）

1. Netlifyにログイン →「Add new site」→「Deploy manually」
2. この `netlify-site` フォルダを**そのままドラッグ&ドロップ**
3. すぐ公開されます

※この方法は自動更新されないので、更新のたびに再ドロップが必要です。
　継続運用するなら方法Aがおすすめです。

---

## キャッシュについて

`netlify.toml` / `_headers` で、**HTMLは毎回サーバーに最新を確認**する設定にしてあります。
これにより「更新したのに古い画面が出る」問題を、サーバー側から根本的に防ぎます。

内容を更新したら、`index.html` を差し替えて push（方法A）または再ドロップ（方法B）すれば、
利用者には次のアクセスから最新版が表示されます。

---

## 補足

- このアプリは外部通信のない**1ファイル完結**の静的サイトです。
  サーバー処理・データベースは不要で、Netlifyの無料枠で十分動作します。
- 利用者の「実践回数・継続日数」は各自の端末（ブラウザ）に保存されます。
  端末をまたいで記録を共有したい場合は、別途ログイン機能とデータ保存先が必要になります。
