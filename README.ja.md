<div align="center">

<p align="center"><a href="README.md">English</a> | <b>日本語</b></p>

<h1 align="center">yt-dlp Downloader</h1>

<h3 align="center">fzf のメニューで、動画・音声・画像をダウンロードする。</h3>

<p align="center"><a href="https://github.com/yt-dlp/yt-dlp">yt-dlp</a> を fzf のメニューで操作するランチャー（コマンド <code>yd</code>）です。URL を貼って、形式・画質・範囲・オプションを選び、確認画面を見てからダウンロードを始めます。</p>

<p align="center">
  <a href="https://www.npmjs.com/package/@lapius/ytdlpdownloader"><img alt="npm" src="https://img.shields.io/npm/v/@lapius/ytdlpdownloader?style=flat-square&color=cb3837&logo=npm"></a>
  <a href="https://github.com/Lapius7/ytdlpdownloader/actions/workflows/release.yml"><img alt="Release workflow" src="https://img.shields.io/github/actions/workflow/status/Lapius7/ytdlpdownloader/release.yml?label=release&style=flat-square&logo=githubactions&logoColor=white"></a>
  <a href="LICENSE"><img alt="License" src="https://img.shields.io/github/license/Lapius7/ytdlpdownloader?style=flat-square&color=97ca00"></a>
  <a href="https://github.com/Lapius7/ytdlpdownloader/stargazers"><img alt="Stars" src="https://img.shields.io/github/stars/Lapius7/ytdlpdownloader?style=flat-square&color=e3b341&logo=github"></a>
  <a href="https://github.com/Lapius7/ytdlpdownloader/commits/main"><img alt="Last commit" src="https://img.shields.io/github/last-commit/Lapius7/ytdlpdownloader?style=flat-square&color=3b82f6"></a>
</p>

<p align="center">
  <a href="#クイックスタート">クイックスタート</a> ·
  <a href="#使い方">使い方</a> ·
  <a href="#必要なもの">必要なもの</a> ·
  <a href="#リリース">リリース</a>
</p>

</div>

## 概要

YouTube 以外にも、yt-dlp が対応するサイト（ニコニコ・X・TikTok・Instagram・Twitch など数千サイト）と、[gallery-dl](https://github.com/mikf/gallery-dl) が対応する画像サイトで使えます。

## クイックスタート

```bash
pnpm add -g @lapius/ytdlpdownloader     # コマンドは yd
```

[lapacks](https://github.com/Lapius7/lapacks) からも入れられます。入れたら `yd` を実行します。

### 必要なもの

| | |
|-|-|
| 必須 | `zsh`、`yt-dlp`、`fzf`（0.63 以降）、`ffmpeg`、`jq` |
| あれば使う | `gallery-dl`（画像の投稿）、`chafa`（サムネイルのプレビュー）、`fd`、`eza` |

Linux・WSL で動作確認しています（macOS も一応対応していますが、この README 作成時には未検証です）。足りないものがあれば、起動時に入れ方を表示します。

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

操作: ↑↓ / j k で移動、Enter で決定、Esc で戻る。ダウンロード中は Ctrl+C で中止します。URL を省くとクリップボードの URL を使います。

### オプション（Space で複数選択）

| 種類 | 選べるもの |
|-|-|
| 動画 | サムネイルの埋め込み・別保存、字幕（埋め込み・別保存・自動字幕）、チャプター、メタデータ、SponsorBlock |
| 音声 | カバー画像の埋め込み・別保存、メタデータ、チャプター、SponsorBlock |
| 画像 | 全サイズのサムネイル、gallery-dl を使う |
| 共通 | 説明文の保存、ダウンロード済みを飛ばす（アーカイブ）、速度制限、Cookie |

選んだオプションは種類ごとに記憶され、次回の初期値になります。設定後に確認画面（タイトル・形式・範囲・オプション・保存先）が出て、そこから各項目を直したり、実行するコマンドをコピーしたりできます。

### ログインが必要なサイト

オプションの「Cookie」または失敗時のメニューから、`cookies.txt` のファイルかブラウザ（Firefox・Chrome など）を選びます。WSL では Windows 側の Chrome/Edge の Cookie は読めないので、Firefox のプロファイルか `cookies.txt` を使います。

## ファイル

- 設定・履歴・アーカイブ: `~/.config/yd/`
- ログ: `~/.yd_logs/`
- 一時ファイル: `~/.cache/yd/`

## リリース

`v*` タグを push すると GitHub Actions（`.github/workflows/release.yml`）が `npm/build.mjs` で npm に公開します（Trusted Publisher で認証するのでトークンは不要）。手元での確認は `node npm/build.mjs 0.0.0-dev --pack` です。

> [!NOTE]
> README の画像はメニューの文字から描いたもので、`yd` のスクリーンショットではありません。ここに書いた動作は従来の README から引き継いだもので、今回の作り直しでは再実行していません。

## ライセンス

[MIT](LICENSE)
