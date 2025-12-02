# コンテナ × AI 推論環境 入門  
〜 LiteLLMで社内AIゲートウェイを構築する 〜

---

## 1. 今日のゴール

- AI推論環境の内部構造を理解する  
- コンテナ環境の構造理解  
- LiteLLMの役割を理解する  
- Redis / Postgresの用途を理解する  
- AIを社内インフラとして扱う視点を持つ  

---

## 2. 技術的なコンテナ環境の説明（重要）

### ● コンテナの特徴

::contentReference[oaicite:0]{index=0}


- ホストOS（カーネル）を共有  
- プロセス分離（namespace）  
- リソース制御（cgroups）  
- 軽い、起動が速い、複製しやすい  
- イミュータブル（変更不可）な実行環境  
- 依存関係の差異がない  

---

### ● VMとコンテナの違い（本質）

::contentReference[oaicite:1]{index=1}


| 項目 | VM | コンテナ |
|---|---|---|
| OS | 仮想化 (ゲストOS) | 共有 (ホストOS) |
| 起動時間 | 数十秒〜数分 | 数百ms〜数秒 |
| CPU / メモリ | 多く消費 | 軽量 |
| 配布 | 重い | 軽量（MB〜GB） |
| 一貫性 | OSごと差異 | 依存関係が固定 |
| スケール | 台数単位 | コンテナ単位 |

---

### ● コンテナ内部の実態（Linux機能）

::contentReference[oaicite:2]{index=2}


---

### ● AI推論とコンテナが相性良い理由

- 依存ライブラリが重い（OpenAI / AWS / Azure SDK）  
- Python & Node の環境差異を排除  
- GPU & CPU の切り替えも簡単  
- 同一環境の複製が容易  
- モデルごとにコンテナ分離できる  

---

### ● 今回のコンテナ構成例

+-------------------------+
| Azure VM | (OS: Ubuntu 22)
| ┌───────────────┐
| │ litellm │ port:4000
| ├───────────────┤
| │ redis │ port:6379
| ├───────────────┤
| │ postgres │ port:5432
| └───────────────┘
+-------------------------+


---

### ● コンテナ間通信（DNS）

litellm → redis:6379
litellm → postgres:5432


ホストIP不要  
Docker内部ネットワークで通信  

---

# 🔧 デモ編（Azure VM上で）

## 3. LiteLLM を起動

docker run -d -p 4000:4000
-e AZURE_API_KEY=$AZURE_API_KEY
-e AZURE_API_BASE=$AZURE_API_BASE
ghcr.io/berriai/litellm:main-stable


---

## 4. モデルに問い合わせる

curl -X POST "http://<VM_IP>:4000/v1/chat/completions"
-H "Content-Type: application/json"
-d '{
"model": "gpt-4o",
"messages": [{"role":"user","content":"DockerとVMの違いは？"}]
}'


---

## 5. LiteLLMによる実務上の利点

- AIを社内API化  
- モデル横断アクセス  
- 使用ログが完全記録  
- 課金管理  
- モデル交換時にクライアント変更不要  

---

## 6. Redisによりレイテンシ改善

- キャッシュによる高速応答  
- 同一質問は即答  
- 課金削減  

---

## 7. Postgresにより透明性確保

- 誰が  
- いつ  
- どのモデルに  
- 何回問い合わせたか  
- コストは？  
- レスポンス時間は？  

---

#  まとめ

✔ AI推論環境は複数コンポーネントで構成される
✔ コンテナは OS 非依存で軽量な分離実行環境
✔ LiteLLM が AIの共通ゲートウェイとして機能
✔ コンテナ化で再現性と拡張性を実現
✔ AIを社内基盤として運用できる

