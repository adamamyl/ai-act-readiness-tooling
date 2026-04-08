---

1. Data Provenance (AI Act / ISO 42001)
Tool: ML-Croissant
Artefact: metadata.json
Mapping: Art. 10 (Data Governance)

---

```json
{
  "@context": "[https://schema.org/](https://schema.org/)",
  "@type": "sc:Dataset",
  "name": "Customer_Support_v2_2026",
  "description": "Fine-tuning set for support agent, PII-scrubbed via Presidio.",
  "license": "[https://spdx.org/licenses/Apache-2.0.html](https://spdx.org/licenses/Apache-2.0.html)",
  "conformsTo": "[https://mlcommons.org/croissant/1.0](https://mlcommons.org/croissant/1.0)",
  "distribution": [
    {
      "@type": "sc:FileObject",
      "name": "training_data",
      "contentUrl": "s3://prod-data/cleaned_support.csv",
      "encodingFormat": "text/csv",
      "sha256": "e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855"
    }
  ],
  "rai": {
    "dataCollection": "User-consented support tickets Jan-Mar 2026.",
    "personalDataStripped": true,
    "provenance": "[https://lineage.company.com/job/scrub-pii-v4](https://lineage.company.com/job/scrub-pii-v4)"
  }
}
```