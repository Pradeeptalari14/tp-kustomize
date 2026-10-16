# Kustomize Declarative Overlays Studio (tp-kustomize)

[![SLSA Level 3](https://img.shields.io/badge/SLSA-Level%203-success?style=flat-square&logo=sigstore)](https://slsa.dev)
[![DevSecOps 9+](https://img.shields.io/badge/DevSecOps-9%2B%20Pillars-blue?style=flat-square&logo=kubernetes)](https://talaripradeep.info)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=flat-square)](LICENSE)

> **Production Repository:** [`Pradeeptalari14/tp-kustomize`](https://github.com/Pradeeptalari14/tp-kustomize)  
> **Interactive Studio Workspace:** [https://talaripradeep.info/tools/kustomize/](https://talaripradeep.info/tools/kustomize/)  
> **Visual Flow Canvas:** [https://talaripradeep.info/studios/flow/?studio=kustomize](https://talaripradeep.info/studios/flow/?studio=kustomize)  
> **Architecture Center:** [https://talaripradeep.info/architecture/](https://talaripradeep.info/architecture/)

---

## 🏛️ Overview
Template-free declarative Kubernetes configuration management with base/overlay topologies and strategic merge patches.

This repository is built following the **9+ DevSecOps / SRE Governance Principles**:
1. **Cosign SLSA L3**: Keyless container and manifest attestation recorded to Rekor.
2. **Semgrep AST Guardrails**: Pre-commit AST rules preventing taint paths and plaintext credentials.
3. **CycloneDX SBOM**: Syft-generated Software Bill of Materials with Grype zero High/Critical CVE gating.
4. **Kyverno Admission Policies**: Enforcing CIS Kubernetes hardening, non-root users, and read-only filesystems.
5. **eBPF In-Kernel Runtime Observability**: Tetragon tracing and live syscall profiling.
6. **GitOps Zero-Drift Synchronization**: ArgoCD/Flux continuous declarative reconciliation.
7. **MELT Golden Signals**: OpenTelemetry traces, Prometheus metrics, and structured logging.
8. **Automated SRE Remediation**: Self-healing circuits and SLO compliance.
9. **Zero-Trust Microsegmentation**: Strict SPIFFE/mTLS and encrypted storage volumes.

---

## 📄 Primary Configuration: `kustomization.yaml`

```yaml
apiVersion: kustomize.config.k8s.io/v1beta1
kind: Kustomization

resources:
  - ../../base

namespace: production

namePrefix: prod-

commonLabels:
  environment: production
  tier: backend
  owner: sre-platform

images:
  - name: app-backend
    newName: ghcr.io/pradeeptalari14/app-backend
    newTag: v2.4.0

configMapGenerator:
  - name: app-config
    behavior: merge
    literals:
      - LOG_LEVEL=warn
      - ENABLE_TRACING=true
      - RETRY_MAX_ATTEMPTS=5

patchesStrategicMerge:
  - replica-patch.yaml
  - resources-patch.yaml

```

---

## 🚀 Quickstart & Verification

```bash
# 1. Clone repository
git clone https://github.com/Pradeeptalari14/tp-kustomize.git
cd tp-kustomize

# 2. Run verification drill
bash scripts/validate.sh
```

---

## 📜 License
MIT License. Copyright (c) 2026 Talari Pradeep. All rights reserved.
