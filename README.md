# 宇宙戦略基金 採択結果ダッシュボード

JAXA「宇宙戦略基金」の採択機関一覧をインタラクティブに可視化する、単一HTMLファイルのダッシュボードです。**168件**の採択データを、機関種別 / 上場区分 / 宇宙SU / 新規・既存 / 分野 / 担当省 / 採択日などの切り口で確認できます。

![dashboard](https://img.shields.io/badge/built%20with-Chart.js-5b8cff) ![pages](https://img.shields.io/badge/deploy-GitHub%20Pages-3ecf8e)

## ファイル構成

| ファイル | 役割 |
| --- | --- |
| `index.html` | ダッシュボード本体（単一ファイル / 外部依存はCDNのChart.jsのみ） |
| `data.js` | 採択データ（JavaScriptで `window.SPACE_FUND_DATA` に格納） |
| `data.json` | 同じデータのJSON版（再利用・差し替え用） |
| `README.md` | 本ファイル |

## ローカルで動かす

`index.html` をブラウザで開くだけです。  
※一部ブラウザは `file://` でJSの読み込みを制限することがあるため、その場合は以下のいずれかで簡易サーバを立ててください。

```bash
# Python 3
python3 -m http.server 8000
# Node
npx serve .
```

→ ブラウザで `http://localhost:8000/` を開きます。

## GitHub Pages にアップロードする手順（最短ルート）

### 方法A: ブラウザだけで完結（推奨）

1. GitHub で新規リポジトリを作成（例: `space-fund-dashboard`、Public）
2. リポジトリ画面の「Add file」→「Upload files」で **このフォルダの中身全部**（`index.html`, `data.js`, `data.json`, `README.md`）をドラッグ＆ドロップ
3. 「Commit changes」をクリック
4. リポジトリの **Settings → Pages** を開く
5. **Source** を「Deploy from a branch」、**Branch** を `main` の `/ (root)` に設定して「Save」
6. 1〜2分後に `https://<ユーザー名>.github.io/space-fund-dashboard/` で公開されます

### 方法B: コマンドラインで

```bash
git init
git add .
git commit -m "feat: 宇宙戦略基金 採択結果ダッシュボード"
git branch -M main
git remote add origin https://github.com/<ユーザー名>/space-fund-dashboard.git
git push -u origin main
```

その後、上記の **Settings → Pages** から有効化してください。

## ダッシュボード機能

- **KPIカード**: 採択件数 / ユニーク機関数 / 民間・大学・独法の内訳 / 上場・宇宙SU・新規参入の比率
- **円グラフ**: 機関種別 / 上場区分・宇宙SU（民間企業） / 新規・既存（民間企業）
- **積み上げ棒グラフ**: 分野×上場区分 / 担当省×分野
- **時系列グラフ**: 月別採択件数（期別の積み上げ）＋ 累計の折れ線
- **クロス集計**: 分野×参画歴 / 分野×上場区分（民間企業のみ）
- **TOP15機関**: 採択件数の多い機関を上場区分カラーで可視化
- **検索＆フィルタ**: 機関名・テーマでのキーワード検索、期・機関種別・分野・担当省・上場区分・参画歴でしぼり込み
- **採択機関一覧テーブル**: 列ヘッダクリックでソート / 各案件のPDFリンク

## データの更新方法

`data.json` を最新のものに差し替えるか、`data.js` の `window.SPACE_FUND_DATA = [...]` を直接編集してください。  
列名（`実施機関名(代表機関)` `機関種別` `宇宙参画歴` `上場区分/宇宙SU` `期` `分野` `担当省` ...）はそのままにしてください。

## データ出典

- [JAXA 宇宙戦略基金](https://fund.jaxa.jp/)

## ライセンス

可視化コード（HTML/JS/CSS）はMITで自由に再利用可能です。データの著作権は出典元に帰属します。
