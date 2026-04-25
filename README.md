# IdeaRequirementsFacilitator

粗いアイディアや既存リポジトリを、README要求定義へ整理するための VS Code / GitHub Copilot カスタムエージェントとプロンプト集です。

まだ仕様にしきれていない相談を、小さなMVP、非対象、未決質問、次のアクションへ分けて扱います。READMEは要求定義として使える文書であり、`/idea-kickoff` の初回出力は草案でもかまいません。対象リポジトリに実装や運用手順がある場合は、その使い方も同じ文書にまとめます。必要に応じて、READMEや関連Markdownの草案作成・更新まで行います。

## このリポジトリが解決すること

アイディア相談では、価値仮説、対象ユーザー、実装案、制約、調査事項が混ざりやすくなります。IdeaRequirementsFacilitator は次の問いに答えることを目的とします。

> このアイディアは、誰のどんな課題を、最初にどこまで解くべきか

そのうえで、READMEやIssueへ転用しやすい形で、要約、MVP、非対象、リスク、未決事項を整理します。

## 想定ユーザー

- 新しいツール、アプリ、ライブラリ、業務支援のアイディアをREADME要求定義へ落としたい個人開発者
- 実装前にREADME相当の要求定義を短く固めたい人
- 既存リポジトリのREADMEを、目的と使い方が伝わる文書へ整えたい人
- Copilot Chat のカスタムエージェントやプロンプトをチームで共有したい人

大規模な要件定義プロセス、網羅的な仕様書、プロジェクト管理体系の置き換えは主目的ではありません。

## 何を出力するか

- README形式の要求定義草案
- アイディアの要約
- 解くべき課題と、まだ仮説に過ぎない点
- 想定ユーザーと主要ユースケース
- 実現方法の選択肢とトレードオフ
- 最小MVPと非対象
- 調査が必要な論点
- 次に確認すべき質問
- READMEへ転用できる見出し案
- 既存リポジトリ向けのREADME本文
- READMEや関連Markdownへのファイル更新

## 何をしないか

- ユーザーの意思決定なしにスコープを広げること
- 未確認の前提を事実としてREADMEへ書くこと
- 実装コマンド、CLI、API、設定ファイルを調査せずに捏造すること
- 未確認の前提を断定したままファイルへ反映すること

## リポジトリ内容

| パス | 役割 |
| --- | --- |
| [.github/instructions/readme-requirements.instructions.md](.github/instructions/readme-requirements.instructions.md) | README要求定義の章立てと判断基準の正本 |
| [.github/agents/idea-requirements-facilitator.agent.md](.github/agents/idea-requirements-facilitator.agent.md) | README要求定義をユーザーと詰め、草案作成・更新を担当するカスタムエージェント |
| [.github/prompts/idea-kickoff.prompt.md](.github/prompts/idea-kickoff.prompt.md) | `/idea-kickoff` で新しいアイディアから `README.md` の草案を作成する prompt |
| [.github/prompts/readme-from-repository.prompt.md](.github/prompts/readme-from-repository.prompt.md) | `/readme-from-repository` でGitHubリポジトリURLからREADMEを作成または更新する prompt |

## 使い方の概観

1. このリポジトリを VS Code で開くか、利用したいリポジトリへ `.github/` をコピーします。
2. 新しいアイディアから始める場合は、Copilot Chat で `/idea-kickoff` を実行し、背景、目的、想定ユーザー、制約、不明点を入力します。
3. 作成された `README.md` を `idea-requirements-facilitator` と一緒に詰め、README要求定義として使える状態へ近づけます。
4. 既存リポジトリからREADMEを作る場合は、対象リポジトリで `/readme-from-repository` を実行し、引数にGitHubリポジトリURLを渡します。

## 前提環境

- VS Code
- GitHub Copilot Chat
- VS Code の prompt files と custom agents を利用できる環境

Web調査が必要な相談では、Copilot Chat からWeb取得ツールを使える環境があると精度が上がります。Web調査が使えない場合でも、リポジトリ内のREADME、docs、設定ファイル、ソースコードをもとに整理できます。

## 最短手順

既存リポジトリでこのテンプレートを使う場合の最短手順です。

```sh
# 1. 対象リポジトリへ移動
cd /path/to/target-repository

# 2. このリポジトリの .github を対象リポジトリへコピー
cp -R /path/to/IdeaRequirementsFacilitator/.github ./.github
```

その後、VS Code で対象リポジトリを開き、Copilot Chat から次のいずれかを実行します。

- `/idea-kickoff`: 新しいアイディアから `README.md` の要求定義草案を作成する
- `/readme-from-repository <GitHubリポジトリURL>`: 既存リポジトリを読み取り、READMEを作成または更新する

## READMEテンプレート

このリポジトリで推奨するREADMEは、要求定義と対象リポジトリの使い方を同じ流れで読める構成にします。正本は [.github/instructions/readme-requirements.instructions.md](.github/instructions/readme-requirements.instructions.md) です。実装済みのツールやライブラリでは「前提環境」「最短手順」「コマンド一覧」を具体化し、アイディア段階のリポジトリでは「何を解くか」「何をしないか」「次に決めること」を厚めにします。

```markdown
# <リポジトリ名>

<誰のどんな課題を解くリポジトリかを1から2文で書く>

## このリポジトリが解決すること

## 想定ユーザー

## 何を提供するか

## 何をしないか

## 使い方の概観

## 前提環境

## 最短手順

## リポジトリ構成

## 既知の制約

## ロードマップ

## ライセンス
```

## 既知の制約

- prompt files と custom agents の読み込み挙動は VS Code / Copilot Chat のバージョンに依存します。
- ファシリテーターは調査と整理を支援しますが、最終的なスコープ判断はユーザーが行います。
- 既存リポジトリからREADMEを作る場合、ソースや設定から確認できない利用手順は `未確認` として残します。

## 再現性の考え方

- README要求定義の章立てと判断基準は [.github/instructions/readme-requirements.instructions.md](.github/instructions/readme-requirements.instructions.md) を正本にします。
- `/idea-kickoff` と `/readme-from-repository` は同じ正本テンプレートを参照するため、入口が違っても成果物の構造は揃います。
- 未確認事項は推測で埋めず、README内に `未確認:` または `要確認:` として残します。
- 既存リポジトリの使い方は、README、docs、設定ファイル、主要ソース、テスト、スクリプトから確認できた内容だけを反映します。

## ロードマップ

初期構成として予定していたカスタムエージェント、プロンプト、README要求定義テンプレートは作成済みです。現時点で追加予定の機能はありません。

## ライセンス

本ソフトウェアは BSD-3-Clause で配布します。詳細は [LICENSE](LICENSE) を参照してください。
