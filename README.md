# イソゲコール LP（公式サイト）

賃貸仲介会社向けサービス「イソゲコール」（運営：株式会社よもやま）の公式ランディングページ。
HTML / CSS / Vanilla JS だけの静的サイトで、**GitHubに保存すると自動で公開**されます（GitHub Pages）。

- 公開URL（独自ドメイン）: **https://isogecall.com/**
- 予備URL（GitHub Pages）: https://t-koza.github.io/isogecall-lp/

---

## 🟢 文章・料金を直したいとき（ノーコード／GitHubの画面だけで完結）

専門知識は不要です。GitHubのWeb画面で文字を書き換えて保存するだけで、数分後にサイトへ反映されます。

### 手順
1. ブラウザで **https://github.com/t-koza/isogecall-lp** を開く
2. 直したいファイルをクリック（文章のほとんどは **`index.html`**）
3. 右上の **鉛筆マーク（✏️ Edit）** をクリック
4. 文字を書き換える（後述の「どこを直す？」を参照）
5. 右上の緑ボタン **「Commit changes」** を押す → そのまま保存
6. **1〜3分待つ** と https://isogecall.com/ に反映されます（反映されないときはブラウザを更新）

> 💡 不安なときは、まず小さな1文字だけ変えて「反映される感覚」を試すのがおすすめです。元に戻したいときは、同じ手順で戻すか、編集画面の履歴から復元できます。

### どこを直す？（`index.html` 内の目印コメントで探せます）
ファイル内を「`▼▼`」で検索すると、編集ポイントにすぐ飛べます。

| 直したいもの | 探す目印（コメント） | 補足 |
| --- | --- | --- |
| Google検索に出るタイトル・説明文 | `▼▼ SEO / タイトル・説明文` | `<title>` と `description` |
| 料金（金額・プラン内容） | `▼▼ 料金を変えるときはこのセクション` | `30,000` などの数字を書き換え |
| よくある質問（Q&A） | `▼▼ Q&Aを増減するときはこのセクション` | `<details>` を増やせばQ&A追加 |
| メールアドレス | `admin@isogecall.com` を検索 | お問い合わせ欄・フッターの2か所 |
| キャッチコピー（一番上の大見出し） | `1. ファーストビュー` | `<h1>` の中 |
| 実績の数字（58% / 41% など） | `信頼バー` や `実績` | 数字を書き換え |
| 導入事例 | `6. 導入事例` | |

---

## 📨 お問い合わせフォームの通知先（Slack）

フォーム送信は **Slack の Incoming Webhook** に直接届きます（指定チャンネルに通知）。

- 通知先を変えるとき: `index.html` 内の `SLACK_WEBHOOK_URL =` の行のURLを差し替え
- セキュリティ上の注意: Webhook URL はサイトのソースから見えます。万一悪用されたら Slack 側で **Revoke → 新規発行 → 差し替え** で即無効化できます（簡易的なbot対策のhoneypotは実装済み）
- 送信内容: 会社名・お名前・メール・電話・種別・本文 が整形されて届きます

---

## 🖼 OGP画像（SNSシェア時のサムネ）の作り直し方

`assets/ogp.png`（1200×630）がSNS・検索時のサムネです。元データは `assets/og-card.html`。
文言を変えたら、ターミナルで以下を実行すると作り直せます（macOS / Chrome利用）。

```bash
cd assets
"/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" \
  --headless=new --disable-gpu --window-size=1200,630 \
  --screenshot="$(pwd)/ogp.png" "file://$(pwd)/og-card.html"
```

---

## 🎨 色を変えたいとき

`style.css` の先頭 `:root` を変えると全体に反映されます。

| 役割 | 変数 | 値 |
| --- | --- | --- |
| ブランド主色（ティール） | `--teal` | `#1f867a` |
| 濃いティール（ダーク背景） | `--teal-d` | `#14463f` |
| CTA・即時性アクセント（オレンジ） | `--orange` | `#f1851f` |
| 文字色（ネイビー） | `--ink` | `#15293b` |
| 温かみ背景（クリーム） | `--cream` | `#f8f5ec` |

---

## ファイル構成

```
isogecall-lp/
├── index.html        … LP本体（文章はほぼここ）
├── style.css         … デザイン・色・レスポンシブ
├── robots.txt        … 検索エンジン向け設定
├── sitemap.xml       … 検索エンジンへのページ一覧
├── CNAME             … 独自ドメイン設定（isogecall.com）
├── README.md         … このファイル
└── assets/
    ├── logo-round.png … ロゴ
    ├── favicon.svg    … ブラウザタブのアイコン
    ├── ogp.png        … SNSシェア用サムネ（1200×630）
    └── og-card.html   … ogp.png の元データ
```

---

## 🌐 独自ドメイン（isogecall.com）の仕組み・メモ

- `CNAME` ファイルに `isogecall.com` を記載済み（GitHub Pages 側の独自ドメイン設定）
- DNS は **Cloudflare** で管理。GitHub Pages へ向けるための推奨レコード:

| Type | Name | Content | Proxy |
| --- | --- | --- | --- |
| A | @ | 185.199.108.153 | DNSのみ（グレー雲） |
| A | @ | 185.199.109.153 | DNSのみ |
| A | @ | 185.199.110.153 | DNSのみ |
| A | @ | 185.199.111.153 | DNSのみ |
| CNAME | www | t-koza.github.io | DNSのみ |

- 設定後、GitHubの **Settings → Pages → Custom domain** が `isogecall.com` になり、`Enforce HTTPS` にチェックが入れば完了
- 反映には DNS浸透で最大数十分かかることがあります

---

## ローカルでの確認

```bash
python3 -m http.server 5173
# → http://localhost:5173
```

## ライセンス
社内利用向け。デザイン・コピーの転用はご相談ください。
