# Build

```mermaid
sequenceDiagram
    participant User
    participant Build Workflow
    participant Nexus

    User->>Build Workflow: Triggers workflow
    Build Workflow->>Nexus: Download packages
    Build Workflow->>Build Workflow: Compile code
    Build Workflow->>Nexus: Upload artifact
```

```mermaid
```

# Release

```mermaid
sequenceDiagram
    participant User
    participant Release Workflow
    participant Remedy
    participant Nexus

    User->>Release Workflow: Triggers workflow
    Release Workflow->>Release Workflow: Build artifacts
    Release Workflow->>Remedy: Create CRQ
    Release Workflow->>Nexus: Upload artifacts
```

# Deploy

```mermaid
sequenceDiagram
    participant User
    participant Deploy Workflow
    participant Remedy
    participant Nexus
    participant Target

    User->>Deploy Workflow: Triggers workflow
    Deploy Workflow->>Remedy: Check for valid CRQ
    Deploy Workflow->>Nexus: Download artifacts
    Deploy Workflow->>Target: Deploy artifacts
    Deploy Workflow->>Remedy: Update status of deployment
```
