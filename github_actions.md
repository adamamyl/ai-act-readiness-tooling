---

This workflow "stitches" your 2026 compliance stack into a single, automated gate. It treats compliance artifacts as Build Outputs, just like your binary or Docker image.

---

```yaml
name: "2026 Compliance-as-Code Gate"

on:
  pull_request:
    branches: [ main ]
  push:
    branches: [ main ]

jobs:
  # --- STAGE 1: SUPPLY CHAIN (CRA COMPLIANCE) ---
  supply-chain:
    name: "CRA & SBOM Analysis"
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: "Generate SBOM (CycloneDX)"
        uses: anchore/sbom-action@v0
        with:
          format: 'cyclonedx-json'
          output-file: 'artifacts/sbom.json'

      - name: "Scan for Vulnerabilities (Grype)"
        uses: anchore/scan-action@v3
        with:
          sbom: 'artifacts/sbom.json'
          fail-build: true
          severity-cutoff: critical

  # --- STAGE 2: AI GOVERNANCE (EU AI ACT & ISO 42001) ---
  ai-governance:
    name: "AI Act Robustness & Bias"
    needs: supply-chain
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: "Validate Data Provenance (Croissant)"
        run: |
          # Check if metadata matches actual dataset hash
          python -m croissant validate --file data/metadata.json

      - name: "Adversarial Probe (PyRIT)"
        run: |
          # Run automated red-teaming against the candidate model
          pyrit-cli --input "attacks/jailbreak_suite.yaml" --output "artifacts/pyrit-results.json"

      - name: "AI Robustness Scan (Giskard)"
        run: |
          # Automated scan for bias and hallucination
          giskard-cli scan --model-path ./models/v4 --output artifacts/giskard-report.json

  # --- STAGE 3: INFRASTRUCTURE AUDIT (NIST / ISO 27k) ---
  infrastructure-audit:
    name: "OSCAL & Istio Validation"
    needs: ai-governance
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: "Install Lula (Compliance-as-Code Engine)"
        run: curl -L [https://github.com/defenseunicorns/lula/releases/latest/download/lula_linux_amd64](https://github.com/defenseunicorns/lula/releases/latest/download/lula_linux_amd64) -o /usr/local/bin/lula && chmod +x /usr/local/bin/lula

      - name: "Validate Istio Config vs. NIST Controls"
        run: |
          # Lula checks the actual K8s/Istio manifests against OSCAL policies
          lula validate -f lula-validation.yaml --output artifacts/audit-evidence.json

  # --- STAGE 4: ARTIFACT ATTESTATION ---
  attestation:
    name: "Sign & Archive Evidence"
    needs: infrastructure-audit
    runs-on: ubuntu-latest
    steps:
      - name: "Upload All Compliance Artifacts"
        uses: actions/upload-artifact@v4
        with:
          name: compliance-bundle-2026
          path: artifacts/

```