# api-ethics-assignment
# API Ethics and Data Privacy Assignment

## Task 1 — Classify and Handle PII Fields

*   **full_name**: Direct PII. **Drop** or **Pseudonymize** (replace with a hashed ID). It directly identifies an individual.
*   **email**: Direct PII. **Drop**. Highly identifiable and not necessary for general research.
*   **date_of_birth**: Indirect PII (Quasi-identifier). **Mask/Generalize**. Convert to "Year of Birth" or age bucket (e.g., 30-40) to reduce re-identification risk while maintaining utility.
*   **zip_code**: Indirect PII (Quasi-identifier). **Mask/Generalize**. Truncate to the first 3 digits (e.g., 422xxx) to prevent linking to specific households.
*   **job_title**: Indirect PII. **Mask/Generalize**. Aggregate specific roles into broader categories (e.g., "Software Engineer" -> "Tech Worker") to prevent identification in small companies.
*   **diagnosis_notes**: Indirect PII (Sensitive). **Drop** or **Anonymize**. Notes often contain identifying details. If essential, use NLP to redact names/dates within the notes.

## Task 2 — Audit the API Script for Ethical Compliance

### Violation 1: Insecure Handling of API Credentials (Security/Ethics)
*   **Problem**: The `API_KEY` is hardcoded directly into the script. If this code is pushed to a public GitHub repository, the key will be stolen, leading to potential usage theft or unauthorized data access.
*   **Corrected Code**: Use environment variables to manage secrets.
```python
import os
import requests

# Load key from environment variable
API_KEY = os.environ.get("HEALTH_API_KEY")
API_URL = "https://healthstats-api.example.com/records"
