# Validation Levels for NWB Files
NWB files must conform to criteria that are enforced via three levels of validation: 

## NWB File Validation
[add links]

## Critical NWB Checks
[add links]

## Missing DANDI Metadata
The following metadata must be present in the NWB file for a successful upload to DANDI:
- subject
- subject_id
- species - must be in Latin binomial, e.g. "Mus musculus"
- sex - must be "M", "F", "O", or "U"
- date_of_birth or age - "age" must be in ISO 8601 format, e.g. "P70D" for 70 days, or, if it is a range, must be "
  [lower]/[upper]", e.g. "P10W/P12W", which means "between 10 and 12 weeks"

[add links]
