# 🛠️ Multi-Environment Kubernetes Management with Kustomize

This project demonstrates how to maintain clean, reusable base Kubernetes manifests and patch variations across **Development** and **Production** environments using **Kustomize**—without template engine complexity or code duplication.

## 📂 Layout Architecture

```text
kustomize-project/
├── base/          # Core resources shared across all environments
└── overlays/
    ├── dev/       # Development target adjustments (Name prefixes, unique labels)
    └── prod/      # Production target adjustments (App scaling patches)
```

## 📋 Prerequisites

- A running **Kubernetes Cluster**
- **kubectl v1.14+** (Kustomize is natively integrated directly into the `kubectl` CLI tool)

## 🚀 How to Run and Deploy

### 1. Inspect Environment Outputs
Generate and review compiled YAML files on your terminal screen without changing your cluster state:

- **For Development:**
  ```bash
  kubectl kustomize overlays/dev
  ```
- **For Production:**
  ```bash
  kubectl kustomize overlays/prod
  ```

### 2. Apply to Cluster
Deploy the specific environment infrastructure you need with a single flag command:

- **Deploy Development:**
  ```bash
  kubectl apply -k overlays/dev
  ```
- **Deploy Production:**
  ```bash
  kubectl apply -k overlays/prod
  ```

### 3. Tear Down Infrastructure
To remove all environment assets safely:
```bash
kubectl delete -k overlays/dev
```

## 🔑 Key Features Demonstrated
- **Base/Overlay Separation:** Keeping structural code DRY (Don't Repeat Yourself).
- **Name Mutation:** Using `namePrefix` to cleanly isolate development namespaces and services (`dev-web-app` vs `prod-web-app`).
- **Strategic Merge Patches:** Overriding deployment values safely (e.g., boosting replica scale to `5` only inside production).
