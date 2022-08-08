# kustomize-replacement

eli is testing a demo of the kustomize replacement feature. You can find [kustomize docs on replacement] here.

Normally in Kustomize we include the "base" and the "overlay" resources. Here we don't care about the "overlay" resources except in as much as they provide us a way to swap in some data to the "base". However, Kustomize [eschews] including resources for a yml you don't want built, but we need to include the resource yml for the replacement command to work. That's why "file" and "overlay" are different types.

To run, just `kustomize build .` The full output as of this writing is:

```bash
$ kustomize build .
apiVersion: v1
kind: Namespace
metadata:
  name: file
  stuff:
  - name: one
    runbook: url
  - name: two
    runbook: IT WORKS!
  - name: three
    runbook: url
---
apiVersion: v1
data:
- name: two
  runbook: IT WORKS!
kind: Configmap
metadata:
  name: runbooks
```

[eschews]: https://kubectl.docs.kubernetes.io/faq/kustomize/eschewedfeatures/#removal-directives
[kustomize docs on replacement]: https://kubectl.docs.kubernetes.io/references/kustomize/kustomization/replacements/
