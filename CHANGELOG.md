# Changelog

All notable changes to the Helm Daily Drill are documented in this file.

The drill evolves incrementally. Each version reflects an intentional expansion
of the same lifecycle-based exercise.

---

## v0.1 — Initial Lifecycle Drill

**Date:** 2025-12-30

### Added
- Namespace-based workflow (`drill`)
- Helm repository setup (Bitnami)
- Release lifecycle:
  - `helm install`
  - `helm upgrade`
  - `helm rollback`
  - `helm uninstall`
- Release inspection:
  - `helm list`
  - `helm status`
  - `helm history`
- Rendering and validation:
  - `helm template`
  - `helm upgrade --dry-run --debug`
- Full cleanup via namespace deletion

### Notes
- This version establishes the core lifecycle drill.
- All future steps build on this flow without changing its structure.

