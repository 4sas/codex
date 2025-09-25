<h1 align="center">OpenAI Codex CLI</h1>

<p align="center"><code>npm i -g @openai/codex</code><br />または <code>brew install codex</code></p>

<p align="center"><strong>Codex CLI</strong> は、あなたのローカルPC上で動作する OpenAI のコーディングエージェントです。
</br>
</br>コードエディタ（VS Code / Cursor / Windsurf）で Codex を使いたい場合は、<a href="https://developers.openai.com/codex/ide">IDE にインストール</a>してください。
</br>OpenAI の<em>クラウド型エージェント</em>である <strong>Codex Web</strong> をお探しの場合は、<a href="https://chatgpt.com/codex">chatgpt.com/codex</a> へ。</p>

<p align="center">
  <img src="./.github/codex-cli-splash.png" alt="Codex CLI スプラッシュ" width="80%" />
  </p>

---

## クイックスタート

### mcp-proxy のインストール

リモートの MCP サーバに接続するためのツールをインストール。
uv を使う場合:

```shell
uv tool install mcp-proxy
```

pipx を使う場合:

```shell
pipx install mcp-proxy
```

Homebrew を使う場合:

```shell
brew install mcp-proxy
```

### Codex CLI のインストールと実行

お好みのパッケージマネージャでグローバルにインストールします。  
npm を使う場合:

```shell
npm install -g @openai/codex
```

Homebrew を使う場合:

```shell
brew install codex
```

その後、`codex` を実行するだけで開始できます:

```shell
codex
```

<details>
<summary><a href="https://github.com/openai/codex/releases/latest">最新の GitHub リリース</a>から、あなたの環境に合うバイナリを直接ダウンロードすることもできます。</summary>

各 GitHub リリースには複数の実行ファイルが含まれますが、一般的には次のいずれかになります。

- macOS
  - Apple Silicon/arm64: `codex-aarch64-apple-darwin.tar.gz`
  - x86_64（旧型の Mac ハードウェア）: `codex-x86_64-apple-darwin.tar.gz`
- Linux
  - x86_64: `codex-x86_64-unknown-linux-musl.tar.gz`
  - arm64: `codex-aarch64-unknown-linux-musl.tar.gz`

各アーカイブには、プラットフォーム名を含む単一の実行ファイル（例: `codex-x86_64-unknown-linux-musl`）が入っています。展開後は `codex` にリネームするとよいでしょう。
</details>

### ChatGPT プランで Codex を使う

<p align="center">
  <img src="./.github/codex-cli-login.png" alt="Codex CLI ログイン" width="80%" />
  </p>

`codex` を起動し、**Sign in with ChatGPT**（ChatGPT でサインイン）を選択します。Plus / Pro / Team / Edu / Enterprise のいずれかの ChatGPT プランで Codex を利用することを推奨します。［<a href="https://help.openai.com/en/articles/11369540-codex-in-chatgpt">ChatGPT プランに含まれる内容の詳細</a>］

API キーでも Codex を利用できますが、[追加の設定](./docs/authentication.md#usage-based-billing-alternative-use-an-openai-api-key)が必要です。従量課金の API キーを以前に使っていた場合は、[移行手順](./docs/authentication.md#migrating-from-usage-based-billing-api-key)を参照してください。ログインで問題がある場合は、[この Issue](https://github.com/openai/codex/issues/1243) にコメントしてください。

### ログイン

`codex login` を実行するか、初回に `codex` を起動すると **Sign in with ChatGPT** の案内が出ます。Enter を押すと既定のブラウザで認証ページが開き、サインイン後に CLI へ戻ります（Plus/Pro/Team などのプランに含まれる利用枠で使えます）。 :contentReference[oaicite:0]{index=0}

ヘッドレス環境や SSH/WSL2 では、ターミナルに表示された URL をコピーして手動でブラウザに貼り付けて認証します。Windows 環境で `python3` が見つからず内部サーバーが起動しない場合は、`python.exe` へのシンボリックリンクを `python3.exe` 名で作成すると解決することがあります（例：PowerShell）。 :contentReference[oaicite:1]{index=1}

```powershell
New-Item -ItemType SymbolicLink `
  -Path "C:\Users\<YOUR_USER>\AppData\Local\Programs\Python\Python39\python3.exe" `
  -Target "C:\Users\<YOUR_USER>\AppData\Local\Programs\Python\Python39\python.exe"
```

### 日本語で話してもらう

Codex の応答を常に日本語にするには、`~/.codex/AGENTS.md` にプロンプトを追記します（この内容は毎回の会話に内部追加されます）。 :contentReference[oaicite:0]{index=0}

```bash
echo 'Please provide all answers in Japanese' >> ~/.codex/AGENTS.md
````

設定後の確認例（非対話で1ターン実行）:

```bash
codex exec hello
# → 「こんにちは！今日は何をお手伝いできますか？」のように日本語で応答します
```

### Model Context Protocol (MCP)

Codex CLI は [MCP サーバー](./docs/advanced.md#model-context-protocol-mcp)をサポートします。`~/.codex/config.toml` に `mcp_servers` セクションを追加して有効化します。

### 設定

Codex CLI は豊富な設定項目をサポートし、設定は `~/.codex/config.toml` に保存されます。全オプションは [Configuration](./docs/config.md) を参照してください。

---

### ドキュメント & FAQ

- [**はじめに**](./docs/getting-started.md)
  - [CLI の使い方](./docs/getting-started.md#cli-usage)
  - [プロンプトを入力にして実行](./docs/getting-started.md#running-with-a-prompt-as-input)
  - [プロンプト例](./docs/getting-started.md#example-prompts)
  - [AGENTS.md を用いたメモリ](./docs/getting-started.md#memory-with-agentsmd)
  - [設定](./docs/config.md)
- [**サンドボックス & 承認フロー**](./docs/sandbox.md)
- [**認証**](./docs/authentication.md)
  - [認証方法](./docs/authentication.md#forcing-a-specific-auth-method-advanced)
  - [ヘッドレス環境でのログイン](./docs/authentication.md#connecting-on-a-headless-machine)
- [**高度な使い方**](./docs/advanced.md)
  - [非対話 / CI モード](./docs/advanced.md#non-interactive--ci-mode)
  - [トレーシング / 詳細ログ](./docs/advanced.md#tracing--verbose-logging)
  - [Model Context Protocol (MCP)](./docs/advanced.md#model-context-protocol-mcp)
- [**ゼロデータ保持（ZDR）**](./docs/zdr.md)
- [**コントリビュート**](./docs/contributing.md)
- [**インストール & ビルド**](./docs/install.md)
  - [システム要件](./docs/install.md#system-requirements)
  - [DotSlash](./docs/install.md#dotslash)
  - [ソースからビルド](./docs/install.md#build-from-source)
- [**FAQ**](./docs/faq.md)
- [**オープンソース基金**](./docs/open-source-fund.md)

---

## ライセンス

このリポジトリは [Apache-2.0 License](LICENSE) の下で提供されています。
