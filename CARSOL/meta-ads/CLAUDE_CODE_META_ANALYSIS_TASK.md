# Claude Code Task — CARSOL Meta広告 分析・Learning Log更新

## 目的

CARSOLのMeta広告CSVを広告単位で分析し、`CARSOL_META_AD_LEARNING_LOG.md` を事実ベースで更新する。

このタスクは「CPAが安い広告を選ぶ」だけではなく、次回の広告制作・顧客層仮説・記事制作に再利用できる学習資産を作ることが目的。

## 必ず読むファイル

1. `META_AD_CREATIVE_AND_OPERATIONS_MANUAL.md`
2. `CARSOL_META_AD_PLAYBOOK.md`
3. `CARSOL_META_AD_LEARNING_LOG.md`
4. `data/meta_ads_2026-08-04_2026-09-02.csv`

## 分析ルール

### 1. 事実・推論・仮説を分離

結果は必ず以下の3分類で書く。

- **OBSERVED**: CSVまたは現場フィードバックから直接確認できる事実
- **INFERENCE**: 観測事実から合理的に推測できるが未検証の解釈
- **HYPOTHESIS**: 次回テストで検証する仮説

推論を事実として書かない。

### 2. リードと電話を混ぜない

成果定義が異なるため、必ず別分析する。

- Lead: `actions:leadgen.other`
- Phone: `actions:click_to_call_native_call_placed`

### 3. 広告単位の指標

各広告について可能な範囲で算出する。

- spend
- results
- CPA / CPL
- impressions
- reach
- frequency = impressions / reach
- CPM = spend / impressions * 1000
- quality ranking

CTRやクリック数はCSVにないため推測しない。

### 4. サンプルサイズへの注意

- 1件しか成果がない広告は参考値扱い
- 消化額が極端に少ない広告は勝敗判定しない
- 0件広告も、消化額が少なければ断定しない
- 既存勝ち広告も3〜7件程度なので、過剰な統計的確信を持たない

### 5. 顧客品質をMeta結果と分ける

現場フィードバック:

> 広告経由の電話は、すでに多数の業者へ声をかけている価格比較層が多い。

これはMeta CSVでは検証できないため、`FIELD_FEEDBACK` として記録する。

次回以降は以下を記録する。

- 他社未相談 / 1社 / 2社 / 3社以上
- 電話理由
- スピード重視 / 手間削減 / 価格重視
- 有効相談
- 査定
- 成約
- 粗利益

## 重点分析テーマ

### A. リード獲得

特に比較:

- 広告A（動画②）
- 広告B（動画①）

確認したい点:

- CPL差
- CPM差
- frequency差
- 動画②が低CPLになった背景として、配信コストの低さも寄与している可能性

### B. 電話獲得

重点比較:

- 広告C（画像①）
- 広告A（動画②）
- 広告C（画像②）
- 広告A（動画③）

確認したい点:

- 画像①はCPAだけでなくCPMも低く品質ランキングが「平均以上」
- 動画②は成果量最大だがCPMは画像①より高い
- 画像②は1件のみで結論保留
- 動画③は1,769円消化・0電話で、既存主力と比べ弱いシグナル

## 必須アウトプット

`CARSOL_META_AD_LEARNING_LOG.md` を更新し、以下の章立てにする。

1. Executive Summary
2. Data Scope / Limitations
3. Lead Campaign Analysis
4. Phone Campaign Analysis
5. Creative Learnings
6. Audience Quality / Field Feedback
7. Current Hypotheses
8. New Test: HASSLE-FREE
9. Decision Rules
10. Article / SEO Insight Backlog
11. Next Data Collection Requirements

## 禁止事項

- CTRを推測しない
- クリックを推測しない
- 成約率を推測しない
- 「画像が動画より強い」など一般化しすぎない
- 1件CPAを勝ち広告と断定しない
- 新しいHASSLE-FREE広告を結果が出る前に成功扱いしない

## 最後に出すもの

- `ANALYSIS_VERDICT`
- `HIGH_CONFIDENCE_LEARNINGS`
- `LOW_CONFIDENCE_SIGNALS`
- `UNRESOLVED_QUESTIONS`
- `NEXT_TEST_RECOMMENDATION`
- 更新したファイル一覧
