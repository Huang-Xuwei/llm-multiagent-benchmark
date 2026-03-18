# MPE マルチエージェント ベンチマーク 🎮🤖

PettingZoo MPE 環境に基づくマルチエージェント強化学習ベンチマークスイート。LLM API 駆動のエージェント意思決定が統合されています。

[![Python](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)
[![PettingZoo](https://img.shields.io/badge/PettingZoo-MPE-green.svg)](https://pettingzoo.farama.org/)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)

🌐 **利用可能な言語**: [English](README_en.md) | [中文](README_zh.md) | [日本語](README_ja.md) | [Tiếng Việt](README_vi.md)

---

## 🌟 プロジェクトのハイライト

- 🎯 **9つの古典的な環境**: 協力、対抗、通信などの様々なシナリオに対応
- 🤖 **LLM統合**: OpenAI、DeepSeek、Qwen、Gemini に対応
- 📊 **標準化解析**: 生の観測値を LLM フレンドリーな JSON 形式に変換
- 📝 **充実したドキュメント**: クイックスタートから高度な開発までの完全なガイド
- 🔧 **モジュール設計**: 拡張とカスタマイズが容易

## 📁 プロジェクト構成

```
MPE_muiltiagent_benchmark/
├── 📄 設定ファイル
│   ├── requirements.txt          # Python 依存関係
│   ├── requirements.lock         # 再現性のためのピン版
│   ├── pyproject.toml           # プロジェクト設定
│   ├── .env.example             # API キーテンプレート
│   └── .gitignore               # Git 無視ルール
│
├── 📚 ドキュメント (docs/)
│   ├── README.md                # ドキュメント ハブ
│   ├── getting_started/         # スタートガイド
│   │   ├── quickstart.md        # ⭐ クイックスタート
│   │   ├── environment_setup.md # 環境セットアップ
│   │   ├── dependency_management.md # 依存関係管理
│   │   └── overview.md          # プロジェクト概要
│   ├── configuration/           # 設定ガイド
│   │   └── api_keys.md          # 🔑 API キー管理
│   ├── architecture/            # アーキテクチャ
│   │   ├── observation_space.md # 観測解析
│   │   ├── logging_system.md    # 📊 ロギング システム
│   │   └── models.md            # 🤖 モデル使用法
│   ├── experiments/             # 実験ガイド
│   │   ├── reproducibility.md   # 🎲 再現性確保
│   │   ├── running_benchmarks.md # ベンチマーク実行
│   │   └── benchmark_review.md  # 📈 ベンチマーク分析
│   └── dev_notes/               # 開発者ノート
│       ├── work_summary.md      # 作業概要
│       ├── workflow_standardization.md # ワークフロー標準化
│       └── api_keys_refactor.md # API キー移行ログ
│
├── 🎮 環境実装 (9つの完全なゲーム)
│   ├── spread_API.py            # Simple Spread
│   ├── adv_API.py               # Simple Adversary
│   ├── tag_API.py               # Simple Tag
│   ├── push.py                  # Simple Push
│   ├── crypto.py                # Simple Crypto
│   ├── reference.py             # Simple Reference
│   ├── speaker_listener.py      # Simple Speaker Listener
│   ├── world_comm.py            # Simple World Comm
│   ├── simple.py                # Simple (Basic)
│   └── utils_api.py             # 統合 LLM API インターフェース
│
├── 🧪 テスト & ツール
│   ├── benchmark_runner.py      # ✅ バッチテストフレームワーク
│   ├── setup_api_keys.py        # ✅ API キー設定スクリプト
│   ├── verify_environment.py    # ✅ 環境検証
│   └── test_unified_api.py      # API テスト
│
├── 🔍 観測解析 (obs/)
│   ├── parse_*_obs.py           # 9つの環境パーサー
│   └── utils.py                 # 共通ユーティリティ関数
│
├── 💬 プロンプト エンジニアリング (prompt/)
│   └── prompt_for_*.py          # 標準化プロンプト モジュール
│
└── 📊 結果出力 (results/)
    └── benchmarks/<env>/        # 環境ごとのテスト結果
        ├── *.mp4                # ビデオ記録
        └── *.json               # 詳細ログ
```

## 🚀 クイックスタート

### システム要件

- **Python**: 3.8+ (推奨: 3.12.3、テスト済み)
- **オペレーティング システム**: Linux / macOS / Windows
- **依存関係管理**: pip / conda / uv

### 1. 依存関係をインストール

```bash
# リポジトリのクローン
git clone https://github.com/HuangShengZeBlueSky/MPE_muiltiagent_benchmark.git
cd MPE_muiltiagent_benchmark

# オプション A: venv を使用 (推奨)
python -m venv .venv
source .venv/bin/activate  # Linux/macOS
# .venv\Scripts\activate   # Windows
pip install -r requirements.txt

# オプション B: conda を使用
conda create -n mpe-bench python=3.12
conda activate mpe-bench
pip install -r requirements.txt

# オプション C: 直接インストール (非推奨)
pip install -r requirements.txt
```

**インストール検証**:
```bash
# 環境検証スクリプトを実行
python verify_environment.py
# ✅ すべてのチェックが通ればセットアップ成功
```

**📖 詳細ガイド**: [docs/getting_started/environment_setup.md](docs/getting_started/environment_setup.md) を参照

### 2. API キーを設定 🔑

#### 方法 A: インタラクティブ設定 (推奨)
```bash
python setup_api_keys.py
```

#### 方法 B: 手動設定
```bash
# テンプレートをコピーして編集
cp .env.example .env
nano .env  # API キーを追加
```

#### 方法 C: 環境変数
```bash
export QWEN_API_KEY="sk-your-key"
export DEEPSEEK_API_KEY="sk-your-key"
export OPENAI_API_KEY="sk-your-key"
```

**API キーを取得**:
- Qwen (推奨): https://dashscope.console.aliyun.com
- DeepSeek: https://platform.deepseek.com
- OpenAI: https://platform.openai.com/api-keys
- Gemini: https://aistudio.google.com/apikey

**📖 詳細設定**: [docs/configuration/api_keys.md](docs/configuration/api_keys.md) を参照

### 3. テストを実行

#### 単一環境テスト
```bash
# 単一ゲームを実行 (デフォルトで Qwen API を使用)
python adv_API.py
python spread_API.py
python tag_API.py
```

#### バッチ ベンチマーク テスト (推奨)
```bash
# 10 エピソード Adversary テストを実行 (シード 1-10)
python benchmark_runner.py

# カスタム環境とエピソード数
python -c "from benchmark_runner import run_benchmark; run_benchmark(env_name='spread', provider='qwen', episodes=20, seed_start=1)"
```

**出力**: ビデオ (`*.mp4`) とログ (`*.json`) が自動的に `results/benchmarks/<env>/` に保存されます

**📖 詳細ガイド**: [docs/getting_started/quickstart.md](docs/getting_started/quickstart.md)

## 📚 ドキュメント ガイド

**完全なドキュメント インデックス**: [docs/README.md](docs/README.md) 📖

### 🚀 はじめに
- [クイック スタート](docs/getting_started/quickstart.md) - 5 分で実行開始
- [環境セットアップ](docs/getting_started/environment_setup.md) - 詳細なセットアップ ガイド
- [依存関係管理](docs/getting_started/dependency_management.md) - requirements.txt vs requirements.lock
- [プロジェクト概要](docs/getting_started/overview.md) - プロジェクト アーキテクチャ

### ⚙️ 設定
- [API キー設定](docs/configuration/api_keys.md) - セキュアな API キー管理

### 🏗️ アーキテクチャ
- [観測空間](docs/architecture/observation_space.md) - 解析開発
- [ロギング システム](docs/architecture/logging_system.md) - ログ形式仕様
- [モデル使用ガイド](docs/architecture/models.md) - サポートされている LLM

### 🧪 実験
- [再現可能な実験](docs/experiments/reproducibility.md) - シード固定ガイド
- [ベンチマーク実行](docs/experiments/running_benchmarks.md) - バッチ テスト ワークフロー
- [ベンチマーク評価](docs/experiments/benchmark_review.md) - マルチロール ログ分析

### 🛠️ 開発者ノート
- [作業概要](docs/dev_notes/work_summary.md) - v1.0 開発履歴
- [ワークフロー標準化](docs/dev_notes/workflow_standardization.md) - 設計原則
- [API キー リファクタリング](docs/dev_notes/api_keys_refactor.md) - 移行ログ

## 🛠️ 開発ステータス

### 完了 ✅ (バージョン 1.0)
- [x] **9 つの完全な環境** (spread, adversary, tag, push, crypto, reference, speaker_listener, world_comm, simple)
- [x] **統合 LLM API インターフェース** (リモート: qwen/deepseek/gpt/gemini; ローカル: transformers/ollama/vllm)
- [x] **観測パーサー** (9 つの環境、標準化 JSON 出力)
- [x] **プロンプト標準化** (4 つのモジュール関数 × 9 つの環境)
- [x] **ロギング システム** (obs + action + thought + reward + final_summary)
- [x] **ベンチマーク フレームワーク** (バッチ テスト + 統計分析)
- [x] **シード メカニズム** (1-20 再現可能な実験)
- [x] **API キー管理** (.env ファイル + インタラクティブ セットアップ スクリプト)
- [x] **ドキュメント** (15+ Markdown ドキュメント)
- [x] **ビデオ 記録** (エピソードごとに自動生成 mp4)

### テスト カバレッジ ✅
- [x] すべての 9 つの環境が独立して実行可能
- [x] ベンチマーク フレームワークが すべての環境をテスト
- [x] シード固定検証済み
- [x] ログ形式統一および完全
- [x] API キー セキュリティ管理

### 計画中 📅 (バージョン 1.1+)
- [ ] パフォーマンス ベンチマーク データベース
- [ ] インタラクティブ ビジュアライゼーション ダッシュボード
- [ ] Few-shot サンプル ライブラリ
- [ ] マルチプロセス並列テスト
- [ ] より多くのローカル モデル サポート

## 🤝 貢献

貢献を歓迎します!手順:

1. このリポジトリをフォーク
2. 機能ブランチを作成 (`git checkout -b feature/AmazingFeature`)
3. 変更をコミット (`git commit -m 'Add some AmazingFeature'`)
4. ブランチにプッシュ (`git push origin feature/AmazingFeature`)
5. プル リクエストを開く

**貢献エリア**:
- 新しい環境のパーサー実装
- プロンプト エンジニアリング テンプレートの改善
- 新しい評価メトリクスの追加
- ドキュメントと例の改善

## 📄 ライセンス

このプロジェクトは MIT ライセンスの下でライセンスされています - [LICENSE](LICENSE) ファイルを参照

## 🙏 謝辞

- [PettingZoo](https://pettingzoo.farama.org/) - マルチエージェント環境ライブラリ
- [OpenAI](https://openai.com/) - LLM API
- すべての貢献者


## ⭐ スター履歴

このプロジェクトがお役に立てば、スターをお願いします ⭐!

---

**最終更新**: 2026-01-26  
**バージョン**: 1.0.0 - すべてのコア機能完了  
**ステータス**: ✅ 本番環境対応
