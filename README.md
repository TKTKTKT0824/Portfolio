# Portfolio

このリポジトリは、静的サイトジェネレーターの Zensical を利用して構築されたポートフォリオサイトのソースコードを管理しています。

## ローカル環境での開発 (Zensical)

パッケージ管理には `uv` を使用しています。あらかじめ [uv](https://github.com/astral-sh/uv) がインストールされていることを確認してください。

### ローカルサーバーの起動
以下のコマンドを実行するとローカル開発用サーバーが起動し、プレビューを確認できます。
```bash
uv run zensical serve
```

### ビルド
本番用の静的ファイルを生成する場合は、以下のコマンドを実行します。生成されたファイルは `site/` ディレクトリに出力されます。
```bash
uv run zensical build
```

### 主なディレクトリ・ファイル構成
- `docs/` : サイトのコンテンツとなる Markdown ファイルやアセットが格納されています。
- `zensical.toml` : Zensical のサイト設定やメタデータが記述されている設定ファイルです。
- `site/` : ビルドによって出力された静的ファイル群が格納されます。


## 自動デプロイについて

GitHub Actions を利用し、**毎朝 5:00 (JST)** に実行されるスケジュールジョブが設定されています。
`main` ブランチにおいて、過去24時間以内に新しいコミットが追加されている（未デプロイのコミットがある）場合のみ、Cloudflare Pages のデプロイフックを叩いて自動デプロイを行います。

### 必要な設定

この自動デプロイを機能させるには、GitHub のリポジトリシークレットに Cloudflare Pages のデプロイフック URL を設定する必要があります。

1. Cloudflare のダッシュボードから、対象の Pages プロジェクトのページを開きます。
2. 「Settings (設定)」 > 「Builds & deployments (ビルドとデプロイ)」 > 「Deploy hooks (デプロイフック)」の順に進み、新しいフックを作成して URL をコピーします。
3. この GitHub リポジトリの「Settings」 > 「Secrets and variables」 > 「Actions」を開きます。
4. 「New repository secret」をクリックし、以下の内容で保存します：
   - Name: `CLOUDFLARE_PAGES_DEPLOY_HOOK`
   - Secret: 先ほどコピーしたデプロイフックの URL

## License

本リポジトリ内のソースコード（GitHub Actionsの設定等）は [MIT License](./LICENSE) の元で公開されています。
ただし、`docs/` ディレクトリ配下に含まれる個人的なコンテンツ（経歴、文章、および写真等のメディアファイル）の著作権は制作者本人に帰属し、これらの無断転載・再利用を禁止します。
