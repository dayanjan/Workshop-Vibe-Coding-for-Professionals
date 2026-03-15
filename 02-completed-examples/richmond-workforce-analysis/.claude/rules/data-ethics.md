## Data Ethics Rules

These rules apply to all data collection, analysis, and reporting in this project.

### Public Data Only

All data used in this project must be publicly available. The BLS QCEW, OEWS, and CES
datasets are published by a federal agency and are free to access without authentication.
Do not incorporate proprietary, licensed, or access-restricted datasets without explicit
approval and documentation of the license terms.

### No Individual Identifiers

Never include individual names, Social Security numbers, employer identification numbers,
or any other personally identifiable information (PII) in analysis files, reports, or
version-controlled code. BLS public data is already aggregated, but be vigilant if
combining with other sources.

### Aggregation Threshold

Report data at the jurisdiction level (MSA, county, state) or higher. If an industry cell
contains fewer than 3 establishments or the data is suppressed by BLS for confidentiality,
do not attempt to reverse-engineer or estimate the suppressed value. Note the suppression
in your output and move on.

### Hedging Language for Uncertainty

When findings depend on preliminary data, small sample sizes, or suppressed cells, use
hedging language:

- "The available data suggest..." rather than "The data prove..."
- "This trend is consistent with..." rather than "This trend confirms..."
- "Approximately" or "roughly" when rounding or estimating.

### Source Attribution

Every table, chart, and factual claim in a report must include:

- **Data source:** e.g., "Bureau of Labor Statistics, Quarterly Census of Employment and Wages"
- **Date range:** e.g., "2023-Q1 through 2025-Q3"
- **Geography:** e.g., "Richmond MSA, FIPS 40060"
- **Retrieval date:** e.g., "Retrieved March 2026"

Place source lines directly below charts and at the end of report sections. Do not bury
citations in footnotes that readers might skip.

### AI-Generated Content Transparency

Clearly distinguish between AI-generated analysis and verified facts. When Claude produces
a narrative summary or interpretation, the report should note that the analysis was
AI-assisted. Raw data and direct BLS statistics are verified facts; trend interpretations,
comparisons, and projections are analytical outputs that should be reviewed by a human
before publication.
