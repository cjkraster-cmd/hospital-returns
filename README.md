[README-HRRPTableau.md](https://github.com/user-attachments/files/34867861/README-HRRPTableau.md)
# Florida Hospital Readmissions, FY 2022–2026

**Live dashboard:** [Tableau Public](https://public.tableau.com/views/FloridaHospitalReadmissionsFY20222026/FloridaReadmissionsDashboard?:language=en-US&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link)

How do Florida hospitals compare with the nation on 30-day readmissions, and do the same hospitals stay above expected year after year? This project profiles CMS Hospital Readmissions Reduction Program (HRRP) data for heart attack (AMI), heart failure (HF) and pneumonia (PN) across five fiscal years. It is Phase 1 of a larger study of whether weekend discharge is linked to readmission in Florida.

## Key findings (FY 2026 unless noted)

- **Florida runs above the nation on all three conditions.** 67% of Florida hospitals had more heart failure readmissions than expected, against 49% nationally (AMI 65% vs. 50%; pneumonia 52% vs. 47%).
- **The gap is persistent.** Florida's heart failure share stayed between 65% and 69% in every fiscal year from 2022 to 2026, while the US stayed near 50%.
- **Many hospitals are consistently above expected.** Of 154 Florida hospitals scored on heart failure in all five years, 54 were above expected every year and only 14 stayed at or below expected every year.
- **39 of 128 Florida hospitals** scored on all three conditions were above expected on all three.
- **Size matters a little.** The largest third of hospitals by discharge volume had the lowest median ratios, and the only median below 1.0 (pneumonia, 0.993).

## Data

| Source | Details |
| --- | --- |
| CMS Hospital Readmissions Reduction Program, hospital-level files | FY 2022–2026, from the [Provider Data Catalog](https://data.cms.gov/provider-data/) and Hospital Data Archive |
| Measure | Excess readmission ratio (ERR): predicted ÷ expected 30-day readmission rate, risk-adjusted by CMS. Above 1.0 = more readmissions than expected. |
| Coverage | All US hospitals in HRRP; Florida = 164 hospitals scored in FY 2026 |
| Performance periods | Each fiscal year reflects about three years of earlier discharges (FY 2026 = July 2021 – June 2024), so neighbouring years overlap |

## Method

1. Combined five annual HRRP files and filtered to AMI, HF and PN.
2. Kept the CMS Certification Number (`facility_id`) as text to preserve leading zeros.
3. Treated "N/A" and "Too Few to Report" as missing, not zero.
4. Computed the share of hospitals above 1.0 and median ratios for Florida and the US by condition and year.
5. Flagged hospitals above 1.0 on all three conditions, and classified hospitals scored in all five years as above every year, at or below every year, or crossed 1.0.
6. Split Florida hospitals into thirds by total FY 2026 discharges as a rough proxy for size.
7. Built the dashboard in Tableau Public using level-of-detail (LOD) expressions for the hospital-level flags.

## Repository structure

```
├── data_raw/          # CMS downloads (git-ignored)
├── sql/               # Queries for the Phase 2 patient-level analysis
├── notebooks/         # Exploration
├── output/            # Cleaned files used by the dashboard
├── clean_profile.py   # Cleans the HRRP file and profiles Florida hospitals
└── README.md
```

Run the cleaning script with:

```
python clean_profile.py FY_2026_Hospital_Readmissions_Reduction_Program_Hospital.csv output/
```

## Limitations

- The ERR is a model-based, risk-adjusted estimate, not a raw readmission rate, and CMS shrinks small hospitals' estimates toward 1.0.
- "Above 1.0" means worse than expected; it is not the same as receiving a payment penalty, which CMS sets against peer-group medians.
- Overlapping performance periods make year-to-year changes gradual by design.
- Discharge volume is only a proxy for hospital size.

## Next: Phase 2

Using the HCUP Florida State Inpatient Database (2022–2023), test whether patients discharged on weekends or holidays are more likely to be readmitted within 30 days, and whether any effect is larger at hospitals that are consistently above expected.

## Tools

Python (pandas), Tableau Public, CMS Provider Data Catalog

---
*Christopher Kraster · Google Data Analytics Certificate · Google AI Professional Certificate*
