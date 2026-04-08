---

3. Vulnerability Intelligence (CRA)
Tool: OpenVEX
Artefact: security_advisory.vex.json
Mapping: CRA (Vulnerability Reachability)

---

```json
JSON
{
  "@context": "[https://openvex.dev/ns/v0.2.0](https://openvex.dev/ns/v0.2.0)",
  "id": "VEX-2026-001",
  "author": "Security Engineering Team",
  "timestamp": "2026-04-07T15:30:00Z",
  "statements": [
    {
      "vulnerability": "CVE-2024-XXXXX",
      "products": ["pkg:pypi/transformers@4.48.0"],
      "status": "not_affected",
      "justification": "vulnerable_code_not_present",
      "impact_statement": "The vulnerable function 'unsafe_load' is deprecated and not called by our inference logic."
    }
  ]
}
```