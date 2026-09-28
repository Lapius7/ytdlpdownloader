# ytdlpdownloader (yd)

[yt-dlp](https://github.com/yt-dlp/yt-dlp) を fzf のメニューで操作する、動画・音声・画像ダウンローダー。
URL を貼って、形式・画質・範囲・オプションを選び、確認画面を見てからダウンロードを始める。
YouTube 以外にも yt-dlp が対応するサイト（ニコニコ・X・TikTok・Instagram・Twitch など数千サイト）と、[gallery-dl](https://github.com/mikf/gallery-dl) が対応する画像サイトで使える。

## インストール

```bash
npm i -g @lapius/ytdlpdownloader     # コマンドは yd
```

[lapacks](https://github.com/Lapius7/lapacks) からも入れられる。

### 必要なもの

| | |
|-|-|
| 必須 | `zsh`、`yt-dlp`、`fzf`（0.63 以降）、`ffmpeg`、`jq` |
| あれば使う | `gallery-dl`（画像の投稿）、`chafa`（サムネイルのプレビュー）、`fd`、`eza` |

Linux・WSL で動作確認している（macOS も一応対応）。足りないものがあれば起動時に入れ方を表示する。

## 使い方

```bash
yd                      # メニューを開く
yd <URL>                # URL を渡して、動画/音声/画像を選ぶ
yd video [URL]          # 動画 (mp4 / mkv / webm)
yd audio [URL]          # 音声 (mp3 / m4a / opus / flac / wav)
yd image [URL]          # サムネイル・画像の投稿 (gallery-dl に自動で切替)
yd batch [URL...|file]  # 複数の URL をまとめて
yd history              # 保存したファイルの履歴
yd update               # yt-dlp を更新
yd --version
```

操作: ↑↓ / j k で移動、Enter で決定、Esc で戻る。ダウンロード中は Ctrl+C で中止。
URL を省くとクリップボードの URL を使う。

### オプション（Space で複数選択）

| 種類 | 選べるもの |
|-|-|
| 動画 | サムネイルの埋め込み・別保存、字幕（埋め込み・別保存・自動字幕）、チャプター、メタデータ、SponsorBlock |
| 音声 | カバー画像の埋め込み・別保存、メタデータ、チャプター、SponsorBlock |
| 画像 | 全サイズのサムネイル、gallery-dl を使う |
| 共通 | 説明文の保存、ダウンロード済みを飛ばす（アーカイブ）、速度制限、Cookie |

選んだオプションは種類ごとに記憶され、次回の初期値になる。
設定後に確認画面（タイトル・形式・範囲・オプション・保存先）が出て、そこから各項目を直したり、実行するコマンドをコピーしたりできる。

### ログインが必要なサイト

オプションの「Cookie」または失敗時のメニューから、`cookies.txt` のファイルかブラウザ（Firefox・Chrome など）を選ぶ。
WSL では Windows 側の Chrome/Edge の Cookie は読めないので、Firefox のプロファイルか `cookies.txt` を使う。

## ファイル

- 設定・履歴・アーカイブ: `~/.config/yd/`
- ログ: `~/.yd_logs/`
- 一時ファイル: `~/.cache/yd/`

## リリース

`v*` タグを push すると GitHub Actions（`.github/workflows/release.yml`）が `npm/build.mjs` で npm に公開する（Trusted Publisher で認証するのでトークンは不要）。手元での確認は `node npm/build.mjs 0.0.0-dev --pack`。

## ライセンス

MIT
