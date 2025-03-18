# Build

```mermaid
sequenceDiagram
    participant User/Event
    participant Build Workflow
    participant Nexus

    User/Event->>Build Workflow: Triggers workflow
    Build Workflow->>Nexus: Download packages
    Build Workflow->>Build Workflow: Compile
    Build Workflow->>Build Workflow: Package
    alt Release Build?
        Build Workflow->>Nexus: Upload artifact package
        Build Workflow->>Build Workflow: Generate attestation
    else
        Build Workflow->>Build Workflow: Skip upload
    end
```

# Release

```mermaid
sequenceDiagram
    participant User
    participant Release Workflow
    participant Build Workflow
    participant Nexus
    participant Remedy

    User->>Release Workflow: Triggers workflow
    Release Workflow->>Build Workflow: Call Build Workflow
    Release Workflow->>Nexus: Upload artifacts
    Release Workflow->>Remedy: Create CRQ
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

# Workflow

```mermaid
graph LR
    User --> Jenkins
    Jenkins --> Sonar
    Sonar --> Nexus
    Nexus --> Target
```
