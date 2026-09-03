# Meta広告 GPT → Claude Code 下書きワークフロー

## 目的

GPTで広告企画・文章・画像を作り、Claude CodeでMeta入稿前の下書きパッケージを検証・保存する。

公開は必ず人がMeta広告マネージャで最終確認して行う。

## 1. GPTへ渡す入力

GPTは以下を必ず読む。

1. `META_AD_CREATIVE_AND_OPERATIONS_MANUAL.md`
2. `CARSOL_META_AD_PLAYBOOK.md`
3. `CARSOL_META_AD_LEARNING_LOG.md`
4. 今回のCampaign Brief

## 2. GPTの出力物

```text
campaigns/YYYY-MM-[campaign]/
  brief.md
  hypothesis.md
  copy.md
  image-spec.md
  assets/
    4x5/
    9x16/
    1x1/
  handoff.md
```

### copy.md 必須項目

- Primary Text
- Headline
- Description / 通話の説明
- CTA
- 広告名
- 変更した変数
- 既存広告との違い

### image-spec.md 必須項目

- 主メッセージ
- サブメッセージ
- ロゴ位置
- 写真テーマ
- 4:5構図
- 9:16構図とセーフゾーン
- 1:1構図
- 禁止表示

## 3. Claude Codeへ渡す標準プロンプト

```text
このフォルダはMeta広告の入稿前パッケージです。

必ず以下を読んでください。
- ../../META_AD_CREATIVE_AND_OPERATIONS_MANUAL.md
- ../../CARSOL_META_AD_PLAYBOOK.md
- ../../CARSOL_META_AD_LEARNING_LOG.md
- brief.md
- hypothesis.md
- copy.md
- image-spec.md

目的:
Meta広告を公開することではなく、Meta広告マネージャへ登録可能な「下書きパッケージ」を作成・検証してください。

実施:
1. 事実条件を照合
2. 禁止表現・未確認表現を検出
3. 画像ファイルの有無・比率・解像度を検証
4. 9:16セーフゾーンのチェック項目を出す
5. Primary Text / Headline / Description / CTA を整形
6. meta-draft.json を生成
7. qa.md を生成
8. blockerがなければ READY_FOR_META_DRAFT とする
9. 結果をgit diffで確認

禁止:
- 固定事実にない事実を補完しない
- 広告を公開しない
- 予算を変更しない
- 既存広告を停止しない
- Meta側の設定を勝手に変更しない

最終出力:
- READY_FOR_META_DRAFT / BLOCKED
- blocker一覧
- 作成・変更ファイル一覧
```

## 4. meta-draft.json 標準

```json
{
  "test_id": "",
  "brand": "CARSOL",
  "campaign_goal": "phone_call",
  "audience_hypothesis": "",
  "creative_angle": "",
  "primary_text": "",
  "headline": "",
  "description": "",
  "cta": "CALL_NOW",
  "assets": {
    "feed_4x5": "",
    "stories_reels_9x16": "",
    "square_1x1": ""
  },
  "facts_checked": true,
  "qa_status": "READY_FOR_META_DRAFT"
}
```

## 5. Meta広告マネージャで人が行う工程

1. 対象キャンペーン / 広告セットを選ぶ
2. 新規広告を作成
3. 画像を配置別にアップロード
4. Primary Text入力
5. Headline入力
6. Description / 通話の説明入力
7. CTA確認
8. 電話番号確認
9. Facebook / Instagram / Reels / Storiesをプレビュー
10. 予算・地域・CVを確認
11. 公開
12. 公開日時・広告IDをLearning Logへ記録

## 6. 将来の自動化

### Phase 1
ローカル/Git内で下書き生成のみ。

### Phase 2
Metaへ広告Draftを作成するがPublishしない。

### Phase 3
人間の承認後のみPublish。

最初から完全自動公開にしない。

## 7. 成果回収

分析時にMeta CSVを取得し、広告ID、訴求軸、形式、期間、広告費、電話 / リード、CPA / CPL、表示 / リーチ、品質、顧客品質、査定、成約、粗利益をLearning Logへ追加する。

広告結果はGPTが次回のCampaign Briefを作る際の入力データとする。
