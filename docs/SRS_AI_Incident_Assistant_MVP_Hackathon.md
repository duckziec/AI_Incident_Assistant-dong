# SRS – AI Incident Assistant

**Software Requirements Specification**  
**Chuẩn IEEE 830-1998 | Phiên bản 1.0 | MVP Hackathon 24h | Tháng 5, 2026**

---

| Trường | Giá trị |
|---|---|
| Tên hệ thống | AI Incident Assistant |
| Tên demo sản phẩm | AI Incident Copilot |
| Phiên bản | 1.0 |
| Ngày soạn thảo | Tháng 5, 2026 |
| Chuẩn áp dụng | IEEE 830-1998 |
| Trạng thái | Bản nháp chính thức cho Hackathon |
| Ngôn ngữ hệ thống | Tiếng Việt, có thể mở rộng sang tiếng Anh |
| Platform MVP | Telegram Group / Web Demo mô phỏng group chat |
| Hệ thống ticket | Mock Jira Board, có thể mở rộng sang Jira REST API |
| Phạm vi MVP | Text-only, 1 Jira project, severity P1/P2/P3 |
| Nhóm thực hiện | [Tên đội] |
| Đối tượng sử dụng | SMEs, team hỗ trợ kỹ thuật, CSKH, IT support, team lead |

---

## Lịch sử thay đổi

| Phiên bản | Ngày | Mô tả | Người thực hiện |
|---|---|---|---|
| 1.0 | 05/2026 | Bản SRS khởi tạo cho MVP Hackathon 24h dựa trên đề tài AI Incident Assistant | Nhóm phát triển |
| 1.1 | Sau Hackathon | Cập nhật nếu tích hợp Jira REST API thật hoặc mở rộng thêm Zalo/Slack | Nhóm phát triển |

---

## Mục lục

