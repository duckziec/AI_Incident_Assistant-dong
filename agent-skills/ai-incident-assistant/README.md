# AI Incident Assistant Agent Skill

Folder này đóng gói hướng dẫn vận hành cho AI agent của sản phẩm AI Incident Assistant, được rút ra từ SRS `SRS_AI_Incident_Assistant_v1.0.docx`.

Mục tiêu của folder:

- Giúp AI nhận diện, triage, tạo/cập nhật incident và phản hồi group chat đúng quy trình.
- Cung cấp permission rules để AI biết role nào được dùng lệnh nào.
- Tách rõ việc AI được tự động làm, việc AI chỉ được gợi ý, và việc bắt buộc cần người có quyền xác nhận.
- Chuẩn hóa severity, SLA, response style, audit log và privacy guardrails.

## Cấu trúc

```text
agent-skills/ai-incident-assistant/
  SKILL.md
  README.md
  prompts/
    response-templates.md
    triage-extraction.md
  rules/
    agent-guardrails.md
    permission-matrix.md
    permissions.json
    permissions.yaml
    severity-sla.json
    severity-sla.yaml
  schemas/
    incident.schema.json
```

## Cách dùng nhanh

1. Nạp `SKILL.md` làm instruction chính cho AI agent.
2. Nạp `rules/permissions.json` hoặc `rules/permissions.yaml` vào backend/policy layer để kiểm tra quyền trước khi agent thực thi command/action.
3. Dùng `prompts/triage-extraction.md` cho bước LLM triage và structured extraction.
4. Dùng `rules/severity-sla.json` hoặc `rules/severity-sla.yaml` để map severity sang SLA và escalation.
5. Validate output incident bằng `schemas/incident.schema.json`.



## Nguồn yêu cầu

Các rule trong folder này dựa trên các phần chính của SRS:

- F1 Intake & Detection
- F2 AI Triage & Extraction
- F3 Incident Matching
- F4 Jira Sync
- F5 SLA Monitoring & Escalation
- F6 Resource Coordination
- NFR-S4 Phân quyền truy cập
- Phụ lục 8.3 Danh sách lệnh Bot
