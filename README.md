# local-ai

ローカル環境でAIを動かす環境構築用リポジトリ。  
Docker を使って [Ollama](https://ollama.com/) と [Open WebUI](https://github.com/open-webui/open-webui) を起動します。

---

## 構成

| サービス | 説明 | URL |
|---|---|---|
| Ollama | LLM 実行エンジン | http://localhost:11434 |
| Open WebUI | チャット UI | http://localhost:3000 |

---

## 前提条件

- [Docker](https://docs.docker.com/get-docker/) および [Docker Compose](https://docs.docker.com/compose/install/) がインストールされていること

GPU を使用する場合は追加で以下が必要です。

- NVIDIA GPU および最新ドライバー
- [NVIDIA Container Toolkit](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/install-guide.html)

---

## 起動方法

### CPU のみで起動する場合

```bash
docker compose up -d
```

### NVIDIA GPU を使用して起動する場合

```bash
docker compose -f docker-compose.yml -f docker-compose.gpu.yml up -d
```

---

## モデルのインストール

コンテナ起動後、以下のコマンドで Gemma 4 E2B モデルを取得します。

```bash
docker exec -it ollama ollama pull gemma4:e2b
```

モデルが取得できたら、動作確認として CLI からも実行できます。

```bash
docker exec -it ollama ollama run gemma4:e2b
```

---

## Open WebUI の使い方

1. ブラウザで http://localhost:3000 を開く
2. 初回アクセス時にアカウントを作成してログイン
3. 画面上部のモデル選択から `gemma4:e2b` を選択してチャット開始

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
docker exec -it ollama ollama rm gemma4:e2b
```