1. [Giới thiệu](#1-giới-thiệu)  
   - 1.1 [Mục đích](#11-mục-đích-purpose)  
   - 1.2 [Phạm vi hệ thống](#12-phạm-vi-hệ-thống-scope)  
   - 1.3 [Định nghĩa và từ viết tắt](#13-định-nghĩa-từ-viết-tắt-và-ký-hiệu-definitions)  
   - 1.4 [Tài liệu tham khảo](#14-tài-liệu-tham-khảo-references)  
   - 1.5 [Tổng quan tài liệu](#15-tổng-quan-tài-liệu-overview)  

2. [Mô tả tổng quan hệ thống](#2-mô-tả-tổng-quan-hệ-thống)  
   - 2.1 [Bối cảnh hệ thống](#21-bối-cảnh-hệ-thống-system-context)  
   - 2.2 [Các tác nhân](#22-các-tác-nhân-actors--stakeholders)  
   - 2.3 [Chức năng tổng quát](#23-chức-năng-tổng-quát-general-functions)  
   - 2.4 [Đặc điểm người dùng](#24-đặc-điểm-người-dùng-user-characteristics)  
   - 2.5 [Ràng buộc tổng quát](#25-ràng-buộc-tổng-quát-general-constraints)  
   - 2.6 [Giả định và phụ thuộc](#26-giả-định-và-phụ-thuộc-assumptions-and-dependencies)  

3. [Yêu cầu chức năng](#3-yêu-cầu-chức-năng)  
   - 3.1 [Module F1 – Tiếp nhận tin nhắn bug](#31-module-f1--tiếp-nhận-tin-nhắn-bug-chat-intake)  
   - 3.2 [Module F2 – AI Triage và trích xuất thông tin](#32-module-f2--ai-triage-và-trích-xuất-thông-tin)  
   - 3.3 [Module F3 – Incident Matching](#33-module-f3--incident-matching-phát-hiện-bug-trùng)  
   - 3.4 [Module F4 – Mock Jira / Jira Sync](#34-module-f4--mock-jira--jira-sync)  
   - 3.5 [Module F5 – SLA và Tagged No-response Watch](#35-module-f5--sla-và-tagged-no-response-watch)  
   - 3.6 [Module F6 – Dispatch Suggestion](#36-module-f6--dispatch-suggestion-gợi-ý-điều-phối-hỗ-trợ)  
   - 3.7 [Module F7 – Web Demo Dashboard](#37-module-f7--web-demo-dashboard)  

4. [Yêu cầu phi chức năng](#4-yêu-cầu-phi-chức-năng)  
   - 4.1 [Hiệu năng](#41-hiệu-năng-performance)  
   - 4.2 [Độ tin cậy](#42-độ-tin-cậy-reliability)  
   - 4.3 [Bảo mật và an toàn AI](#43-bảo-mật-và-an-toàn-ai-security--ai-safety)  
   - 4.4 [Khả năng bảo trì và mở rộng](#44-khả-năng-bảo-trì-và-mở-rộng-maintainability--scalability)  
   - 4.5 [Khả năng sử dụng](#45-khả-năng-sử-dụng-usability)  

5. [Ràng buộc thiết kế và kiến trúc](#5-ràng-buộc-thiết-kế-và-kiến-trúc)  
   - 5.1 [Kiến trúc đề xuất](#51-kiến-trúc-đề-xuất)  
   - 5.2 [Công nghệ gợi ý](#52-công-nghệ-gợi-ý)  
   - 5.3 [Ràng buộc MVP Hackathon](#53-ràng-buộc-mvp-hackathon)  

6. [Mô tả Use Case](#6-mô-tả-use-case)  
   - 6.1 [Danh sách Use Case](#61-danh-sách-use-case)  
   - 6.2 [UC-01 – Báo cáo bug mới từ group chat](#62-uc-01--báo-cáo-bug-mới-từ-group-chat)  
   - 6.3 [UC-02 – Phát hiện và gộp bug trùng](#63-uc-02--phát-hiện-và-gộp-bug-trùng)  
   - 6.4 [UC-03 – Khách tag nhân viên nhưng không phản hồi](#64-uc-03--khách-tag-nhân-viên-nhưng-không-phản-hồi)  
   - 6.5 [UC-04 – Team quá tải và cần đề xuất người hỗ trợ](#65-uc-04--team-quá-tải-và-cần-đề-xuất-người-hỗ-trợ)  
   - 6.6 [UC-05 – Xem trạng thái incident](#66-uc-05--xem-trạng-thái-incident)  
   - 6.7 [UC-06 – Xem tóm tắt incident](#67-uc-06--xem-tóm-tắt-incident)  

7. [Ma trận truy xuất yêu cầu](#7-ma-trận-truy-xuất-yêu-cầu)  

8. [Phụ lục](#8-phụ-lục)  
   - 8.1 [Ví dụ luồng tin nhắn mẫu](#81-ví-dụ-luồng-tin-nhắn-mẫu)  
   - 8.2 [Schema JSON – AI Triage Output](#82-schema-json--ai-triage-output)  
   - 8.3 [Schema dữ liệu tối thiểu](#83-schema-dữ-liệu-tối-thiểu)  
   - 8.4 [Danh sách lệnh bot](#84-danh-sách-lệnh-bot)  
   - 8.5 [Luồng hoạt động tổng quát](#85-luồng-hoạt-động-tổng-quát-flow-diagram)  

---

# 1. Giới thiệu

## 1.1 Mục đích (Purpose)

Tài liệu này là **Đặc tả Yêu cầu Phần mềm (Software Requirements Specification – SRS)** cho hệ thống **AI Incident Assistant**, một giải pháp ứng dụng trí tuệ nhân tạo trong lĩnh vực **Kinh doanh và Quản lý vận hành**, nhằm hỗ trợ doanh nghiệp nhỏ và vừa xử lý các sự cố kỹ thuật phát sinh trong group chat khách hàng.

Mục tiêu của tài liệu là:

- Xác định rõ phạm vi, chức năng và hành vi mong đợi của hệ thống.
- Làm cơ sở để nhóm phát triển xây dựng MVP trong Hackathon 24h.
- Làm tài liệu tham chiếu cho báo cáo, slide, video demo và kiểm thử sản phẩm.
- Giúp ban giám khảo hiểu rõ hệ thống giải quyết vấn đề gì, AI được ứng dụng ở đâu và MVP chứng minh được giá trị nào.
- Phân biệt rõ giữa phần **MVP/mô phỏng** và phần **có thể triển khai thực tế sau Hackathon**.

**Đối tượng đọc tài liệu:**

| Đối tượng | Mục đích đọc |
|---|---|
| Nhóm phát triển | Hiểu yêu cầu để code/demo đúng phạm vi |
| Nhóm business/pitch | Viết báo cáo, slide, script demo |
| Ban giám khảo | Đánh giá tính sáng tạo, khả thi, ứng dụng AI |
| Doanh nghiệp SMEs | Hiểu cách hệ thống có thể áp dụng vào vận hành hỗ trợ kỹ thuật |
| Team Lead/Manager | Hiểu cách hệ thống giúp theo dõi SLA và điều phối nhân sự |

---

## 1.2 Phạm vi hệ thống (Scope)

**AI Incident Assistant** là một bot AI hoạt động như một **lớp trung gian thông minh** giữa group chat hỗ trợ khách hàng và hệ thống quản lý issue như Jira.

Trong thực tế, khách hàng thường báo lỗi trực tiếp trong group chat thay vì tạo ticket chuẩn. Điều này khiến doanh nghiệp dễ bị trôi tin nhắn, tạo nhiều ticket trùng, phản hồi chậm và không theo dõi được SLA. Hệ thống được thiết kế để xử lý khoảng trống này bằng cách biến tin nhắn tự nhiên trong group chat thành incident có cấu trúc.

### Phạm vi MVP Hackathon 24h bao gồm:

- Tiếp nhận tin nhắn bug từ **Telegram group** hoặc **web demo mô phỏng group chat**.
- Hỗ trợ xử lý **text-only**.
- Nhận diện tin nhắn có phải bug/incident hay không.
- Dùng AI để trích xuất:
  - Tiêu đề lỗi.
  - Tóm tắt lỗi.
  - Module liên quan.
  - Mức độ nghiêm trọng.
  - Phạm vi ảnh hưởng.
  - Gợi ý phản hồi khách hàng.
- Phân loại severity theo **P1 / P2 / P3**.
- Kiểm tra bug mới hay bug trùng với incident đang mở.
- Tạo ticket mới hoặc cập nhật ticket cũ trên **Mock Jira Board**.
- Theo dõi SLA phản hồi theo severity.
- Theo dõi tình huống khách hàng tag nhân viên nhưng người đó không phản hồi.
- Đề xuất người hỗ trợ phù hợp khi team hiện tại quá tải.
- Hiển thị toàn bộ quy trình trên web demo.

### Ngoài phạm vi MVP:

- Không xử lý hình ảnh, voice, file log.
- Không tự động sửa lỗi code.
- Không rollback production.
- Không tự động tắt dịch vụ.
- Không tự động điều chuyển nhân sự giữa các team nếu chưa có phê duyệt.
- Không tự động thêm người vào group khách hàng.
- Không đánh giá hiệu suất cá nhân.
- Không thay thế Jira.
- Không xây dựng dashboard vận hành phức tạp.
- Không tối ưu workforce toàn công ty.
- Không bắt buộc tích hợp Jira thật trong Hackathon.

---

## 1.3 Định nghĩa, từ viết tắt và ký hiệu (Definitions)

| Thuật ngữ / Từ viết tắt | Định nghĩa |
|---|---|
| **AIA** | AI Incident Assistant – tên hệ thống trong tài liệu này. |
| **AI Incident Copilot** | Tên demo/phiên bản trình diễn của hệ thống. |
| **SME** | Small and Medium-sized Enterprise – Doanh nghiệp nhỏ và vừa. |
| **Bug** | Lỗi phần mềm hoặc lỗi chức năng được khách hàng báo cáo. |
| **Incident** | Sự cố có ảnh hưởng đến người dùng, hệ thống hoặc hoạt động kinh doanh. |
| **Triage** | Quá trình phân loại, tóm tắt và đánh giá mức độ nghiêm trọng của bug/incident. |
| **SLA** | Service Level Agreement – Cam kết thời gian phản hồi hoặc xử lý. |
| **Jira** | Hệ thống quản lý issue/ticket phổ biến trong các đội kỹ thuật. |
| **Mock Jira** | Bảng Jira giả lập dùng trong MVP để mô phỏng tạo/cập nhật ticket. |
| **Ticket** | Bản ghi chính thức của một bug/incident trong hệ thống quản lý issue. |
| **P1/P2/P3** | Ba mức độ nghiêm trọng trong MVP: P1 nghiêm trọng nhất, P3 nhẹ nhất. |
| **Incident Matching** | Quá trình xác định bug mới có trùng với incident đang mở hay không. |
| **Duplicate / Dedupe** | Bug trùng / quá trình gộp bug trùng để tránh tạo nhiều ticket. |
| **Tagged No-response Watch** | Cơ chế theo dõi khi khách hàng tag nhân viên nhưng nhân viên không phản hồi. |
| **Dispatch Suggestion** | Gợi ý người hỗ trợ phù hợp dựa trên kỹ năng, workload và trạng thái sẵn sàng. |
| **Workload** | Khối lượng công việc hiện tại của một nhân sự, ví dụ số issue đang xử lý. |
| **LLM** | Large Language Model – mô hình ngôn ngữ lớn dùng để phân tích tin nhắn. |
| **JSON Output** | Đầu ra có cấu trúc để hệ thống có thể đọc và xử lý tiếp. |
| **Web Demo** | Giao diện web dùng để mô phỏng hoạt động của hệ thống trong Hackathon. |
| **Approval Required** | Trạng thái yêu cầu team lead phê duyệt trước khi bot thực hiện hành động rủi ro. |

---

## 1.4 Tài liệu tham khảo (References)

- IEEE Std 830-1998 – IEEE Recommended Practice for Software Requirements Specifications.
- Báo cáo ý tưởng: **AI Incident Assistant – Bot AI hỗ trợ tiếp nhận bug, gom incident, đồng bộ Jira, theo dõi SLA và điều phối hỗ trợ kỹ thuật trong các group chat với khách hàng**.
- Tài liệu Telegram Bot API.
- Tài liệu Jira REST API.
- Tài liệu OpenAI API hoặc LLM provider tương đương.
- Quy định Hackathon Vòng 2: báo cáo tối đa 15 trang, có thể kèm demo code/prototype/dataset/video.

---

## 1.5 Tổng quan tài liệu (Overview)

Tài liệu này được tổ chức theo cấu trúc SRS gồm 8 phần:

| Phần | Nội dung |
|---|---|
| Phần 1 | Giới thiệu mục đích, phạm vi, thuật ngữ và tài liệu tham khảo |
| Phần 2 | Mô tả tổng quan hệ thống, bối cảnh, actor và chức năng chính |
| Phần 3 | Đặc tả yêu cầu chức năng theo từng module F1–F7 |
| Phần 4 | Yêu cầu phi chức năng về hiệu năng, bảo mật, khả năng dùng và mở rộng |
| Phần 5 | Ràng buộc thiết kế, kiến trúc và công nghệ đề xuất |
| Phần 6 | Use Case chi tiết cho các luồng demo chính |
| Phần 7 | Ma trận truy xuất yêu cầu |
| Phần 8 | Phụ lục gồm ví dụ hội thoại, schema JSON, command bot và flow diagram |

---

# 2. Mô tả tổng quan hệ thống

## 2.1 Bối cảnh hệ thống (System Context)

Trong nhiều doanh nghiệp phần mềm hoặc dịch vụ số, khách hàng thường không báo lỗi qua cổng ticket chuẩn ngay từ đầu. Thay vào đó, họ gửi tin nhắn trực tiếp trong các group chat hỗ trợ. Các tin nhắn này thường ngắn, rời rạc và không có cấu trúc.

Ví dụ:

```text
app không login được
nhiều user bên em bị
team check gấp giúp anh
@Minh xem giúp lỗi thanh toán
```

Những tin nhắn này nếu không được xử lý kịp thời sẽ dẫn đến:

- Bug bị trôi trong group chat.
- Nhiều mô tả khác nhau nhưng cùng một lỗi.
- Tạo nhiều ticket trùng.
- Không biết lỗi nào nghiêm trọng nhất.
- Chậm phản hồi khách hàng.
- Không ai theo dõi SLA.
- Lead chỉ biết vấn đề khi sự cố đã lớn.
- Khách hàng tag đúng người nhưng vẫn bị im lặng.
- Team hiện tại quá tải nhưng chưa có cơ chế điều phối hỗ trợ.

**AI Incident Assistant** giải quyết vấn đề này bằng cách đứng trước Jira như một lớp AI đầu vào:

```text
Group Chat / Web Demo
        ↓
AI Incident Assistant
        ↓
AI Triage + Incident Matching
        ↓
Mock Jira / Jira
        ↓
SLA Watch + Dispatch Suggestion
```

---

## 2.2 Các tác nhân (Actors / Stakeholders)

| Tác nhân | Vai trò | Tương tác với hệ thống |
|---|---|---|
| **Khách hàng** | Người báo lỗi trong group chat | Gửi tin nhắn bug, tag nhân viên, nhận phản hồi từ bot |
| **AIA Bot** | Tác nhân chính của hệ thống | Nhận tin nhắn, phân tích AI, tạo/gộp ticket, nhắc SLA |
| **Nhân viên hỗ trợ** | Người phản hồi khách hàng | Nhận nhắc nhở, xác nhận đã tiếp nhận, cập nhật tình trạng |
| **Kỹ sư kỹ thuật** | Người xử lý lỗi | Nhận ticket hoặc được đề xuất hỗ trợ |
| **Team Lead** | Người quản lý xử lý incident | Nhận escalation, phê duyệt điều phối, theo dõi workload |
| **Mock Jira Board** | Hệ thống ticket giả lập | Lưu ticket SUP-101, SUP-102 trong MVP |
| **Jira thật** | Hệ thống issue thực tế sau MVP | Có thể tích hợp qua Jira REST API |
| **Web Demo** | Giao diện trình diễn MVP | Cho phép nhập bug, xem AI output, ticket board, SLA, dispatch |

---

## 2.3 Chức năng tổng quát (General Functions)

AIA gồm 7 nhóm chức năng chính:

| Module | Tên | Mô tả ngắn |
|---|---|---|
| **F1** | Chat Intake | Tiếp nhận tin nhắn bug từ group chat hoặc web demo |
| **F2** | AI Triage & Extraction | Dùng AI phân tích tin nhắn và trích xuất thông tin có cấu trúc |
| **F3** | Incident Matching | Xác định bug mới hay bug trùng với incident đang mở |
| **F4** | Mock Jira / Jira Sync | Tạo ticket mới hoặc cập nhật ticket cũ |
| **F5** | SLA & Tagged Watch | Theo dõi SLA và tình huống khách tag người nhưng không phản hồi |
| **F6** | Dispatch Suggestion | Đề xuất người hỗ trợ khi team hiện tại quá tải |
| **F7** | Web Demo Dashboard | Hiển thị toàn bộ luồng demo cho giám khảo |

---

## 2.4 Đặc điểm người dùng (User Characteristics)

### 2.4.1 Khách hàng

- Không nhất thiết có kiến thức kỹ thuật.
- Thường mô tả lỗi bằng ngôn ngữ tự nhiên.
- Có thể viết tắt, viết không đầy đủ, dùng từ đời thường.
- Thường muốn được phản hồi nhanh.
- Không quan tâm quy trình Jira nội bộ của doanh nghiệp.

Ví dụ:

```text
app bị lỗi rồi anh ơi
không thanh toán được
login cứ xoay vòng mãi
```

### 2.4.2 Nhân viên hỗ trợ

- Cần đọc nhiều group chat cùng lúc.
- Cần biết lỗi nào nghiêm trọng để ưu tiên.
- Có thể bị quá tải khi nhiều khách hàng báo lỗi cùng lúc.
- Cần bot giúp tóm tắt và ghi nhận incident.

### 2.4.3 Kỹ sư kỹ thuật

- Cần thông tin bug có cấu trúc.
- Cần biết module lỗi, severity, mô tả, phạm vi ảnh hưởng.
- Không muốn nhận nhiều ticket trùng cho cùng một incident.

### 2.4.4 Team Lead / Manager

- Cần biết incident nào đang mở.
- Cần biết ai đang xử lý.
- Cần biết SLA nào sắp trễ hoặc đã trễ.
- Cần gợi ý điều phối khi team hiện tại quá tải.
- Không muốn bot tự ý ra quyết định rủi ro cao.

---

## 2.5 Ràng buộc tổng quát (General Constraints)

- MVP phải hoàn thành trong khung thời gian Hackathon 24h.
- Hệ thống phải có thể demo được bằng web app hoặc prototype.
- Hệ thống không bắt buộc phải kết nối Telegram/Jira thật nếu đã có mock hợp lý.
- Dữ liệu sử dụng trong demo phải là dữ liệu giả lập, không dùng dữ liệu khách hàng thật.
- Bot chỉ được đề xuất điều phối, không được tự điều chuyển nhân sự.
- Bot không được thực hiện hành động rủi ro như rollback production, tắt dịch vụ hoặc đánh giá nhân viên.
- Các hành động có rủi ro phải có trạng thái **Approval Required**.
- Web demo phải trình bày rõ luồng: **Chat → AI → Ticket → SLA → Dispatch**.

---

## 2.6 Giả định và phụ thuộc (Assumptions and Dependencies)

### Giả định

- Doanh nghiệp mục tiêu là SME cung cấp phần mềm hoặc dịch vụ số.
- Doanh nghiệp có nhiều group chat hỗ trợ khách hàng.
- Doanh nghiệp đang dùng hoặc có thể dùng Jira để quản lý issue.
- Trong MVP, Jira có thể được mô phỏng bằng mock board.
- Team có dataset giả lập gồm 15–20 tin nhắn bug.
- Team có bảng nhân sự giả lập gồm tên, kỹ năng, trạng thái và workload.
- Team có thể sử dụng AI API hoặc mock AI output nếu API không ổn định.

### Phụ thuộc

| Thành phần | Phụ thuộc |
|---|---|
| AI Triage | OpenAI API hoặc logic mock/rule-based |
| Chat Intake | Telegram Bot API hoặc web demo input |
| Ticket Board | Mock Jira board / Google Sheet / SQLite / Supabase |
| SLA Watch | Timestamp và severity của incident |
| Dispatch Suggestion | Bảng team_members giả lập |
| Demo | Máy tính chạy local web hoặc video demo |

---

# 3. Yêu cầu chức năng

> **Quy ước mức độ bắt buộc:**  
> **PHẢI (MUST):** Bắt buộc trong MVP.  
> **NÊN (SHOULD):** Nên có nếu đủ thời gian.  
> **CÓ THỂ (MAY):** Tùy chọn, có thể triển khai sau Hackathon.

---

## 3.1 Module F1 – Tiếp nhận tin nhắn bug (Chat Intake)

### 3.1.1 Nguồn đầu vào

**FR-F1-01:** Hệ thống **PHẢI** cho phép người dùng nhập tin nhắn bug thông qua web demo.

**FR-F1-02:** Hệ thống **NÊN** hỗ trợ nhận tin nhắn từ Telegram Bot nếu team có đủ thời gian tích hợp.

**FR-F1-03:** Hệ thống **PHẢI** hỗ trợ chạy demo bằng dataset mẫu trong trường hợp không kết nối Telegram thật.

**FR-F1-04:** Hệ thống **PHẢI** chỉ xử lý tin nhắn văn bản trong MVP.

**FR-F1-05:** Hệ thống **KHÔNG PHẢI** xử lý ảnh, voice, file log hoặc attachment trong MVP.

---

### 3.1.2 Cách kích hoạt bot

**FR-F1-06:** Hệ thống **PHẢI** nhận diện các dạng kích hoạt bug report sau:

| Phương thức | Ví dụ | Mức độ |
|---|---|---|
| Slash command | `/bug app không login được` | Must |
| Mention bot | `@bot bên em lỗi thanh toán` | Should |
| Tin nhắn tự nhiên | `nhiều user bên em không vào app được` | Must |
| Tag nhân viên | `@Minh check giúp lỗi payment` | Must |

---

### 3.1.3 Metadata tin nhắn

**FR-F1-07:** Khi nhận tin nhắn, hệ thống **PHẢI** lưu các metadata sau:

| Trường | Mô tả | Ví dụ |
|---|---|---|
| `message_id` | ID tin nhắn | MSG-001 |
| `group_id` | ID group | G01 |
| `group_name` | Tên group | Support ACME |
| `sender_id` | ID người gửi | CUS-001 |
| `sender_name` | Tên người gửi | Customer A |
| `message_text` | Nội dung tin nhắn | `/bug app không login được` |
| `timestamp` | Thời điểm nhận | 2026-05-02 10:00 |
| `mentioned_user` | Người bị tag | Minh |
| `platform` | Nguồn tin nhắn | Web Demo / Telegram |

---

### 3.1.4 Phản hồi tiếp nhận ban đầu

**FR-F1-08:** Sau khi nhận tin nhắn, hệ thống **PHẢI** hiển thị phản hồi tiếp nhận:

```text
[AIA] ✅ Đã ghi nhận tin nhắn. Đang phân tích sự cố...
```

**FR-F1-09:** Nếu tin nhắn không phải bug, hệ thống **NÊN** hiển thị:

```text
[AIA] Tin nhắn này không được xác định là bug/incident. Không tạo ticket.
```

---

## 3.2 Module F2 – AI Triage và trích xuất thông tin

### 3.2.1 Nhận diện bug report

**FR-F2-01:** Hệ thống **PHẢI** xác định tin nhắn có phải bug/incident hay không.

| Tin nhắn | Kết quả mong muốn |
|---|---|
| `/bug app không login được` | Bug |
| `nhiều user bên em không vào app được` | Bug |
| `@Minh check giúp lỗi payment` | Bug + tagged watch |
| `bên em muốn hỏi cách đổi mật khẩu` | Request thường |
| `hello team` | Không phải bug |

---

### 3.2.2 Trích xuất thông tin có cấu trúc

**FR-F2-02:** Nếu tin nhắn là bug, hệ thống **PHẢI** trích xuất các trường sau:

| Trường | Tên kỹ thuật | Bắt buộc | Mô tả |
|---|---|---|---|
| Có phải bug không | `is_bug_report` | Có | true/false |
| Tiêu đề lỗi | `title` | Có | Tên lỗi ngắn gọn |
| Tóm tắt | `summary` | Có | Tóm tắt nội dung bug |
| Module | `module` | Có | Login/Auth, Payment, API, Mobile... |
| Mức độ nghiêm trọng | `severity` | Có | P1/P2/P3 |
| Phạm vi ảnh hưởng | `affected_scope` | Có | Một user, nhiều user, nhiều group |
| Người bị tag | `tagged_user` | Không | Minh, Huy, Lan... |
| Gợi ý phản hồi | `suggested_reply` | Có | Câu trả lời ngắn cho khách |
| Độ tin cậy | `confidence_score` | Nên có | 0.00–1.00 |

---

### 3.2.3 Đầu ra JSON

**FR-F2-03:** Hệ thống **PHẢI** hiển thị hoặc lưu output AI dưới dạng JSON.

Ví dụ:

```json
{
  "is_bug_report": true,
  "title": "Lỗi đăng nhập app mobile",
  "summary": "Nhiều người dùng không thể đăng nhập vào ứng dụng mobile từ sáng.",
  "module": "Login/Auth",
  "severity": "P1",
  "affected_scope": "Multiple users",
  "tagged_user": null,
  "suggested_reply": "Hệ thống đã ghi nhận sự cố đăng nhập và chuyển đến đội kỹ thuật xử lý. Team sẽ cập nhật trong vòng 30 phút.",
  "confidence_score": 0.92
}
```

---

### 3.2.4 Quy tắc phân loại severity

**FR-F2-04:** Hệ thống **PHẢI** phân loại severity theo 3 mức trong MVP:

| Severity | Tiêu chí | SLA phản hồi | Ví dụ |
|---|---|---:|---|
| P1 | Lỗi nghiêm trọng, ảnh hưởng nhiều user, chức năng lõi như login/payment bị lỗi | 30 phút | Không login được, payment fail toàn bộ |
| P2 | Lỗi trung bình, ảnh hưởng một nhóm nhỏ hoặc có workaround | 2 giờ | Một tính năng phụ lỗi, API chậm |
| P3 | Lỗi nhẹ, request hỗ trợ, không ảnh hưởng chức năng chính | 8 giờ | Hỏi cách đổi mật khẩu, giao diện hiển thị sai nhẹ |

---

### 3.2.5 Gợi ý phản hồi khách hàng

**FR-F2-05:** Hệ thống **PHẢI** tạo câu phản hồi gợi ý phù hợp với severity.

Ví dụ P1:

```text
Chúng tôi đã ghi nhận sự cố nghiêm trọng và chuyển đến đội kỹ thuật xử lý. Team sẽ cập nhật trong vòng 30 phút.
```

Ví dụ P2:

```text
Chúng tôi đã ghi nhận vấn đề và đang kiểm tra. Team sẽ phản hồi trong vòng 2 giờ.
```

Ví dụ P3:

```text
Chúng tôi đã ghi nhận yêu cầu hỗ trợ và sẽ phản hồi trong ngày.
```

---

## 3.3 Module F3 – Incident Matching: Phát hiện bug trùng

### 3.3.1 Kiểm tra incident đang mở

**FR-F3-01:** Sau khi AI triage, hệ thống **PHẢI** kiểm tra danh sách incident đang mở trên Mock Jira Board.

**FR-F3-02:** Hệ thống **PHẢI** xác định bug mới có trùng với incident đang mở hay không.

---

### 3.3.2 Logic matching trong MVP

**FR-F3-03:** Trong MVP, hệ thống **CÓ THỂ** sử dụng rule-based matching thay vì embedding phức tạp.

Rule đề xuất:

```text
Nếu module giống nhau
và keyword chính tương tự
và incident cũ chưa resolved
→ xác định là duplicate
```

Ví dụ:

| Tin nhắn mới | Incident đang mở | Kết quả |
|---|---|---|
| `app không login được` | SUP-101 – Lỗi đăng nhập app mobile | Duplicate |
| `không vào app được` | SUP-101 – Lỗi đăng nhập app mobile | Duplicate |
| `xoay vòng ở màn hình đăng nhập` | SUP-101 – Lỗi đăng nhập app mobile | Duplicate |
| `không thanh toán được` | SUP-101 – Lỗi đăng nhập app mobile | New incident |

---

### 3.3.3 Xử lý bug trùng

**FR-F3-04:** Nếu phát hiện duplicate, hệ thống **PHẢI**:

1. Không tạo ticket mới.
2. Gắn tin nhắn mới vào ticket cũ.
3. Tăng `mention_count`.
4. Tăng `affected_group_count` nếu tin nhắn đến từ group mới.
5. Cập nhật `last_seen`.
6. Hiển thị thông báo duplicate.

Thông báo mẫu:

```text
[AIA] 🔄 Duplicate detected.
Linked to: SUP-101
Affected groups updated: 1 → 2
```

---

### 3.3.4 Xử lý bug mới

**FR-F3-05:** Nếu không tìm thấy duplicate, hệ thống **PHẢI** tạo incident mới.

Mã ticket trong MVP:

```text
SUP-101
SUP-102
SUP-103
```

---

## 3.4 Module F4 – Mock Jira / Jira Sync

### 3.4.1 Mock Jira Board

**FR-F4-01:** Trong MVP, hệ thống **PHẢI** có Mock Jira Board để hiển thị các incident/ticket.

Mock Jira Board có thể được xây bằng:

- Bảng trong web demo.
- Google Sheet.
- SQLite.
- Supabase.
- File JSON/CSV.

---

### 3.4.2 Tạo ticket mới

**FR-F4-02:** Khi bug mới được xác nhận, hệ thống **PHẢI** tạo ticket mới trên Mock Jira Board với các trường:

| Trường | Ví dụ |
|---|---|
| `jira_key` | SUP-101 |
| `title` | Lỗi đăng nhập app mobile |
| `summary` | Nhiều user không thể login |
| `module` | Login/Auth |
| `severity` | P1 |
| `status` | Open |
| `owner` | Unassigned |
| `affected_group_count` | 1 |
| `mention_count` | 1 |
| `created_at` | 10:00 |
| `last_seen` | 10:00 |
| `sla_deadline` | 10:30 |

---

### 3.4.3 Cập nhật ticket cũ

**FR-F4-03:** Khi bug trùng được phát hiện, hệ thống **PHẢI** cập nhật ticket cũ:

| Trường cập nhật | Hành động |
|---|---|
| `affected_group_count` | Tăng nếu group mới |
| `mention_count` | Tăng thêm 1 |
| `last_seen` | Cập nhật thời gian mới |
| `comments` | Thêm mô tả mới |
| `severity` | Có thể tăng nếu nhiều group bị ảnh hưởng |

---

### 3.4.4 Tích hợp Jira thật sau MVP

**FR-F4-04:** Sau Hackathon, hệ thống **CÓ THỂ** mở rộng sang Jira thật thông qua Jira REST API.

Các thao tác có thể hỗ trợ:

- Tạo issue mới.
- Comment vào issue cũ.
- Cập nhật priority.
- Cập nhật assignee.
- Đọc status.
- Đọc workload theo assignee.
- Nhận Jira webhook khi issue thay đổi.

---

### 3.4.5 Phản hồi sau khi tạo/cập nhật ticket

**FR-F4-05:** Sau khi tạo hoặc cập nhật ticket, hệ thống **PHẢI** phản hồi cho group/web demo.

Ví dụ bug mới:

```text
[AIA] ✅ Đã ghi nhận sự cố mới

Ticket: SUP-101
Title: Lỗi đăng nhập app mobile
Severity: P1
SLA: 30 phút
Status: Open
```

Ví dụ bug trùng:

```text
[AIA] 🔄 Sự cố này trùng với SUP-101 đang xử lý.
Đã ghi nhận thêm phạm vi ảnh hưởng.
Affected groups: 2
```

---

## 3.5 Module F5 – SLA và Tagged No-response Watch

### 3.5.1 SLA theo severity

**FR-F5-01:** Hệ thống **PHẢI** gán SLA cho mỗi incident dựa trên severity.

| Severity | SLA phản hồi | Hành động nếu quá hạn |
|---|---:|---|
| P1 | 30 phút | Báo lead ngay |
| P2 | 2 giờ | Nhắc owner |
| P3 | 8 giờ | Nhắc trong ngày |

---

### 3.5.2 SLA status

**FR-F5-02:** Mỗi ticket **PHẢI** có trạng thái SLA:

| Trạng thái | Ý nghĩa |
|---|---|
| On Track | Còn nhiều thời gian |
| Warning | Gần đến hạn |
| Overdue | Đã quá hạn |
| Escalated | Đã báo lead |

---

### 3.5.3 Tagged no-response watch

**FR-F5-03:** Nếu khách hàng tag một nhân viên trong tin nhắn bug, hệ thống **PHẢI** tạo watch theo dõi phản hồi.

Ví dụ input:

```text
@Minh check giúp bên em lỗi payment
```

Watch được tạo:

| Trường | Giá trị |
|---|---|
| `incident_id` | INC-002 |
| `jira_key` | SUP-102 |
| `tagged_user` | Minh |
| `watch_start` | 10:00 |
| `expires_at` | 12:00 |
| `status` | Waiting for response |

---

### 3.5.4 Định nghĩa phản hồi hợp lệ

**FR-F5-04:** Một phản hồi được xem là hợp lệ nếu nhân viên hoặc team nội bộ gửi tin nhắn có ý nghĩa xử lý, ví dụ:

- “Mình đã nhận.”
- “Đang kiểm tra.”
- “Đã chuyển team payment xử lý.”
- “Đang check log.”
- “Sẽ cập nhật lại trong 30 phút.”

Không xem là phản hồi hợp lệ nếu chỉ reaction, seen hoặc nhắn không liên quan.

---

### 3.5.5 Escalation khi không phản hồi

**FR-F5-05:** Nếu sau 2 giờ người được tag chưa phản hồi hợp lệ, hệ thống **PHẢI**:

1. Tạo cảnh báo.
2. Nhắc nội bộ người được tag.
3. Nếu vẫn không phản hồi, báo lead.
4. Hiển thị trạng thái trên web demo.

Thông báo mẫu:

```text
[SLA Alert] Khách hàng đã tag Minh trong SUP-102 nhưng chưa có phản hồi hợp lệ sau 2 giờ.
Recommended action: Escalate to Team Lead.
```

---

## 3.6 Module F6 – Dispatch Suggestion: Gợi ý điều phối hỗ trợ

### 3.6.1 Điều kiện kích hoạt

**FR-F6-01:** Module Dispatch Suggestion **PHẢI** được kích hoạt khi xảy ra một trong các điều kiện:

- Incident có severity P1.
- Ticket chưa có owner.
- Team hiện tại không còn người available.
- Lead bấm nút `Suggest Support`.
- Bot phát hiện capacity shortage.
- Nhiều incident nghiêm trọng xuất hiện cùng lúc.

---

### 3.6.2 Dữ liệu đầu vào

**FR-F6-02:** Hệ thống **PHẢI** sử dụng bảng `team_members` để gợi ý người hỗ trợ.

| Trường | Mô tả | Ví dụ |
|---|---|---|
| `user_id` | ID nhân sự | U001 |
| `name` | Tên | Huy |
| `team` | Team | Mobile |
| `skills` | Kỹ năng | Login/Auth |
| `status` | Trạng thái | available |
| `active_issue_count` | Số issue đang mở | 1 |
| `p1_count` | Số P1 đang xử lý | 0 |
| `access_match` | Có quyền truy cập module không | true |

---

### 3.6.3 Tiêu chí đề xuất

**FR-F6-03:** Hệ thống **PHẢI** đề xuất người hỗ trợ dựa trên các tiêu chí:

| Tiêu chí | Ý nghĩa |
|---|---|
| Skill match | Có kỹ năng phù hợp với module lỗi |
| Module match | Có kinh nghiệm với module liên quan |
| Workload thấp | Số issue đang xử lý thấp |
| Availability | Đang available, không nghỉ phép, không locked |
| Access match | Có quyền truy cập hệ thống cần xử lý |

---

### 3.6.4 Kết quả đề xuất

**FR-F6-04:** Hệ thống **PHẢI** hiển thị tối đa 3 người phù hợp nhất.

Ví dụ:

| Rank | Name | Team | Skill | Status | Active Tasks | Match |
|---:|---|---|---|---|---:|---:|
| 1 | Huy | Mobile | Login/Auth | Available | 1 | 92% |
| 2 | Lan | QA Shared | Testing | Available | 2 | 78% |
| 3 | Minh | Backend | Payment | Busy | 6 | 35% |

Kết luận của bot:

```text
Recommended: Huy
Reason: Skill match Login/Auth, available, low workload.
Approval required: Lead.
```

---

### 3.6.5 Giới hạn quyền điều phối

**FR-F6-05:** Hệ thống **KHÔNG ĐƯỢC** tự động điều chuyển nhân sự giữa các team.

**FR-F6-06:** Hệ thống **PHẢI** yêu cầu lead phê duyệt trước khi:

- Add người hỗ trợ vào Jira.
- Đổi owner chính.
- Tạo war room.
- Gửi thông báo vào group điều phối nội bộ.
- Mời thêm người vào bất kỳ group nào.

---

## 3.7 Module F7 – Web Demo Dashboard

### 3.7.1 Màn hình chính

**FR-F7-01:** Web demo **PHẢI** có ít nhất 4 màn hình/tab:

| Màn | Nội dung |
|---|---|
| Chat Intake | Nhập tin nhắn khách hàng |
| AI Triage Result | Hiển thị kết quả AI phân tích |
| Incident Board | Hiển thị ticket/mock Jira |
| SLA & Dispatch | Hiển thị SLA alert và gợi ý người hỗ trợ |

---

### 3.7.2 Chat Intake screen

**FR-F7-02:** Màn hình Chat Intake **PHẢI** có:

- Chọn group.
- Chọn sender.
- Ô nhập tin nhắn.
- Nút `Analyze Incident`.
- Nút chọn demo scenario mẫu.

Ví dụ input:

```text
/bug app mobile không đăng nhập được từ sáng
```

---

### 3.7.3 AI Triage screen

**FR-F7-03:** Màn hình AI Triage **PHẢI** hiển thị:

- Bug detected.
- Title.
- Summary.
- Module.
- Severity.
- Affected scope.
- Suggested reply.
- JSON output.

---

### 3.7.4 Incident Board screen

**FR-F7-04:** Màn hình Incident Board **PHẢI** hiển thị bảng ticket:

| Jira Key | Title | Module | Severity | Status | Owner | Affected Groups |
|---|---|---|---|---|---|---:|
| SUP-101 | Lỗi đăng nhập app mobile | Login/Auth | P1 | Open | Unassigned | 2 |
| SUP-102 | Lỗi thanh toán | Payment | P1 | In Progress | Minh | 1 |

---

### 3.7.5 SLA & Dispatch screen

**FR-F7-05:** Màn hình SLA & Dispatch **PHẢI** có:

- Bảng SLA watch.
- Bảng tagged no-response.
- Bảng team workload.
- Gợi ý người hỗ trợ.
- Trạng thái `Approval required`.

---

### 3.7.6 KPI dashboard

**FR-F7-06:** Web demo **NÊN** có KPI tổng quan:

| KPI | Ví dụ |
|---|---:|
| Open incidents | 4 |
| P1 incidents | 2 |
| Duplicate avoided | 3 |
| SLA alerts | 1 |

---

# 4. Yêu cầu phi chức năng

## 4.1 Hiệu năng (Performance)

| ID | Yêu cầu | Chỉ số đo lường |
|---|---|---|
| NFR-P1 | Thời gian hiển thị xác nhận tiếp nhận | ≤ 3 giây trong demo |
| NFR-P2 | Thời gian AI triage | ≤ 5 giây nếu dùng AI API |
| NFR-P3 | Thời gian mock AI output | Gần như tức thì |
| NFR-P4 | Thời gian tạo/cập nhật mock ticket | ≤ 2 giây |
| NFR-P5 | Thời gian chạy demo 4 luồng | ≤ 3 phút trong video |
| NFR-P6 | Web demo không bị treo khi chạy 4 scenario mẫu | 100% trong điều kiện local |

---

## 4.2 Độ tin cậy (Reliability)

| ID | Yêu cầu | Chi tiết |
|---|---|---|
| NFR-R1 | Có dữ liệu mẫu dự phòng | Nếu AI/API lỗi vẫn chạy demo bằng mock data |
| NFR-R2 | Không phụ thuộc bắt buộc vào Jira thật | Mock Jira phải đủ để demo workflow |
| NFR-R3 | Không phụ thuộc bắt buộc vào Telegram thật | Web input phải thay thế được Telegram |
| NFR-R4 | Có video demo dự phòng | Nếu app lỗi khi chấm, giám khảo vẫn xem được video |
| NFR-R5 | Idempotency cơ bản | Một tin nhắn demo không được tạo nhiều ticket trùng nếu đã xử lý |

---

## 4.3 Bảo mật và an toàn AI (Security & AI Safety)

| ID | Yêu cầu | Chi tiết |
|---|---|---|
| NFR-S1 | Không dùng dữ liệu khách hàng thật | Dataset phải là dữ liệu giả lập |
| NFR-S2 | Không lộ API key | Không đưa token OpenAI, Telegram, Jira vào file nộp |
| NFR-S3 | Không lưu thông tin nhạy cảm | Không lưu số điện thoại, email thật, thông tin doanh nghiệp thật |
| NFR-S4 | AI không tự thực hiện hành động rủi ro | Không rollback, không tắt dịch vụ, không điều người |
| NFR-S5 | Có human approval | Các hành động điều phối cần lead phê duyệt |
| NFR-S6 | Có risk table | Báo cáo phải nêu rủi ro và cách kiểm soát |
| NFR-S7 | Có audit log cơ bản | Ghi nhận hành động tạo ticket, gộp ticket, escalation, dispatch suggestion |

---

## 4.4 Khả năng bảo trì và mở rộng

| ID | Yêu cầu | Chi tiết |
|---|---|---|
| NFR-M1 | Tách module rõ ràng | Intake, AI triage, matching, ticket, SLA, dispatch |
| NFR-M2 | Có thể thay mock Jira bằng Jira thật | Thiết kế có lớp Jira adapter |
| NFR-M3 | Có thể thay web input bằng Telegram bot thật | Thiết kế có lớp chat adapter |
| NFR-M4 | Có thể mở rộng từ rule matching sang semantic matching | MVP dùng rule, bản sau dùng embedding |
| NFR-M5 | Có thể thêm Zalo/Slack sau | Không hard-code quá chặt vào Telegram |
| NFR-M6 | Có README | Hướng dẫn cách chạy/xem demo rõ ràng |

---

## 4.5 Khả năng sử dụng (Usability)

| ID | Yêu cầu | Chi tiết |
|---|---|---|
| NFR-U1 | Giao diện dễ hiểu | Giám khảo nhìn vào hiểu ngay Chat → AI → Ticket → SLA → Dispatch |
| NFR-U2 | Ít chữ, nhiều bảng rõ | Ưu tiên bảng, trạng thái, tag màu |
| NFR-U3 | Severity dễ nhận biết | P1/P2/P3 có màu hoặc nhãn rõ |
| NFR-U4 | Có nút scenario mẫu | Cho phép chạy nhanh Demo 1–4 |
| NFR-U5 | Phản hồi bot ngắn gọn | Không quá dài, có ticket, severity, next step |
| NFR-U6 | Có screenshot | Báo cáo/slide phải chèn ảnh demo |

---

# 5. Ràng buộc thiết kế và kiến trúc

## 5.1 Kiến trúc đề xuất

```text
┌──────────────────────────────┐
│       Group Chat / Web Demo  │
│  - Telegram group             │
│  - Web input                  │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│        Chat Intake Layer      │
│  - nhận message               │
│  - lưu metadata               │
│  - phát hiện mention/tag      │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│        AI Triage Layer        │
│  - detect bug                 │
│  - extract JSON               │
│  - severity P1/P2/P3          │
│  - suggested reply            │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│     Incident Matching Layer   │
│  - new incident?              │
│  - duplicate?                 │
│  - update affected groups     │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│       Mock Jira Board         │
│  - SUP-101                    │
│  - SUP-102                    │
│  - status / owner / SLA       │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│   SLA & Dispatch Layer        │
│  - SLA warning                │
│  - tagged no-response watch   │
│  - suggest support person     │
└──────────────────────────────┘
```

---

## 5.2 Công nghệ gợi ý

| Thành phần | Công nghệ gợi ý | Ghi chú |
|---|---|---|
| Web demo | Streamlit / React / Next.js | Streamlit nhanh nhất cho hackathon |
| Backend | Node.js + Express hoặc Python | Theo năng lực team |
| AI | OpenAI API hoặc mock AI output | Có fallback nếu API lỗi |
| Database | SQLite / Supabase / JSON file | Đủ cho MVP |
| Ticket board | Mock Jira Board | Không cần Jira thật nếu không kịp |
| Jira thật | Jira REST API | Optional |
| Scheduler SLA | node-cron / Python scheduler | Có thể giả lập thời gian trong demo |
| Video demo | OBS / Zoom recording | Dự phòng khi app lỗi |
| Dataset | Excel/CSV | 15–20 tin nhắn mẫu |

---

## 5.3 Ràng buộc MVP Hackathon

- MVP phải demo được trong 2–3 phút.
- MVP chỉ cần 4 luồng chính:
  1. Bug mới.
  2. Bug trùng.
  3. Tagged no-response.
  4. Dispatch suggestion.
- Không thêm tính năng ngoài scope sau mốc giữa Hackathon.
- Nếu code không ổn, dùng prototype + video + screenshot.
- Nếu Jira thật không kịp, dùng Mock Jira.
- Nếu Telegram bot không kịp, dùng web input.
- Nếu AI API lỗi, dùng mock AI output.
- Báo cáo phải ghi rõ phần nào là mock/prototype.

---

# 6. Mô tả Use Case

## 6.1 Danh sách Use Case

| UC ID | Tên Use Case | Tác nhân chính | Module |
|---|---|---|---|
| UC-01 | Báo cáo bug mới từ group chat | Khách hàng | F1, F2, F3, F4 |
| UC-02 | Phát hiện và gộp bug trùng | AIA Bot | F2, F3, F4 |
| UC-03 | Khách tag nhân viên nhưng không phản hồi | Khách hàng, AIA Bot | F1, F5 |
| UC-04 | Team quá tải và cần đề xuất người hỗ trợ | Team Lead, AIA Bot | F6 |
| UC-05 | Xem trạng thái incident | Khách hàng / Support | F4 |
| UC-06 | Xem tóm tắt incident | Team Lead | F5, F6 |

---

## 6.2 UC-01 – Báo cáo bug mới từ group chat

| Trường | Chi tiết |
|---|---|
| Use Case ID | UC-01 |
| Tên | Báo cáo bug mới từ group chat |
| Tác nhân | Khách hàng, AIA Bot, Mock Jira |
| Tiền điều kiện | Web demo hoặc Telegram bot đã sẵn sàng |
| Kích hoạt | Khách gửi tin nhắn `/bug app mobile không đăng nhập được từ sáng` |
| Kết quả mong muốn | Hệ thống tạo ticket SUP-101 |

### Luồng chính

1. Khách hàng gửi tin nhắn bug.
2. Hệ thống ghi nhận message và metadata.
3. Bot phản hồi: “Đã ghi nhận, đang phân tích.”
4. AI xác định đây là bug report.
5. AI trích xuất:
   - Title: Lỗi đăng nhập app mobile.
   - Module: Login/Auth.
   - Severity: P1.
   - Affected scope: Multiple users.
6. Incident Matching kiểm tra chưa có ticket trùng.
7. Hệ thống tạo ticket SUP-101 trên Mock Jira Board.
8. Hệ thống gán SLA 30 phút.
9. Bot phản hồi lại group/web demo.

### Output mẫu

```text
[AIA] ✅ Đã ghi nhận sự cố mới

Ticket: SUP-101
Title: Lỗi đăng nhập app mobile
Severity: P1
SLA: 30 phút
Status: Open
```

### Hậu điều kiện

- Ticket SUP-101 được tạo.
- Incident được lưu.
- SLA bắt đầu đếm.
- Incident xuất hiện trên Incident Board.

---

## 6.3 UC-02 – Phát hiện và gộp bug trùng

| Trường | Chi tiết |
|---|---|
| Use Case ID | UC-02 |
| Tên | Phát hiện và gộp bug trùng |
| Tác nhân | Khách hàng group khác, AIA Bot |
| Tiền điều kiện | SUP-101 đang mở |
| Kích hoạt | Khách gửi `nhiều user bên em không vào app được` |
| Kết quả mong muốn | Gộp vào SUP-101, không tạo ticket mới |

### Luồng chính

1. Group khác gửi mô tả lỗi tương tự.
2. AI xác định đây là bug Login/Auth.
3. Incident Matching so sánh với các incident đang mở.
4. Hệ thống phát hiện trùng SUP-101.
5. Hệ thống không tạo ticket mới.
6. Hệ thống cập nhật:
   - `affected_group_count`: 1 → 2.
   - `mention_count`: +1.
   - `last_seen`: thời điểm hiện tại.
7. Bot phản hồi group rằng incident đã được ghi nhận trước đó.

### Output mẫu

```text
[AIA] 🔄 Sự cố này trùng với SUP-101 đang xử lý.

Đã ghi nhận thêm phạm vi ảnh hưởng.
Affected groups: 2
Status: Open
```

### Hậu điều kiện

- SUP-101 được cập nhật.
- Không có ticket trùng.
- Duplicate avoided tăng thêm 1.

---

## 6.4 UC-03 – Khách tag nhân viên nhưng không phản hồi

| Trường | Chi tiết |
|---|---|
| Use Case ID | UC-03 |
| Tên | Khách tag nhân viên nhưng không phản hồi |
| Tác nhân | Khách hàng, Nhân viên hỗ trợ, AIA Bot, Team Lead |
| Tiền điều kiện | Khách tag nhân viên trong tin nhắn bug |
| Kích hoạt | Khách gửi `@Minh check giúp bên em lỗi payment` |
| Kết quả mong muốn | Bot tạo watch và escalate nếu không phản hồi sau 2 giờ |

### Luồng chính

1. Khách hàng gửi tin nhắn tag Minh.
2. Bot phát hiện `mentioned_user = Minh`.
3. AI xác định đây là bug Payment.
4. Hệ thống tạo ticket SUP-102.
5. Hệ thống tạo `tagged_response_watch`.
6. Sau 2 giờ giả lập, hệ thống kiểm tra chưa có phản hồi hợp lệ.
7. Bot tạo SLA alert.
8. Bot đề xuất escalate cho lead.

### Output mẫu

```text
[SLA Alert] Khách hàng đã tag Minh trong SUP-102 nhưng chưa có phản hồi hợp lệ sau 2 giờ.

Recommended action: Escalate to Team Lead.
```

### Hậu điều kiện

- Watch chuyển sang trạng thái Overdue.
- Escalation level tăng.
- Team Lead nhận cảnh báo trong demo.

---

## 6.5 UC-04 – Team quá tải và cần đề xuất người hỗ trợ

| Trường | Chi tiết |
|---|---|
| Use Case ID | UC-04 |
| Tên | Team quá tải và cần đề xuất người hỗ trợ |
| Tác nhân | Team Lead, AIA Bot |
| Tiền điều kiện | Có incident P1 và team hiện tại quá tải |
| Kích hoạt | Lead bấm `Suggest Support` |
| Kết quả mong muốn | Bot đề xuất tối đa 3 người hỗ trợ |

### Luồng chính

1. Incident P1 mới xuất hiện.
2. Hệ thống kiểm tra owner hiện tại đang busy hoặc chưa có owner.
3. Bot đọc bảng `team_members`.
4. Bot tính mức độ phù hợp dựa trên:
   - Skill match.
   - Module match.
   - Workload.
   - Availability.
   - Access match.
5. Bot hiển thị shortlist.
6. Lead phê duyệt hoặc từ chối.

### Output mẫu

```text
[AIA] 💡 Suggested support for SUP-101

1. Huy – Mobile – Login/Auth – Available – Match 92%
2. Lan – QA Shared – Testing – Available – Match 78%
3. Minh – Backend – Payment – Busy – Match 35%

Recommended: Huy
Reason: Skill match Login/Auth, available, low workload.
Approval required: Lead.
```

### Hậu điều kiện

- Lead có cơ sở ra quyết định.
- Bot không tự điều người.
- Hành động vẫn nằm trong kiểm soát của con người.

---

## 6.6 UC-05 – Xem trạng thái incident

| Trường | Chi tiết |
|---|---|
| Use Case ID | UC-05 |
| Tên | Xem trạng thái incident |
| Tác nhân | Khách hàng / Support |
| Kích hoạt | Người dùng nhập `/status SUP-101` |
| Kết quả mong muốn | Bot hiển thị trạng thái ticket |

### Luồng chính

1. Người dùng nhập `/status SUP-101`.
2. Bot tìm ticket trong Mock Jira Board.
3. Bot trả trạng thái hiện tại.

### Output mẫu

```text
[AIA] Status for SUP-101

Title: Lỗi đăng nhập app mobile
Severity: P1
Status: In Progress
Owner: Huy
Affected groups: 2
Next update: 10:30
```

---

## 6.7 UC-06 – Xem tóm tắt incident

| Trường | Chi tiết |
|---|---|
| Use Case ID | UC-06 |
| Tên | Xem tóm tắt incident |
| Tác nhân | Team Lead |
| Kích hoạt | Lead nhập `/summary` |
| Kết quả mong muốn | Bot hiển thị tóm tắt incident đang mở |

### Output mẫu

```text
[AIA] Summary of Open Incidents

Open incidents: 4
P1 incidents: 2
Duplicate avoided: 3
SLA alerts: 1

Top priority:
SUP-101 – Login/Auth – P1 – 2 groups affected
SUP-102 – Payment – P1 – tagged user no response
```

---

# 7. Ma trận truy xuất yêu cầu

| FR ID | Mô tả tóm tắt | Module | Use Case | Ưu tiên |
|---|---|---|---|---|
| FR-F1-01 | Nhập tin nhắn qua web demo | F1 | UC-01 | Must |
| FR-F1-02 | Nhận tin nhắn Telegram nếu kịp | F1 | UC-01 | Should |
| FR-F1-06 | Nhận diện slash command/mention/tin nhắn tự nhiên | F1 | UC-01, UC-03 | Must |
| FR-F1-07 | Lưu metadata tin nhắn | F1 | UC-01 | Must |
| FR-F1-08 | Phản hồi đã tiếp nhận | F1 | UC-01 | Must |
| FR-F2-01 | Xác định có phải bug không | F2 | UC-01 | Must |
| FR-F2-02 | Trích xuất thông tin có cấu trúc | F2 | UC-01 | Must |
| FR-F2-03 | Hiển thị JSON output | F2 | UC-01 | Must |
| FR-F2-04 | Phân loại severity P1/P2/P3 | F2 | UC-01 | Must |
| FR-F2-05 | Gợi ý phản hồi khách hàng | F2 | UC-01 | Must |
| FR-F3-01 | Kiểm tra incident đang mở | F3 | UC-02 | Must |
| FR-F3-03 | Rule matching bug trùng | F3 | UC-02 | Must |
| FR-F3-04 | Gộp bug trùng | F3 | UC-02 | Must |
| FR-F3-05 | Tạo incident mới nếu không trùng | F3 | UC-01 | Must |
| FR-F4-01 | Có Mock Jira Board | F4 | UC-01, UC-02 | Must |
| FR-F4-02 | Tạo ticket mới | F4 | UC-01 | Must |
| FR-F4-03 | Cập nhật ticket cũ | F4 | UC-02 | Must |
| FR-F4-04 | Có khả năng mở rộng sang Jira thật | F4 | Future | May |
| FR-F5-01 | Theo dõi SLA theo severity | F5 | UC-03 | Must |
| FR-F5-03 | Tạo tagged no-response watch | F5 | UC-03 | Must |
| FR-F5-05 | Escalate khi không phản hồi | F5 | UC-03 | Must |
| FR-F6-01 | Kích hoạt dispatch suggestion | F6 | UC-04 | Should |
| FR-F6-03 | Đề xuất theo skill/workload/status | F6 | UC-04 | Should |
| FR-F6-05 | Không tự động điều phối | F6 | UC-04 | Must |
| FR-F7-01 | Web demo có 4 màn chính | F7 | UC-01–UC-04 | Must |
| FR-F7-06 | Có KPI dashboard | F7 | UC-06 | Should |

---

# 8. Phụ lục

## 8.1 Ví dụ luồng tin nhắn mẫu

### Kịch bản 1 – Bug mới

```text
[10:00] Customer A:
  /bug app mobile không đăng nhập được từ sáng

[10:00] AIA Bot:
  ✅ Đã ghi nhận tin nhắn. Đang phân tích sự cố...

[10:01] AIA Bot:
  ✅ Đã ghi nhận sự cố mới

  Ticket: SUP-101
  Title: Lỗi đăng nhập app mobile
  Module: Login/Auth
  Severity: P1
  SLA: 30 phút
  Status: Open

  Gợi ý phản hồi:
  "Chúng tôi đã ghi nhận sự cố đăng nhập và chuyển đến đội kỹ thuật xử lý. Team sẽ cập nhật trong vòng 30 phút."
```

---

### Kịch bản 2 – Bug trùng

```text
[10:15] Customer B:
  /bug nhiều user bên em không vào app được

[10:15] AIA Bot:
  🔄 Sự cố này trùng với SUP-101 đang xử lý.

  Đã ghi nhận thêm phạm vi ảnh hưởng.
  Affected groups: 2
  Status: Open
  Next update: trước 10:30
```

---

### Kịch bản 3 – Khách tag nhân viên nhưng bị im lặng

```text
[11:00] Customer C:
  @Minh check giúp bên em lỗi payment

[11:00] AIA Bot:
  ✅ Đã ghi nhận lỗi payment.
  Ticket: SUP-102
  Tagged user: Minh
  Watch created: waiting for response

[13:00] AIA Bot:
  ⚠️ SLA Alert:
  Khách hàng đã tag Minh trong SUP-102 nhưng chưa có phản hồi hợp lệ sau 2 giờ.
  Recommended action: Escalate to Team Lead.
```

---

### Kịch bản 4 – Team quá tải

```text
[13:10] AIA Bot:
  Capacity shortage detected for Login/Auth P1 incident.

  Suggested support:
  1. Huy – Mobile – Login/Auth – Available – Match 92%
  2. Lan – QA Shared – Testing – Available – Match 78%
  3. Minh – Backend – Payment – Busy – Match 35%

  Recommended: Huy
  Reason: Skill match Login/Auth, available, low workload.
  Approval required: Lead.
```

---

## 8.2 Schema JSON – AI Triage Output

```json
{
  "message_id": "MSG-001",
  "is_bug_report": true,
  "title": "Lỗi đăng nhập app mobile",
  "summary": "Nhiều người dùng không thể đăng nhập vào ứng dụng mobile từ sáng.",
  "module": "Login/Auth",
  "severity": "P1",
  "affected_scope": "Multiple users",
  "tagged_user": null,
  "suggested_reply": "Hệ thống đã ghi nhận sự cố đăng nhập và chuyển đến đội kỹ thuật xử lý. Team sẽ cập nhật trong vòng 30 phút.",
  "confidence_score": 0.92
}
```

---

## 8.3 Schema dữ liệu tối thiểu

### Bảng `messages`

| Field | Type | Mô tả |
|---|---|---|
| id | string | ID tin nhắn |
| group_id | string | ID group |
| sender_id | string | ID người gửi |
| text | string | Nội dung tin nhắn |
| timestamp | datetime | Thời điểm gửi |
| mentioned_user | string/null | Người được tag |
| incident_id | string/null | Incident liên quan |

---

### Bảng `incidents`

| Field | Type | Mô tả |
|---|---|---|
| id | string | ID incident |
| title | string | Tiêu đề |
| summary | string | Tóm tắt |
| module | string | Module |
| severity | enum | P1/P2/P3 |
| status | enum | Open/In Progress/Resolved |
| jira_key | string | SUP-101 |
| owner | string/null | Người phụ trách |
| mention_count | number | Số lần được báo |
| affected_group_count | number | Số group bị ảnh hưởng |
| first_seen | datetime | Lần đầu xuất hiện |
| last_seen | datetime | Lần gần nhất xuất hiện |
| sla_deadline | datetime | Hạn SLA |

---

### Bảng `team_members`

| Field | Type | Mô tả |
|---|---|---|
| user_id | string | ID nhân sự |
| name | string | Tên |
| team | string | Team |
| skills | array | Kỹ năng |
| status | enum | available/busy/locked/on_leave |
| active_issue_count | number | Số issue đang mở |
| p1_count | number | Số P1 đang xử lý |
| access_match | boolean | Có quyền truy cập module liên quan không |

---

### Bảng `watches`

| Field | Type | Mô tả |
|---|---|---|
| incident_id | string | Incident liên quan |
| jira_key | string | SUP-102 |
| tagged_user_id | string | Người được tag |
| created_at | datetime | Thời điểm bắt đầu watch |
| expires_at | datetime | Thời điểm hết hạn |
| status | enum | waiting/responded/overdue/escalated |
| escalated_level | number | Mức escalation |

---

## 8.4 Danh sách lệnh bot

| Lệnh | Quyền sử dụng | Mô tả | Trạng thái MVP |
|---|---|---|---|
| `/bug [mô tả]` | Tất cả | Báo cáo bug | Must |
| `/status SUP-xxx` | Tất cả | Xem trạng thái ticket | Should |
| `/summary` | Support/Lead | Xem tóm tắt incident đang mở | Should |
| `/suggest SUP-xxx` | Lead | Gợi ý người hỗ trợ | Should |
| `/ack SUP-xxx` | Support/Engineer | Xác nhận đã nhận xử lý | May |
| `/resolve SUP-xxx` | Support/Engineer | Đánh dấu đã xử lý xong | May |
| `/help` | Tất cả | Xem hướng dẫn | May |

---

## 8.5 Luồng hoạt động tổng quát (Flow Diagram)

```text
Khách hàng gửi tin nhắn bug
          │
          ▼
┌────────────────────────┐
│ F1: Chat Intake        │
│ - Nhận message         │
│ - Lưu metadata         │
│ - Phát hiện mention    │
└───────────┬────────────┘
            │
            ▼
┌────────────────────────┐
│ F2: AI Triage          │
│ - Bug or not?          │
│ - Title / Summary      │
│ - Module / Severity    │
│ - Suggested Reply      │
└───────────┬────────────┘
            │
            ▼
┌────────────────────────┐
│ F3: Incident Matching  │
│ - New incident?        │
│ - Duplicate?           │
└───────┬─────────┬──────┘
        │         │
        │         │
        ▼         ▼
┌────────────┐  ┌────────────────┐
│ New Bug    │  │ Duplicate Bug  │
│ Create     │  │ Update Old     │
│ SUP-101    │  │ SUP-101        │
└──────┬─────┘  └───────┬────────┘
       │                │
       └───────┬────────┘
               ▼
┌────────────────────────┐
│ F4: Mock Jira Board    │
│ - Ticket list          │
│ - Status / Owner       │
│ - Affected groups      │
└───────────┬────────────┘
            │
            ▼
┌────────────────────────┐
│ F5: SLA Watch          │
│ - SLA by severity      │
│ - Tagged no-response   │
│ - Escalation           │
└───────────┬────────────┘
            │
            ▼
┌────────────────────────┐
│ F6: Dispatch Suggest   │
│ - Skill match          │
│ - Workload             │
│ - Availability         │
│ - Approval required    │
└────────────────────────┘
```

---

*— Hết tài liệu SRS AI Incident Assistant v1.0 – MVP Hackathon 24h —*

*Tài liệu này được soạn thảo theo cấu trúc IEEE 830-1998 và được điều chỉnh để phù hợp với phạm vi MVP Hackathon 24h. Mọi thay đổi về phạm vi, công nghệ hoặc luồng demo cần được cập nhật vào bảng Lịch sử thay đổi.*
