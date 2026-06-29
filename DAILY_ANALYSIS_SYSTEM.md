# 毎日の競合分析 × 自己分析 × Manus連携システム

## システム概要

```
【毎朝20分のルーティン】

① データ収集（10分）
   └─ 競合TOP10 + 自分のアカウントの数値を記録
          ↓
② Claude/ChatGPTで分析（5分）
   └─ prompts/STEP2_analysis_prompt.md を使用
          ↓
③ 修正判断（2分）
   └─ 「要修正」なら → 該当Manusプロンプトをコピー
          ↓
④ Manusに渡して実行（3分）
   └─ prompts/manus/ の該当ファイルを貼り付け
```

## 毎日確認するアカウント設定

`prompts/STEP1_data_template.md` に自分の競合TOP10を登録する。
最初の1回だけ設定すれば、以後はそのテンプレートを毎日コピーして数値を入れるだけ。

## 使用ツール

| ツール | 用途 | 料金 |
|---|---|---|
| Claude Pro / ChatGPT Plus | STEP2の分析 | 月3,000円 |
| Manus | 修正アクション実行 | 利用プランによる |
| Social Blade (socialblade.com) | フォロワー推移の確認 | 無料 |
| Phlanx (phlanx.com) | エンゲージメント率の計算 | 無料 |

## フォルダ構成

```
prompts/
├── STEP1_data_template.md      ← 毎日コピーして数値を入れる
├── STEP2_analysis_prompt.md    ← Claude/ChatGPTに貼るプロンプト
├── STEP3_manus_selector.md     ← どのManusプロンプトを使うか判断
└── manus/
    ├── M1_content_gap.md       ← コンテンツ不足を埋める
    ├── M2_viral_clone.md       ← バズ投稿フォーマットを真似る
    ├── M3_trend_ride.md        ← トレンドに乗ったコンテンツ作成
    ├── M4_engagement_fix.md    ← エンゲージメント低下の改善
    ├── M5_schedule_optimize.md ← 投稿スケジュール最適化
    ├── M6_weekly_calendar.md   ← 週間カレンダー自動生成
    └── M7_account_audit.md     ← 月1回の全体監査
```

## 修正判断の基準（Manus起動条件）

| 状況 | 使うManusプロンプト |
|---|---|
| 競合が扱っているが自分が扱っていないトピックがある | M1 |
| 競合の特定フォーマット（スレッド/画像/動画）がバズっている | M2 |
| X/SNS全体でトレンドトピックが発生している | M3 |
| 自分のエンゲージメント率が競合の50%以下 | M4 |
| 自分の投稿頻度が競合の半分以下 | M5 |
| 月曜日（週始め） | M6 |
| 月末（月1回） | M7 |
