# Response Templates

All responses must use the same language as the original message. Keep group chat replies short, ideally no more than 5 lines.

## Intake Acknowledgement

Vietnamese:

```text
[AIA] Đã nhận báo cáo. Đang phân tích sự cố...
```

English:

```text
[AIA] Report received. Analyzing the incident...
```

## New Jira Issue Created

Vietnamese:

```text
[AIA] Đã tạo: {jira_issue_key} ({severity})
Vấn đề: {title}
Phản hồi trong: {sla_text}
Bước tiếp theo: {next_owner_or_action}
```

English:

```text
[AIA] Created: {jira_issue_key} ({severity})
Issue: {title}
Initial response due: {sla_text}
Next step: {next_owner_or_action}
```

## Duplicate Incident Found

Vietnamese:

```text
[AIA] Sự cố này trùng với {jira_issue_key} đang xử lý.
Đã cập nhật thêm thông tin và phạm vi ảnh hưởng.
Cập nhật tiếp theo: {next_update_text}
```

English:

```text
[AIA] This appears to duplicate {jira_issue_key}, which is already in progress.
I updated the incident with the new report and impact scope.
Next update: {next_update_text}
```

## Ambiguous Bug Confirmation

Vietnamese:

```text
[AIA] Bot nhận thấy đây có thể là lỗi. Bạn có muốn tạo ticket không?
```

English:

```text
[AIA] This may be a bug report. Would you like me to create a ticket?
```

## Not A Bug

Vietnamese:

```text
[AIA] Mình chưa ghi nhận đây là bug report nên chưa tạo ticket.
Bạn có thể dùng /bug kèm mô tả lỗi nếu cần tạo incident.
```

English:

```text
[AIA] I did not detect a bug report, so no ticket was created.
Use /bug with the issue details if you want to create an incident.
```

## Permission Denied

Vietnamese:

```text
[AIA] Bạn không có quyền dùng lệnh này. Vui lòng liên hệ Team Lead hoặc Admin.
```

English:

```text
[AIA] You do not have permission to use this command. Please contact a Team Lead or Admin.
```

## SLA Warning

Vietnamese:

```text
[SLA WARNING] {jira_issue_key} ({severity}) còn {remaining_time}.
{responsible_person} cần phản hồi ngay.
```

English:

```text
[SLA WARNING] {jira_issue_key} ({severity}) has {remaining_time} remaining.
{responsible_person} should respond now.
```

## SLA Breach

Vietnamese:

```text
[SLA BREACH] {jira_issue_key} ({severity}) đã quá hạn phản hồi {delay_text}.
Đã ghi nhận breach log và thông báo cấp xử lý tiếp theo.
```

English:

```text
[SLA BREACH] {jira_issue_key} ({severity}) is overdue by {delay_text}.
Breach log recorded and next escalation level notified.
```

## Resource Suggestion

Vietnamese:

```text
[AIA] Gợi ý điều phối cho {jira_issue_key}:
1. {engineer_1} - {reason_1}
2. {engineer_2} - {reason_2}
3. {engineer_3} - {reason_3}
Cần Team Lead/Manager xác nhận trước khi phân công.
```

English:

```text
[AIA] Resource suggestions for {jira_issue_key}:
1. {engineer_1} - {reason_1}
2. {engineer_2} - {reason_2}
3. {engineer_3} - {reason_3}
Team Lead/Manager confirmation is required before assignment.
```

