---

4. Compliance-as-Code (NIST / ISO 27k)
Tool: OSCAL (NIST Standard)
Artefact: component-definition.yaml
Mapping: NIST SP 800-53 / ISO 27001

---

```yaml
component-definition:
  uuid: 654321-abcd-1234-efgh
  metadata:
    title: AI Inference Platform Compliance
    last-modified: "2026-04-07T12:00:00Z"
  components:
    - uuid: 1111-2222-3333
      type: software
      title: Inference API
      description: Production inference endpoint for LLMs.
      control-implementations:
        - uuid: cccc-dddd-eeee
          source: "[https://github.com/nist/oscal-content/800-53-rev5.xml](https://github.com/nist/oscal-content/800-53-rev5.xml)"
          implemented-requirements:
            - control-id: "sc-8.1"
              description: "Transmission Confidentiality: All traffic is TLS 1.3 encrypted via Istio mTLS."
```