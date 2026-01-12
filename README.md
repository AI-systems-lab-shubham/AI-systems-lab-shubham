# Week 1: Foundations

Week 1 covers system thinking fundamentals for DressUp!: architecture decisions, ERD/DFDs, documentation structure, and a production prompt with test evidence.

## Quick links (start here)

### Production prompt + inputs
- Production prompt: [[daily_outfit_v1.0.txt](prompts/generation/daily_outfit_v1.0.txt)](https://github.com/AI-systems-lab-shubham/AI-systems-lab-shubham/blob/main/week1_foundations/prompts/generation/daily_outfit_v1.0.txt)
- Sample input bundle: [week1_foundations/prompts/test_inputs/daily_outfit_sample_input.json](https://github.com/AI-systems-lab-shubham/AI-systems-lab-shubham/blob/main/week1_foundations/prompts/test_inputs/daily_outfit_sample_input.json)

### Prompt testing (evidence)
- Testing harness (Claude Opus 4.5): [[daily_outfit_prompt_test_harness_opus45.md](prompts/testing_harnesses/daily_outfit_prompt_test_harness_opus45.md)](https://github.com/AI-systems-lab-shubham/AI-systems-lab-shubham/blob/main/week1_foundations/prompts/testing_harnesses/daily_outfit_prompt_test_harness_opus45.md)
- Test report (results): [[DressUp_Prompt_Test_Report_v1.md](prompts/prompt_testing_reports/DressUp_Prompt_Test_Report_v1.md)](https://github.com/AI-systems-lab-shubham/AI-systems-lab-shubham/blob/main/week1_foundations/prompts/prompt_testing_reports/DressUp_Prompt_Test_Report_v1.md)

## Folder map

- `adr/`  
  Architecture Decision Records (why choices were made).
- `diagrams/`  
  Exports for system architecture, ERD, and DFDs.
- `docs/`  
  Week 1 syllabus and supporting documentation.
- `prompts/`  
  Prompt library standards + prompt artifacts.

## What the daily outfit prompt does

Given a JSON input bundle (wardrobe + preferences + weather + context + history), it returns **valid JSON only** with:
- 1 primary outfit
- 2 backup outfits
- 1 budget / low-effort option
- a concise explanation, warnings, and assumptions
- scored dimensions with weights that sum to ~1.0

## Status

Week 1 prompt testing is complete and the daily_outfit prompt is production-ready based on the included test report.
