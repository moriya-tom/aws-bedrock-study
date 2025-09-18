# AWS Bedrockとは？

## その前に生成AIについて改めて
- 2022年11月にOpenAI社からChatGPTが発表され、生成AIという言葉が話題になる。
- 名前の通り様々なコンテンツを生成できるAIの総称。メディアで使われだした言葉で厳密な定義はない。

## 代表的な製品
- テキスト生成:ChatGPT
- 画像生成:Stable Diffusion
- コード生成:GitHub Copilot

## 生成AIのモデルとは？
- 基板モデル:大量のデータでトレーニングされた汎用的なモデル
- 大規模言語モデル(LLM):言語ベースの処理を汎用的にこなすモデル
- 
## Amazon Bedrockの概要
Amazonが提供する生成AIサービス複数のAIモデルをAPIで簡単に利用できる。
生成AIモデルのAPIとは?
開発者が生成AIモデルを自身のアプリケーションから呼び出す手段
クラウド上で主に提供されている生成AIモデルのAPI
- MicroSoft Azure:Azure OpenAI Service
- Google Cloud:Vertex AI
- Oracle Cloud:OCI Generative AI

## 特徴
- Claude, Titan, Llama 2などのモデルを選択可能(API経由で手軽に利用できる)
- セキュアなAWS環境で動作
- サーバーレスでスケーラブル

## Claud Opusについて
- images/Designer.png

## 利用料金
- オンデマンド(従量課金)
- プロビジョンドスループット(事前購入)

## 活用例
- チャットボット
- 自動要約
- コード生成

## 使い方
1. AWSアカウント作成
2. Bedrockコンソールにアクセス
3. モデルを有効化してAPIを呼び出す
