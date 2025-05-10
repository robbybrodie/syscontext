```mermaid
graph TD
    %% Black-box internal system
    OpenShift["OpenShift Platform"]

    %% Human roles
    Developer(("Developer"))
    PlatformAdmin(("Platform Admin"))
    SecurityTeam(("Security Team"))
    Operations(("Operations"))

    %% External systems
    GitHub["GitHub Enterprise"]
    Ping["PING Identity"]
    SplunkSIEM["Splunk SIEM"]
    SplunkLogging["Splunk Logging"]
    ServiceNowInc["ServiceNow Incident Management"]
    ServiceNowReq["ServiceNow Request Management"]
    Venafi["Venafi Certificate Management"]
    DNS["Corporate DNS"]
    Monitoring["Monitoring Platform"]
    EmailService["Email Notification System"]
    ArtifactRepo["Artifact Repository"]
    CMDB["ServiceNow CMDB"]

    %% Interactions
    Developer -->|"CI/CD pipelines, GitOps"| OpenShift
    PlatformAdmin -->|"Cluster config, RBAC"| OpenShift
    SecurityTeam -->|"Security alert review"| OpenShift
    Operations -->|"Ops support & triage"| OpenShift

    OpenShift -->|"OIDC federation via Keycloak"| Ping
    OpenShift -->|"Log forwarding"| SplunkLogging
    OpenShift -->|"Security events"| SplunkSIEM
    OpenShift -->|"Incident tickets"| ServiceNowInc
    OpenShift -->|"Service requests"| ServiceNowReq
    OpenShift -->|"Cert issuance via cert-manager"| Venafi
    OpenShift -->|"DNS registration"| DNS
    OpenShift -->|"Metrics export"| Monitoring
    OpenShift -->|"Webhook sync"| GitHub
    OpenShift -->|"Pull artifacts"| ArtifactRepo
    OpenShift -->|"CMDB updates"| CMDB
    OpenShift -->|"Email alerts"| EmailService
