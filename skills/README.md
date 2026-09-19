# FlyRank Skills Reference

This directory documents the core guidelines and skills used across the FlyRank ML Foundations curriculum.

## Available Skills

### 1. `training-honest-models`
Guidelines for honest ML development, validation design, and baseline comparisons:
- **Baseline Parity**: Every model candidate must be evaluated on the exact same holdout split and identical evaluation metric as the heuristic/Week-4 baseline.
- **Leakage Prevention**: Feature engineering, imputation, and scaling must be fit strictly on training splits and applied to validation/test splits.
- **Metric Realism**: Use task-appropriate metrics (e.g. PR-AUC, Precision@K, Spearman Rank Correlation, Calibration) rather than raw accuracy on imbalanced targets.
- **Complexity Justification**: Start with linear and tree benchmarks. Do not adopt complex architectures unless they demonstrate a significant, validated lift over interpretable alternatives.
- **Error Inspection**: Inspect false positives, false negatives, and residual distributions qualitatively to understand real-world failure modes.

### 2. `flyrank/flyrank-data`
Standards for FlyRank SEO telemetry and data schema:
- **Entity**: Google Search Console (GSC) URL/query performance records.
- **Primary Telemetry**:
  - `url`: Page slug identifier (e.g., `/blog/article-0001`).
  - `position`: Average Google SERP ranking position (1.0 to 15.0+).
  - `ctr`: Observed click-through rate (`clicks / impressions`).
  - `expected_ctr`: Benchmark CTR based on the position-curve lookup.
  - `ctr_gap`: Difference between observed CTR and expected benchmark (`ctr - expected_ctr`).
  - `impressions`: Total search impressions in the evaluation period.
  - `clicks`: Total search clicks in the evaluation period.
  - `monthly_volume`: Keyword search volume demand.
  - `days_since_update`: Content freshness indicator (days since last edit).
- **Target Actions & Lanes**:
  - **CTR-fix Lane**: Focuses on top-10 ranking pages with significant CTR deficits (`ctr_fix_flag`, action: `rewrite_title_meta`, reason: `LOW_CTR_TOP10`).
  - **Content Refresh Lane**: Focuses on decaying or stale pages (`refresh_flag`).
  - **Quick-Win Lane**: High-volume, high-opportunity keyword ranking pages (`quick_win_flag`).
