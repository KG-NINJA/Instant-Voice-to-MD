# Instant-Voice-to-MD

モバイルWeb向けの PTT (Push-to-Talk) アプリです。
ボタンを押している間だけ録音し、音声書き取り結果を Markdown に蓄積して `.md` ファイルとして保存できます。

## データ取り扱い（重要）

- このアプリは、**アプリ独自のサーバーへ音声・テキストを保存しません**。
- 記録データは、ブラウザ上で生成された Markdown をユーザー操作で `.md` ダウンロードする方式です。
- つまり、アプリ側にアカウント機能・クラウド保存機能・履歴同期機能はありません。
- ただし、音声認識にはブラウザ実装の `SpeechRecognition` を利用するため、認識処理の仕様は利用ブラウザに依存します。

## 主な機能

- 押下中のみ録音（`pointerdown` 開始 / `pointerup` 停止）
- `SpeechRecognition` を使った日本語書き取り（`ja-JP`）
- Markdown形式で記録
  - `- [HH:mm:ss] 書き取り本文`
- 端末へ `.md` をダウンロード保存

## 対応ブラウザ

`window.SpeechRecognition` または `window.webkitSpeechRecognition` が必要です。
未対応ブラウザでは録音ボタンが無効になり、エラーメッセージを表示します。

## 使い方

1. ページを開く
2. 「押している間だけ録音」ボタンを長押しする
3. 話し終わったらボタンを離す（録音停止）
4. 書き取り結果がプレビューに追記される
5. 「Markdownを保存」を押して `.md` を保存する

## ローカル起動

```bash
cd /home/user/voice-md-recorder
npm install
npm run dev
```

## テスト

```bash
npm test
```

## GitHub Pages 公開

このリポジトリには Pages デプロイ用 workflow を含めています。

- workflow: `.github/workflows/deploy-pages.yml`
- push 先: `main` ブランチ
- 配信元: `publishable/`（workflow内で自動生成して配信）

### 公開前のGitHub設定

1. リポジトリをGitHubへpush
2. GitHubリポジトリの `Settings > Pages` で `Build and deployment` を `GitHub Actions` に設定
3. `main` へpushすると自動デプロイ

## 公開可能ファイルをひとまとめにする

```bash
npm run publishable
```

上記で `publishable/` フォルダが生成されます。`publishable/` の中身をそのまま静的ホスティングに配置すれば公開できます。
