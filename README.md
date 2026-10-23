# CrimeBusters: Victimisation Rates in New Zealand

This project looks at how police-recorded victimisation rates in New Zealand vary by age and sex for three crime types: assault, sexual offences and theft from a person. It combines NZ Police unique-victim data with Stats NZ population estimates for the 12-month periods ending June 2024, 2025 and 2026.

## Files

- `399_CrimeBusters_final.Rmd` is the full analysis. It cleans the data, joins the victim counts onto the population, calculates victimisation rates (victims ÷ population), and plots them by age, and by age and sex.
- `Data_Jun2024.csv`, `Data_Jun2025.csv` and `Data_Jun2026.csv` are the NZ Police victim data, one file per year.
- `Population_data.csv` holds the Stats NZ population estimates by year, sex and age group.

## Running it

Open `399_CrimeBusters_final.Rmd` in RStudio with the CSV files in the same folder and click **Knit**. The only package needed is `tidyverse`. The plots are saved as `.png` files in that folder.
