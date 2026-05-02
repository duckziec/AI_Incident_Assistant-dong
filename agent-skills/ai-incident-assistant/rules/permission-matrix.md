# Permission Matrix

This matrix summarizes who can do what in AI Incident Assistant. The machine-readable source of truth is `permissions.yaml`.

## Roles

| Role | Meaning |
|---|---|
| Customer | User who reports bugs in Telegram/Zalo group chat. |
| Support Staff | Staff member who responds to customers and handles first-line incident flow. |
| Engineer | Technical owner who investigates and fixes incidents. |
| Team Lead | Operational approver for resource coordination and SLA escalation recipient. |
| Manager | Manager who monitors SLA reports and resource allocation. |
| Admin | System administrator who manages configuration and integrations. |
| AIA Bot | Automated system actor. |

## Command Permissions

| Command | Customer | Support | Engineer | Team Lead | Manager | Admin | Notes |
|---|---:|---:|---:|---:|---:|---:|---|
| `/bug [description]` | Yes | Yes | Yes | Yes | Yes | Yes | Incident intake. |
| `/incident [description]` | Yes | Yes | Yes | Yes | Yes | Yes | Alias of `/bug`. |
| `/report [description]` | Yes | Yes | Yes | Yes | Yes | Yes | Incident intake if the intent is a bug report. |
| `/status PROJ-xxx` | Limited | Yes | Yes | Yes | Yes | Yes | Customer only sees incidents linked to their chat. |
| `/report sla` | No | Yes | No | Policy | Yes | Yes | Team Lead optional by organization policy. |
| `/suggest PROJ-xxx` | No | No | No | Yes | Yes | Yes | AI suggests people, does not assign. |
| `/reassign PROJ-xxx` | No | No | No | Yes | Yes | Yes | Human-approved assignment flow only. |
| `/incidents` | No | Yes | No | Policy | Yes | Yes | Team Lead optional by organization policy. |
| `/config` | No | No | No | No | No | Yes | Admin only. Requires audit and confirmation. |

## Automated AI Permissions

| Action | AI May Do Automatically | Conditions |
|---|---:|---|
| Classify inbound message | Yes | Webhook is validated. |
| Ask whether to create ticket | Yes | Bug probability is uncertain. |
| Create Jira issue | Yes | Bug probability >= 0.70 or user confirms, no duplicate found, Jira healthy. |
| Add comment to duplicate Jira issue | Yes | Similarity >= 0.80 and target issue is open. |
| Send SLA warning | Yes | Incident open, no first response, 20 percent SLA time remains. |
| Escalate SLA breach | Yes | SLA breached and no first response. |
| Suggest engineers | Yes | Trigger condition met and requester/recipient scope is valid. |
| Assign or reassign engineer | No | Team Lead or Manager approval required. |
| Change system configuration | No | Admin approval required. |
| Reveal secrets or raw private logs | No | Always forbidden. |

## Access Boundaries

Customers can see the Jira key, severity, expected SLA, and public status for incidents linked to their chat. They must not see internal workload, global SLA reports, raw audit logs, or configuration.

Support Staff can see and act on support-scope incidents and SLA reports. They cannot change system config or approve automatic assignment unless they also have a Team Lead or Manager role.

Engineers can see incidents assigned to them or visible in their Jira project scope. They do not automatically receive global reports or admin config access.

Team Leads and Managers can request resource suggestions and approve assignment changes. Admin-only configuration remains outside their permission unless they also hold Admin.

Admins can manage configuration, integration credentials, thresholds, and audit access according to privacy policy.

