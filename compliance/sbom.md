---

2. Supply Chain Security (CRA)
Tool: Syft / CycloneDX
Artefact: sbom.json
Mapping: EU Cyber Resilience Act (Product Transparency)

---

```json
{
  "bomFormat": "CycloneDX",
  "specVersion": "1.7",
  "serialNumber": "urn:uuid:3e671687-395b-41f5-a30f-a58921a69b79",
  "version": 1,
  "metadata": {
    "timestamp": "2026-04-07T14:00:00Z",
    "component": {
      "type": "application",
      "name": "Agentic-Inference-Engine",
      "version": "4.2.0"
    }
  },
  "components": [
    {
      "type": "library",
      "name": "transformers",
      "version": "4.48.0",
      "purl": "pkg:pypi/transformers@4.48.0",
      "externalReferences": [
        { "type": "vcs", "url": "[https://github.com/huggingface/transformers](https://github.com/huggingface/transformers)" }
      ]
    }
  ]
}
```