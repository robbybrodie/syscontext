```mermaid
graph LR;
    %% Black-box internal system
    OpenShift[OpenShift Platform (Black Box)]

    %% Human roles
    subgraph Human Actors
        Developer((Developer))
        PlatformAdmin((Platform Admin))
        SecurityTeam((Security Team))
        Operations((Operations))
    end

    %% External Systems
    subgraph Identity & Access Management
        Ping[PING Identity (Enterprise IAM)]
    end

    subgraph Observability & Monitoring
        SplunkSIEM[Splunk (SIEM)]
        SplunkLogging[Splunk (Log Aggregation)]
        Monitoring[External Monitoring Platform]
        EmailService[Email Notification System]
    end

    subgraph ITSM & CMDB
        ServiceNowInc[ServiceNow (Incident Mgmt)]
        ServiceNowReq[ServiceNow (Request Mgmt)]
        CMDB[ServiceNow CMDB]
    end

    subgraph DevOps Tooling
        GitHub[Source Code Repository]
        ArtifactRepo[Artifact Repo (Nexus/Artifactory)]
    end

    subgraph Infrastructure Integration
        Venafi[Venafi (Cert Mgmt)]
        DNS[Corporate DNS]
    end

    %% Interactions
    Developer -->|CI/CD Pipelines, GitOps| OpenShift
    PlatformAdmin -->|Cluster Config, RBAC| OpenShift
    SecurityTeam -->|Reviews Security Events| OpenShift
    Operations -->|Incident Handling| OpenShift

    OpenShift -->|OIDC via Keycloak| Ping
    OpenShift -->|Log Forwarding| SplunkLogging
    OpenShift -->|Security Alerts| SplunkSIEM
    OpenShift -->|Monitoring Exporters| Monitoring
    OpenShift -->|Email Alerts| EmailService

    OpenShift -->|Incident Tickets| ServiceNowInc
    OpenShift -->|Requests / Changes| ServiceNowReq
    OpenShift -->|Auto-Discovery Updates| CMDB

    OpenShift -->|Webhook / Source Sync| GitHub
    OpenShift -->|Pull Artifacts| ArtifactRepo

    OpenShift -->|Cert Requests| Venafi
    OpenShift -->|External DNS Updates| DNS
```
