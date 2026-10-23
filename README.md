# CrimeBusters: Victimisation Rates in New Zealand

How likely is a New Zealander to be recorded by Police as a victim of crime, and how does that vary with age and sex?

This project calculates police-recorded victimisation rates for three crime types — **assault**, **sexual offences** and **theft from a person** — by combining NZ Police unique-victim data with Stats NZ population estimates for the 12-month periods ending June 2024, 2025 and 2026.

## Key findings

| Crime type | Highest-rate age group | Average annual rate |
|---|---|---|
| Assault | 25–29 years | 2.05% |
| Sexual offences | 15–19 years | 0.52% |
| Theft from a person | 30–34 years | 0.06% |

Rates are averaged over 2024–2026, with both sexes combined. Breakdowns by sex are in the plots below.

## Plots

| By age | By age and sex |
|---|---|
| ![Assault by age](plot1_assault_age.png) | ![Assault by age and sex](plot2_assault_age_sex.png) |
| ![Sexual offences by age](plot3_sexoff_age.png) | ![Sexual offences by age and sex](plot4_sexoff_age_sex.png) |
| ![Theft from a person by age](plot5_theft_age.png) | ![Theft from a person by age and sex](plot6_theft_age_sex.png) |

## Repository contents

| File | Description |
|---|---|
| `399_CrimeBusters_final.Rmd` | Full analysis: cleaning, joining, rate calculation and plots |
| `Data_Jun2024.csv`, `Data_Jun2025.csv`, `Data_Jun2026.csv` | NZ Police unique-victim data ("Age Sex ROV" dataset), one file per 12-month period ending June |
| `Population_data.csv` | Stats NZ mean estimated resident population by year, sex and 5-year age group (cleaned) |
| `Technical supplement.pdf` | Data sources, assumptions, and step-by-step processing instructions |
| `plot*.png` | Output figures |

## Data sources

- **Victims:** [NZ Police Data](https://www.police.govt.nz/about-us/publications-statistics/data-and-statistics/policedatanz) — dataset "Age Sex ROV", 12-month periods ending June 2024–2026.
- **Population:** [Stats NZ Infoshare](https://infoshare.stats.govt.nz/) — Population → Population Estimates – DPE → *Estimated Resident Population by Age and Sex (1991+) (Annual-Jun)*, mean year ended June.

The population table was reshaped in Excel before analysis. The exact steps are in the technical supplement.

## How to run

1. Install [R](https://cran.r-project.org/) and [RStudio](https://posit.co/download/rstudio-desktop/).
2. Install the one required package:
   ```r
   install.packages("tidyverse")
   ```
3. Clone this repository and open `399_CrimeBusters_final.Rmd` in RStudio, with the four CSV files in the same folder.
4. Click **Knit**. This produces an HTML report and re-saves the six `plot*.png` files.

## Method

1. Stack the three Police files, keep assault, sexual offences and theft from a person, and drop victims with unknown sex or age.
2. Sum `Victim Count` by year, sex, age group and crime type.
3. Combine the Stats NZ 80–84 and 85–89 age bands into "80 years or over", to match the Police age bands.
4. For each crime type, left join the victim counts onto the population by year, sex and age. Groups with no recorded victims are set to 0.
5. **Victimisation rate = victims ÷ population.** Counts and population are summed over all three years before dividing, rather than averaging yearly rates.

## Assumptions and limitations

- **Recorded crime only.** Rates reflect crime reported to and recorded by Police, not the true prevalence. Reporting rates differ by crime type; sexual offences in particular are under-reported.
- **Unique victims.** Police count a person once per offence division per 12-month period, so a rate is the share of people recorded as a victim at least once in a year. Pooled across three years, counts are person-years.
- **Missing data.** Victims with unknown age or sex are excluded and assumed to be missing at random.
- **Descriptive, not causal.** Differences between groups describe who is recorded as a victim, not why.
