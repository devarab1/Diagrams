# Diagrams

sequenceDiagram
    participant User
    participant BuildWorkflow
    participant ArtifactRepository

    User->>BuildWorkflow: Trigger build workflow
    BuildWorkflow->>BuildWorkflow: Compile code
    BuildWorkflow->>ArtifactRepository: Upload artifact
