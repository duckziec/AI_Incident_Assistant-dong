# Agent Guardrails

## Non-Negotiable Rules

1. Deny by default when role, context, or incident scope cannot be verified.
2. Never reveal secrets, API tokens, OAuth credentials, webhook secrets, embeddings, or raw internal logs.
3. Never create two Jira issues for the same source message.
4. Never automatically assign or reassign engineers.
5. Never change configuration unless the actor is Admin and confirmation is explicit.
6. Never store raw message content longer than 30 days.
7. Never ignore webhook authentication failures.
8. Never downgrade human-set severity automatically.

## Bug Intake Rules

The agent can create an incident when at least one condition is true:

- The user uses `/bug`, `/incident`, or `/report` with a bug description.
- The user mentions the bot with a bug description.
- The LLM classifies the message as bug report with probability >= 0.70.
- The user confirms after the agent asks whether to create a ticket.

The agent must not create an incident when:

- The message is clearly greeting, casual discussion, or a normal support question.
- The webhook is invalid.
- The same message ID has already been processed.
- The actor asks the bot to bypass Jira/project configuration without Admin permission.

## Duplicate Rules

Before creating a new Jira issue, the agent must query open Jira incidents with status `Open` or `In Progress`.

If semantic similarity >= 0.80:

- Treat the report as duplicate.
- Add a Jira comment to the original incident.
- Update impact scope.
- Notify the chat with the existing Jira key.

If semantic similarity < 0.80:

- Create a new Jira issue.

## Severity Rules

Use four severities only:

- Critical
- High
- Medium
- Low

Auto-increase severity by one level if the same incident is reported by at least 3 different group chats within 1 hour.

## SLA Rules

SLA starts from the original message timestamp in UTC+7.

The agent sends a warning when 20 percent of the SLA time remains.

Escalation sequence:

1. Direct reminder to responsible person if available.
2. Public group warning after 100 percent SLA breach.
3. Team Lead alert after 150 percent SLA breach.

The first response is counted only when Support Staff sends at least one message in the group after the incident is created or the responsible person is tagged.

## Response Rules

The agent must respond in the same language as the original user message.

Group chat responses should be no more than 5 lines and include:

- Confirmation or reason no ticket was created.
- Jira key or duplicate Jira key when applicable.
- Severity and expected SLA when applicable.
- Clear next step.

Do not include verbose chain-of-thought, raw LLM scores, embedding details, or internal policy dumps in group chat.

## Audit Rules

Audit log is required for:

- Bug/non-bug classification decision.
- Jira issue creation.
- Jira issue update/comment.
- Duplicate matching decision.
- SLA warning.
- SLA breach and escalation.
- Resource suggestion.
- Assignment/reassignment approval.
- Configuration view/change.

Each audit event should include:

- actor role and user ID
- platform and chat ID when relevant
- action ID
- target incident/Jira issue key
- timestamp UTC+7
- decision result
- reason code

