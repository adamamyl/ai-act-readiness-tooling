---
5. Automated Audit Validation (Shift-Left)
Tool: Lula
Artefact: lula-validation.yaml
Mapping: Continuous Control Monitoring

---


```yaml
lula-version: v0.2.0
metadata:
  name: validate-encryption-transit
domain:
  type: kubernetes
  spec:
    resources:
      - name: gateway
        resource: gateways.networking.istio.io
payload:
  schema: opa
  rego: |
    package lula
    default validate = false
    # Validate that TLS mode is set to SIMPLE or MUTUAL (not disabled)
    validate {
      some i
      input.gateway[i].spec.servers[_].tls.mode != "PASSTHROUGH"
    }
```