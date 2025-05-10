```mermaid
graph TD;
    %% Black-box internal system
    OpenShift[OpenShift Platform (Black Box)];

    %% Human roles
    Developer((Developer))
    PlatformAdmin((Platform Admin))
    SecurityTeam((Security Team))
    Operations((Operations))

    %% External systems
    GitHub[Source Code Repository (GitHub Enterprise)]
    Ping[PING Identity (Enterprise IAM)]
    SplunkSIEM[Splunk (SIEM)]
    SplunkLogging[Splunk (Log Aggregation)]
    ServiceNowInc[ServiceNow (Incident Management)]
    ServiceNowReq[ServiceNow (Request Management)]
    Venafi[Venafi (Certificate Management)]
    DNS[Corporate DNS]
    Monitoring[External Monitoring Platform]
    EmailService[Email Notification System]
    ArtifactRepo[Artifact Repository (e.g., Nexus/Artifactory)]
    CMDB[ServiceNow CMDB]

    %% Interactions
    Developer -->|CI/CD pipelines, GitOps| OpenShift
    PlatformAdmin -->|Cluster configuration, RBAC| OpenShift
    SecurityTeam -->|Review security alerts| OpenShift
    Operations -->|Operate and triage incidents| OpenShift

    OpenShift -->|OIDC Federation via Keycloak| Ping
    OpenShift -->|Log forwarding| SplunkLogging
    OpenShift -->|Security alerts & correlation| SplunkSIEM
    OpenShift -->|Incident ticketing| ServiceNowInc
    OpenShift -->|Change/Request management| ServiceNowReq
    OpenShift -->|Certificate requests via cert-manager| Venafi
    OpenShift -->|ExternalDNS Operator| DNS
    OpenShift -->|Prometheus Exporters| Monitoring
    OpenShift -->|Webhook & Source sync| GitHub
    OpenShift -->|Artifact pulls| ArtifactRepo
    OpenShift -->|CMDB updates (auto-discovery)| CMDB
    OpenShift -->|Email alerts| EmailService
```
