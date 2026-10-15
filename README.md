# Ghost Citations Study 2026

**Do AI answers that link to your site actually name your brand?**

Methodology and aggregated data for the Ghost Citations study by [Ivan Nonveiller](https://github.com/IvanNon) at [Reach](https://usereach.ai). This repo holds only aggregated, anonymized tables. No brand names, prompts, answer text or page URLs.

## Definition

A **ghost citation** is an AI answer that links to a brand's own domain but does not name the brand in the answer text.

## Headline results

| Finding | Number |
|---|---|
| Answers that link to the brand's site but don't name it | **43%** (9,624 of 22,375) |
| Ghost answers that name *other* brands instead | **87%** |
| Ghost rate when the cited own page is a listicle ("best / top / vs / alternatives") vs other own pages | 50% vs 34% |
| Ghost rate, brand **not** in the cited page's title vs **in** the title (Jan–Aug, pooled) | **42.9% vs 12.2%** |
| Same comparison, within brands (Mantel-Haenszel stratified) | **about 60% fewer** ghost citations |

By engine (answers linking to the brand's site that don't name it): AI Mode 36%, AI Overviews 40%, ChatGPT 43%, Perplexity 54%.

The title effect holds on every engine (no brand in title → brand in title, Jan–Aug): AI Mode 34→10%, AI Overviews 37→8%, ChatGPT 54→19%, Perplexity 52→13%.

## Method

- **Source:** Reach's production data. Tracked prompts for client brands, run on four engines: ChatGPT, Perplexity, Google AI Mode and Google AI Overviews. Read-only, aggregate statistics only.
- **Unit:** a brand × answer pair.
- **Engine-level sample (`ghost_citation_rates_by_engine`, `mention_citation_matrix_by_engine`):** 119,848 brand × answer pairs across all 75 active client workspaces, 4 engines, 12 sampled days between Jun 3 and Aug 19, 2026.
- **Page-level sample (title analysis):** answers that cite exactly one of the brand's own pages ("single own page"). About 46,000 page × answer pairs for Jun 1 – Aug 21 (43 brands, every day except Jun 2 and Aug 5–6). Extended back to Jan 1 for about 71,000 pairs in total.
- **"Named":** Reach's answer-extraction flag (`is_mentioned`), not text matching, so generic brand names don't distort it.
- **"Links to the brand":** the answer cites a URL on the brand's own domain.
- **Listicle:** URL-pattern match for "best", "top", "vs", "alternatives".
- **"Brand in title":** the brand name appears in the cited page's `<title>`, taken from Reach's stored snapshot of the page.
- **Within-brand robustness check:** every 2nd day Jan 3 – Aug 21 (456 engine-days, 36,400 page citations), 40 brands. Among the 20 brands with at least 10 citations in both groups, brand-in-title pages were ghosted less often in 17 of 20 (two-sided sign test p = 0.003). Leave-one-brand-out keeps the pooled reduction between 64.5% and 78.8%.

## Data

All files are in [`data/`](data). Percentages are in percent, not fractions.

| File | What it contains |
|---|---|
| `ghost_citation_rates_by_engine.csv` | Own-link rate, named rate and ghost rate per engine, plus ghost rate by link type (listicle vs other own page). |
| `mention_citation_matrix_by_engine.csv` | Share of answers that are named-and-cited, mention-only, ghost, or invisible, per engine. |
| `ghost_rate_by_title_jan_to_aug.csv` | Ghost rate by brand-in-title, listicle and engine, for Jan–May, Jun–Aug and combined. |
| `ghost_rate_by_title_monthly.csv` | Monthly ghost rate with and without the brand in the title. August is a partial month. |
| `ghost_rate_by_brand_prominence.csv` | Ghost rate by brand in title, brand in intro and mention-count bucket. `ALL_PAIRS` covers every cited own page per answer. `SINGLE_*` covers answers citing exactly one own page, overall and per engine. The two scopes give different absolute rates by design. |
| `within_brand_check_anonymised.csv` | Per-brand ghost rates with and without the brand in the title, for the 20 brands with the most brand-in-title citations. Brands are relabelled A–T in order of volume. |

## Caveats

- **Correlational.** Pages with the brand in the title are often homepages, product pages or "Brand vs X" comparisons, which are inherently about the brand.
- **Concentrated.** The top brand supplies 34.5% of brand-in-title citations, and the top 3 supply 60.5%.
- **Pooled vs within-brand.** The pooled reduction (72%) partly reflects brand mix. The within-brand estimate (about 60%) is the more conservative figure.
- **The listicle-specific claim is weaker within brands.** Only 5 brands qualify, 3 of 5 lower, 40.4% stratified reduction.
- **Raw brand-mention count doesn't help.** Pages with 10+ mentions have the highest ghost rate, likely because they are mostly listicles and the count includes boilerplate.
- **Snapshot mismatch.** Titles come from Reach's snapshot, which may not be the version the engine saw.
- **Sample.** Reach client brands only, mostly B2B/SaaS in Portugal and the US. Some prompts are branded. Perplexity's mid-June to mid-July missing-citations issue lowers counts but not the ratios much.
- **Trend.** The no-brand-title ghost rate rises from about 30–37% (Jan–May) to about 45–48% (Jun–Aug). It may reflect brand mix and a July onboarding wave rather than a real trend.

## Cite

Nonveiller, I. (2026). *Ghost Citations Study 2026*. https://github.com/IvanNon/ghost-citations-study-2026

Questions or challenges: open an issue.
