# イソゲコール LP

賃貸仲介会社向けサービス「イソゲコール」のランディングページ。
HTML / CSS / Vanilla JS のみで構成された静的サイトで、GitHub Pages にそのままデプロイできます。

## ファイル構成

```
isogecall-lp/
├── index.html      … LP本体（10セクション構成）
├── style.css       … デザイン・レスポンシブ
├── README.md       … このファイル
└── assets/
    ├── favicon.svg
    ├── hero-dark.png        … 任意（OGP用に流用可）
    └── lp-reference.png     … OGP画像
```

- 外部フレームワーク不要（Noto Sans JP のみ Google Fonts から読み込み）
- スマホ閲覧優先（390px〜）。PC・タブレットでもレスポンシブ対応
- 画像が無くても CSS グラデーション・アイコンで成立するように構成

## ローカルでの確認

`index.html` をブラウザで直接開くだけで確認できます。

```bash
open index.html
# もしくは簡易サーバー
python3 -m http.server 8000
# → http://localhost:8000
```

## GitHub Pages での公開手順

1. GitHub で新規リポジトリを作成（例: `isogecall-lp`）
2. このフォルダの中身をすべてアップロード（または `git push`）
   ```bash
   git init
   git add .
   git commit -m "Initial commit: isogecall LP"
   git branch -M main
   git remote add origin https://github.com/<your-account>/isogecall-lp.git
   git push -u origin main
   ```
3. GitHub のリポジトリページで **Settings → Pages** を開く
4. **Source** を `Deploy from a branch` にする
5. **Branch** を `main` / `/ (root)` に設定して **Save**
6. 数分後に `https://<your-account>.github.io/isogecall-lp/` で公開されます

## カスタマイズ

### お問い合わせフォーム → Slack 連携

LP最下部のフォーム送信は **Slack Incoming Webhook** に直接POSTされ、指定チャネル（`C0B38MHCJ6M`）に通知されます。

#### Webhook URL の差し替え

`index.html` 内の以下を、実運用の Webhook URL に書き換えてください。

```js
var SLACK_WEBHOOK_URL = "https://hooks.slack.com/services/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";
```

#### Slack側の設定手順（再発行や別チャネルに変更する場合）

1. https://api.slack.com/apps へアクセスし、対象アプリを開く（無ければ「Create New App → From scratch」）
2. **Incoming Webhooks** を有効化
3. **Add New Webhook to Workspace** をクリック
4. 投稿先チャネル（例: `#xxx`、内部ID `C0B38MHCJ6M`）を選択して許可
5. 発行された `https://hooks.slack.com/services/...` を `index.html` の `SLACK_WEBHOOK_URL` に貼り付け

#### セキュリティ上の注意

- Webhook URL は静的サイトに埋め込まれるため、**ブラウザのソースで閲覧可能**です
- 万一スパムや悪用があった場合は、Slack 側で当該 Webhook を **Revoke → 新規発行 → 差し替え** すれば即座に無効化できます
- 将来的に Cloudflare Workers / Vercel Functions などの**サーバーレス Proxy 経由**にすると、URL をクライアントに露出せず安全になります
- 本実装には簡易的な honeypot フィールドを含めており、単純な bot 送信は弾けます

#### 送信メッセージの見え方（Slack側）

```
🆕 LPから新しいお問い合わせ
─────────────────
会社名:        株式会社○○
お名前:        山田 太郎
メール:        taro@example.co.jp
電話番号:      03-0000-0000
お問い合わせ種別: 資料請求
─────────────────
お問い合わせ内容:
○○について詳しく知りたいです。

🌐 送信元: https://xxx.github.io/isogecall-lp/  ／ 🕒 2026/05/19 14:30:00
```

### 料金
`index.html` の「料金プラン」セクション（`#price`）の以下を編集してください。

- 初期費用 `50,000円〜`
- 月額費用 `10,000円〜`
- 含まれる内容（3項目）

### お客様の声
`#voice` セクションの A社 / B社 部分を、実際の導入企業のコメントに差し替えてください。

### OGP画像
`assets/lp-reference.png` を差し替えると、SNS共有時のサムネが切り替わります。
`index.html` 内の `og:image` のパスも必要に応じて変更してください。

## カラー

ダーク（黒〜濃紺）×ネオン（シアン / グリーン / ブルー）のBtoB SaaSテイスト。
カラーは `style.css` 冒頭の `:root` で一括変更できます。

| 役割 | 変数 | 値 |
| --- | --- | --- |
| 背景 | `--bg` | `#020b14` |
| アクセント（シアン） | `--aqua` | `#18e0c2` |
| アクセント（ブルー） | `--blue` | `#1c8dff` |
| アクセント（グリーン） | `--green` | `#3ef58a` |

## ライセンス

社内利用向け。デザイン・コピーの転用はご相談ください。
