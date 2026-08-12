# 車中泊さがし

釣りの後、その場で近くの車中泊スポットを探す個人用 Web アプリ。**単一 HTML ファイル**・ビルド不要。

## 公開URL（GitHub Pages）

<https://ask-holdings.github.io/shachuhaku-spots/>

- リポジトリ: `ask-holdings/shachuhaku-spots`（main ブランチ / root 配信）
- 更新方法: `index.html` を編集して `git push` するだけ（約1分で反映）
- 自分で追加したスポットはブラウザ（localStorage）に保存されるため、**URL が固定される GitHub Pages 運用が前提**。

## ローカルで開く

GPS・保存・外部通信を使うため、ファイルの直接ダブルクリック（`file://`）では正しく動きません。httpサーバ経由で開くこと。

```bash
# Codespaces / Python がある環境
python3 -m http.server 8000
```

```powershell
# このPC（Python なし）: 同梱の簡易サーバで http://localhost:8788
powershell -NoProfile -ExecutionPolicy Bypass -File .claude\serve.ps1
```

## 構成

```
車中泊スポット/
├── CLAUDE.md            # Claude Code 用ガイド（最初に読む）
├── README.md            # このファイル
├── SPEC.md              # 詳細仕様
├── index.html           # アプリ本体
├── index_5.html         # 初期デモ（比較用・非公開/git管理外）
├── data/
│   └── spots.seed.json  # 初期データ 73 件（const SPOTS と同一内容）
└── .claude/serve.ps1    # ローカル確認用の簡易サーバ（git管理外）
```

## 主な機能

- 現在地から近い順に表示（GPS追尾モード／地図タップで基準点）。距離帯見出し（~1km/~5km/~15km/~50km）
- フィルター：トイレ・24時間・無料・温泉近く・静か（地図のピンも連動）
- 詳細：経路案内（Google マップのナビ）／地図で見る（Google マップで開きストリートビューで下見）
- 周辺のライブ検索（OpenStreetMap から道の駅・RVパーク・キャンプ場・SA/PA・休憩所を取得。墓地等は自動除外。結果は24時間キャッシュ）
- 自分のスポットの追加・編集・削除・バックアップ（クリップボード/JSONファイルの書き出し・読み込み）
- フィルター・基準点・地図サイズは保存され、開き直しても復元される

詳細は `SPEC.md` を参照。
