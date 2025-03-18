# Build

```mermaid
sequenceDiagram
    participant Build Event
    participant Build Workflow
    participant Nexus

    Build Event->>Build Workflow: triggers
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
    participant Release Event
    participant Release Workflow
    participant Build Workflow
    participant Remedy

    Release Event->>Release Workflow: triggers
    Release Workflow->>Build Workflow: Call Build Workflow
    Release Workflow->>Remedy: Create CRQ
```

# Deploy

```mermaid
sequenceDiagram
    participant Deploy Event
    participant Deploy Workflow
    participant Remedy
    participant Nexus
    participant Target

    Deploy Event->>Deploy Workflow: triggers
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
