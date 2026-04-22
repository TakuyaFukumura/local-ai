# local-ai

ローカル環境でAIを動かす環境構築用リポジトリ。  
Docker を使って [Ollama](https://ollama.com/) と [Open WebUI](https://github.com/open-webui/open-webui) を起動します。

---

## 構成

| サービス       | 説明         | URL                    |
|------------|------------|------------------------|
| Ollama     | LLM 実行エンジン | http://localhost:11434 |
| Open WebUI | チャット UI    | http://localhost:3000  |

---

## 前提条件

- [Docker](https://docs.docker.com/get-docker/) および [Docker Compose](https://docs.docker.com/compose/install/) がインストールされていること

---

## 起動方法

```bash
docker compose up -d
```

起動すると `ollama-model-init` コンテナが自動で `qwen3.5:0.8b` モデルを取得します（初回は数分かかります）。

---

## Open WebUI の使い方

1. ブラウザで http://localhost:3000 を開く
2. 初回アクセス時にアカウントを作成してログイン
3. 画面上部のモデル選択から `qwen3.5:0.8b` を選択してチャット開始

---

## 停止方法

```bash
docker compose down
```

データ（モデルやチャット履歴）を含めて完全に削除する場合は以下を実行します。

```bash
docker compose down -v
```

---

## その他の Ollama コマンド

```bash
# 取得済みモデルの一覧表示
docker exec -it ollama ollama list

# モデルの削除
docker exec -it ollama ollama rm qwen3.5:0.8b
```
