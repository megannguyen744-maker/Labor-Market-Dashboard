# US Labor Market Pulse Dashboard

A Power BI dashboard analyzing current U.S. labor market conditions using real government data — built to answer the question: *"Is now a good time to change jobs?"*

## Overview
This project combines two official BLS data sources to analyze labor market momentum and pay benchmarks:
- **JOLTS** (Job Openings and Labor Turnover Survey) — monthly hires, quits, job openings, and layoffs/discharges rates, pulled live via the [BLS Public API](https://www.bls.gov/developers/)
- **OEWS** (Occupational Employment and Wage Statistics) — median annual wages across the most common U.S. occupations, May 2025 release

## Key Findings
As of the latest data, the labor market shows early signs of moderating: job openings and hiring rates have both fallen roughly 12–13% year-over-year, while the quits rate remains flat at its 2016–2019 pre-pandemic average. Layoffs show no meaningful increase — suggesting a gradual normalization from a historically tight market rather than a downturn. Pay varies widely across common occupations, from ~$37K to $136K median annual wage.

## Dashboard Pages
1. **Labor Market Pulse** — current KPI snapshot and rate trends since 2016
   (<img width="1337" height="746" alt="JOLTS-OEWS PG 1" src="https://github.com/user-attachments/assets/24e61abb-d9d1-4b73-b9f5-d4a6ccd9ffa9" />
)
3. **Trend & Momentum** — year-over-year rate comparisons
4. **Pay Benchmarking** — median wages and employment size across top occupations
5. **The Verdict** — synthesized takeaway

## Tools
Power BI Desktop, Power Query (M), DAX, BLS Public API

## Data Sources
- [BLS JOLTS](https://www.bls.gov/jlt/)
- [BLS OEWS](https://www.bls.gov/oes/tables.htm)

![Labor Market Pulse](page1-pulse.png)
![The Verdict](page4-verdict.png)
