---
title: "まめトレード"
description: "暗号資産トレード Bot の研究基盤。実注文を出さない Paper モードを前提に、特徴量生成・レジーム分類・Risk Engine・バックテストまでを一気通貫で実装し、戦略を「検証可能な形」で育てている。"
pubDate: 2026-07-05
techStack:
  - Python
  - SQLAlchemy
  - FastAPI
  - Docker
  - uv
status: "研究中"
---

暗号資産の自動トレード Bot を、**いきなり実弾を撃たずに**育てるための研究基盤。

トレード Bot は「思いつきの戦略をすぐ動かして溶かす」失敗が定番。実際、痛い目を見た。  
なので、このプロジェクトでは逆に振り切った。  
デフォルトは必ず Paper モード（実取引所に注文を出さない）で、手数料・スプレッド・滑り・ドローダウンまで含めて戦略を検証できる土台づくりを最優先にしている。

現在の戦略では、まだガチホを超えるリターンを得られていない。

## パイプライン

市場データを取得し、以下を一気通貫で処理する。

1. **CandleBuilder** — 生データからローソク足を構築
2. **Feature Engine** — EMA・ATR・RSI・Donchian・Volume Z-score・板情報（spread / depth）などの特徴量を生成
3. **Regime Classifier** — 相場状態（トレンド / レンジなど）を分類
4. **Strategies + Overlays** — レジームに応じた戦略群と、暴落時に現金化する Crash Cash Guard などのオーバーレイを組み合わせる
5. **Risk Engine** — ポジションサイジング、損失上限、ドローダウン、連敗、レバレッジの管理と control lock
6. **Execution（Paper）** — maker-first エントリーと stop / take-profit 監視
7. **Reconciler** — DB と取引所状態の照合。ズレを検知したら risk lock を作成

## 検証まわり

- イベント駆動のバックテストと、performance / monthly / validation などの各種レポート生成
- 戦略比較・過剰適合（overfit）監査・アウトオブサンプル検証用の CLI 群
- 採用 / 不採用の判断は strategy research log に記録し、決定済みの論点を蒸し返さない運用
- FastAPI 製のダッシュボードと Telegram 通知

戦略そのものより、「戦略を安全に試し、比較し、記録する仕組み」を作ることに全力を注いだプロジェクト。
