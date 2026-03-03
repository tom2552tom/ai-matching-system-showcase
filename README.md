# 🤖 AI Matching System — 案件 × エンジニア 自動マッチング

[![Python](https://img.shields.io/badge/Python-3.11-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
[![Django](https://img.shields.io/badge/Django-5.2.8-092E20?style=for-the-badge&logo=django&logoColor=white)](https://www.djangoproject.com/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-16-4169E1?style=for-the-badge&logo=postgresql&logoColor=white)](https://www.postgresql.org/)
[![Redis](https://img.shields.io/badge/Redis-7.x-DC382D?style=for-the-badge&logo=redis&logoColor=white)](https://redis.io/)
[![Celery](https://img.shields.io/badge/Celery-5.x-37814A?style=for-the-badge&logo=celery&logoColor=white)](https://docs.celeryq.dev/)
[![Gemini](https://img.shields.io/badge/Google_Gemini_API-1.5_Pro-4285F4?style=for-the-badge&logo=google&logoColor=white)](https://ai.google.dev/)
[![Render](https://img.shields.io/badge/Deploy-Render.com-46E3B7?style=for-the-badge&logo=render&logoColor=white)](https://render.com/)

> **案件情報とエンジニアのスキルセットを AI が自動解析し、最適なマッチングを提案する本格的な Django Web アプリケーション。**

---

## 🎯 プロジェクト概要

SES（システムエンジニアリングサービス）業界において、案件とエンジニアのマッチングは担当者の経験と感覚に依存しがちです。
本システムは **Google Gemini API × sentence-transformers × scikit-learn** を組み合わせた AI エンジンにより、
スキルの意味的類似度・経験年数・稼働条件などを総合的に評価し、最適なマッチング候補を自動提案します。

---

## ✨ 主な機能

| 機能 | 説明 |
|---|---|
| 📋 **案件・エンジニア管理** | 案件情報・エンジニアのスキルセットを登録・管理 |
| 🤖 **AI 自動マッチング** | Gemini API による意味解析 + ベクトル類似度スコアリング |
| ⚡ **非同期バックグラウンド処理** | Celery + Redis による大量マッチングの非同期実行 |
| 📊 **リアルタイムダッシュボード** | タスク実行状況・マッチング結果をリアルタイム表示 |
| 📧 **メール通知** | マッチング完了時の自動メール送信 |
| 🔄 **定期自動実行** | Celery Beat による定期マッチングタスクスケジューリング |

---

## 🏗️ システムアーキテクチャ

```
┌─────────────────────────────────────────────────┐
│                  ユーザー（ブラウザ）               │
└───────────────────────┬─────────────────────────┘
                        │ HTTP リクエスト
┌───────────────────────▼─────────────────────────┐
│            Django 5.2.8  (Gunicorn)              │
│  ┌──────────────┐   ┌────────────────────────┐  │
│  │  Views / API  │   │  AI Matching Engine    │  │
│  │  (案件・     │   │  ・Gemini API          │  │
│  │   エンジニア  │   │  ・sentence-transformers│  │
│  │   CRUD)      │   │  ・scikit-learn        │  │
│  └──────┬───────┘   └──────────┬─────────────┘  │
└─────────┼────────────────────── ┼ ───────────────┘
          │                       │ タスク投入
┌─────────▼───────┐   ┌──────────▼──────────────┐
│   PostgreSQL    │   │   Redis (Message Broker) │
│   (データ永続化) │   └──────────┬──────────────┘
└─────────────────┘              │ タスク取得
                       ┌─────────▼──────────────┐
                       │  Celery Worker / Beat   │
                       │  (非同期マッチング処理)  │
                       └────────────────────────┘
```

---

## 🧠 AI マッチングの仕組み

```
① 案件情報を受信
   └─ 必要スキル・経験年数・稼働条件 etc.

② Gemini API でテキスト正規化・意味解析
   └─ 要件の曖昧な表現を構造化データに変換

③ sentence-transformers でベクトル化
   └─ 案件要件 ↔ エンジニアスキルを同一ベクトル空間に配置

④ scikit-learn でコサイン類似度スコアリング
   └─ 類似度スコア上位 N 件を候補としてランキング

⑤ マッチング結果をダッシュボードに反映
   └─ リアルタイムで確認・承認・却下が可能
```

---

## 🛠️ 技術スタック

### Backend
| カテゴリ | 技術 | バージョン |
|---|---|---|
| Web Framework | Django | 5.2.8 |
| WSGI Server | Gunicorn | 最新版 |
| Task Queue | Celery | 5.x |
| Message Broker | Redis | 7.x |

### AI / ML
| カテゴリ | 技術 | 用途 |
|---|---|---|
| LLM | Google Gemini API (1.5 Pro) | テキスト解析・意味理解 |
| Embedding | sentence-transformers | スキルのベクトル化 |
| ML | scikit-learn | 類似度計算・スコアリング |

### Infrastructure
| カテゴリ | 技術 |
|---|---|
| Database | PostgreSQL 16 |
| Deploy | Render.com（Web / Worker / Beat / DB / Redis） |
| Version Control | GitHub |

---

## 🚀 デプロイ構成（Render.com）

```
Render.com
├── 🌐 Web Service        (Django + Gunicorn)
├── ⚙️  Background Worker  (Celery Worker)
├── ⏰  Background Worker  (Celery Beat — 定期タスク)
├── 🗄️  PostgreSQL         (データベース)
└── ⚡  Redis              (メッセージブローカー)
```

---

## 📸 スクリーンショット

> ※ スクリーンショットは順次追加予定です。

| ダッシュボード | マッチング結果 |
|---|---|
| （準備中） | （準備中） |

---

## 🔒 ソースコードについて

本リポジトリはポートフォリオ用のショーケースです。  
**ソースコードはクライアント都合により非公開**としています。  
実装の詳細・デモ・コードレビューをご希望の方はお問い合わせください。

---

## 👤 作成者

**畑中 智和（Tomokazu Hatanaka）**  
AI Application Developer / System Architect  
📍 Los Angeles, CA, USA  

[![GitHub](https://img.shields.io/badge/GitHub-tom2552tom-181717?style=flat-square&logo=github)](https://github.com/tom2552tom)
[![Email](https://img.shields.io/badge/Email-tom2552tom%40gmail.com-D14836?style=flat-square&logo=gmail)](mailto:tom2552tom@gmail.com)

---

## 🔗 関連プロジェクト

- [AI Customer Support System](https://github.com/tom2552tom) — Gemini API × Retell AI による音声 + チャット対応 AI カスタマーサポート

---

*© 2025 Tomokazu Hatanaka. All rights reserved.*
