# Kustomize inheritance test

- The `common/` kustomization defines a `namespace` and some labels, and includes a common configmap + the namespace definition itself.
- The `svc1/base` kustomization inherits from `common/` and defines a configmap for svc1.
- The `svc1/overlays/test` kustomization inherits from `svc1/base` and defines a test environment specific configmap for svc1.

Observed behavior:

- `kustomize build common/` correctly creates the namespace, and the created configmap has the correct namespace and labels set.
- `kustomize build svc1/base` correctly creates the namespace from the `common/` manifest and the common configmap has the correct namespace and labels set, but the svc1 config map does not have a namespace set nor any labels.
- `kustomize build svc1/overlays/test` has the same behavior as `svc1/base/`; namespace is created, common configmap has correct namespace and labels, but any svc1 specific resources does not have labels or namespace set.
