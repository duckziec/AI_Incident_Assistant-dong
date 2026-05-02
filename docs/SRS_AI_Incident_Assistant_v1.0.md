# SRS – AI Incident Assistant

**Software Requirements Specification**
**Chuẩn IEEE 830-1998 | Phiên bản 1.0 | Tháng 4, 2026**

---

| Trường | Giá trị |
|---|---|
| Phiên bản | 1.0 |
| Ngày soạn thảo | Tháng 4, 2026 |
| Chuẩn áp dụng | IEEE 830-1998 |
| Trạng thái | Bản nháp chính thức |
| Ngôn ngữ hệ thống | Song ngữ Việt – Anh |
| Platform tích hợp | Telegram Bot, Zalo OA / Group Chat |
| Nhóm thực hiện | Phạm Việt Tiến · Bùi Minh Nhật · Trần Quốc Đồng · Hồ Đức Việt |

---

## Lịch sử thay đổi

| Phiên bản | Ngày | Mô tả | Người thực hiện |
|---|---|---|---|
| 1.0 | 04/2026 | Bản SRS khởi tạo dựa trên báo cáo sơ bộ | Nhóm phát triển |

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
   - 3.1 [Module F1 – Tiếp nhận & Nhận diện Bug](#31-module-f1--tiếp-nhận--nhận-diện-bug-intake--detection)
   - 3.2 [Module F2 – AI Triage & Trích xuất thông tin](#32-module-f2--ai-triage--trích-xuất-thông-tin)
   - 3.3 [Module F3 – Incident Matching](#33-module-f3--incident-matching-phát-hiện-trùng-lặp)
   - 3.4 [Module F4 – Đồng bộ với Jira](#34-module-f4--đồng-bộ-với-jira)
   - 3.5 [Module F5 – Theo dõi SLA & Escalation](#35-module-f5--theo-dõi-sla--escalation)
   - 3.6 [Module F6 – Gợi ý điều phối nhân sự](#36-module-f6--gợi-ý-điều-phối-nhân-sự)
4. [Yêu cầu phi chức năng](#4-yêu-cầu-phi-chức-năng)
   - 4.1 [Hiệu năng](#41-hiệu-năng-performance)
   - 4.2 [Độ tin cậy](#42-độ-tin-cậy-reliability)
   - 4.3 [Bảo mật](#43-bảo-mật-security)
   - 4.4 [Khả năng bảo trì & Mở rộng](#44-khả-năng-bảo-trì--mở-rộng-maintainability--scalability)
   - 4.5 [Khả năng sử dụng](#45-khả-năng-sử-dụng-usability)
5. [Ràng buộc thiết kế và kiến trúc](#5-ràng-buộc-thiết-kế-và-kiến-trúc)
   - 5.1 [Kiến trúc đề xuất](#51-kiến-trúc-đề-xuất)
   - 5.2 [Công nghệ gợi ý](#52-công-nghệ-gợi-ý)
   - 5.3 [Ràng buộc tích hợp nền tảng](#53-ràng-buộc-tích-hợp-nền-tảng)
6. [Mô tả Use Case](#6-mô-tả-use-case)
   - 6.1 [Danh sách Use Case](#61-danh-sách-use-case)
   - 6.2 [UC-01 – Báo cáo lỗi qua Telegram](#62-uc-01--báo-cáo-lỗi-qua-telegram)
   - 6.3 [UC-02 – Báo cáo lỗi qua Zalo](#63-uc-02--báo-cáo-lỗi-qua-zalo)
   - 6.4 [UC-03 – Phát hiện và gộp incident trùng lặp](#64-uc-03--phát-hiện-và-gộp-incident-trùng-lặp)
   - 6.5 [UC-04 – SLA vi phạm và leo thang](#65-uc-04--sla-vi-phạm-và-leo-thang)
   - 6.6 [UC-05 – Gợi ý điều phối nhân sự](#66-uc-05--gợi-ý-điều-phối-nhân-sự)
   - 6.7 [UC-06 – Xem báo cáo SLA](#67-uc-06--xem-báo-cáo-sla)
7. [Ma trận truy xuất yêu cầu](#7-ma-trận-truy-xuất-yêu-cầu)
8. [Phụ lục](#8-phụ-lục)
   - 8.1 [Ví dụ luồng tin nhắn mẫu](#81-ví-dụ-luồng-tin-nhắn-mẫu)
   - 8.2 [Schema JSON – Incident Object](#82-schema-json--incident-object)
   - 8.3 [Danh sách lệnh Bot](#83-danh-sách-lệnh-bot)
   - 8.4 [Luồng hoạt động tổng quát (Flow Diagram)](#84-luồng-hoạt-động-tổng-quát-flow-diagram)

---

## 1. Giới thiệu

### 1.1 Mục đích (Purpose)

Tài liệu này là **Đặc tả Yêu cầu Phần mềm (SRS)** cho hệ thống **AI Incident Assistant (AIA)**, xây dựng theo chuẩn IEEE 830-1998. Tài liệu mô tả đầy đủ các yêu cầu chức năng, phi chức năng, ràng buộc hệ thống và hành vi mong đợi của phần mềm nhằm:

- Cung cấp cơ sở tham chiếu cho nhóm phát triển khi thiết kế, lập trình và kiểm thử hệ thống.
- Làm tài liệu hợp đồng / kiểm chứng giữa nhóm phát triển và các bên liên quan.
- Phục vụ cuộc thi *"Trí tuệ Nhân tạo trong Kinh doanh Mùa 3"* với chủ đề ứng dụng AI liên ngành.

**Đối tượng đọc:** Nhóm phát triển, giám khảo cuộc thi, bên liên quan doanh nghiệp (SME).

---

### 1.2 Phạm vi hệ thống (Scope)

**AI Incident Assistant (AIA)** là một chatbot AI hoạt động như **lớp trung gian thông minh** (AI middleware layer) giữa kênh group chat hỗ trợ khách hàng và hệ thống quản lý issue **Jira**. Hệ thống phục vụ các doanh nghiệp nhỏ và vừa (SME) hoạt động trong lĩnh vực phần mềm và dịch vụ số.

**Phạm vi bao gồm:**

- Tích hợp với hai nền tảng: **Telegram Bot API** và **Zalo Official Account (OA) / Group Chat API**.
- Xử lý ngôn ngữ tự nhiên **song ngữ Việt – Anh** để nhận diện và phân tích báo cáo lỗi.
- Tích hợp hai chiều với **Jira Software Cloud/Server** qua REST API.
- Theo dõi **SLA phản hồi** và cơ chế **escalation** tự động.
- Module **gợi ý điều phối nhân sự** dựa trên workload và skill.

**Ngoài phạm vi (Out of Scope):**

- Không thay thế Jira hay bất kỳ hệ thống ticket nào hiện có.
- Không hỗ trợ các nền tảng chat khác (Slack, Microsoft Teams, v.v.) trong phiên bản 1.0.
- Không tự động phân công hoặc di chuyển nhân sự — chỉ gợi ý cho quản lý.
- Không xử lý các loại phản ánh ngoài phạm vi bug / incident phần mềm.

---

### 1.3 Định nghĩa, từ viết tắt và ký hiệu (Definitions)

| Thuật ngữ / Từ viết tắt | Định nghĩa |
|---|---|
| **AIA** | AI Incident Assistant – tên hệ thống được xây dựng trong tài liệu này. |
| **SME** | Small and Medium-sized Enterprise – Doanh nghiệp nhỏ và vừa. |
| **Bug / Incident** | Lỗi phần mềm hoặc sự cố dịch vụ do khách hàng báo cáo. |
| **Triage** | Quá trình phân loại và đánh giá mức độ nghiêm trọng của incident. |
| **SLA** | Service Level Agreement – Thỏa thuận mức độ dịch vụ về thời gian phản hồi. |
| **Jira** | Phần mềm quản lý dự án và theo dõi issue của Atlassian. |
| **NLP** | Natural Language Processing – Xử lý ngôn ngữ tự nhiên. |
| **LLM** | Large Language Model – Mô hình ngôn ngữ lớn (ví dụ: GPT-4o, Claude 3.5). |
| **Semantic Matching** | Kỹ thuật so khớp ngữ nghĩa để phát hiện hai mô tả khác nhau nhưng cùng phản ánh một incident. |
| **Escalation** | Quá trình leo thang, chuyển vấn đề lên cấp cao hơn khi không được xử lý trong thời gian quy định. |
| **Workload** | Khối lượng công việc hiện tại của một nhân sự kỹ thuật (số incident đang xử lý). |
| **Webhook** | Cơ chế nhận sự kiện HTTP từ nền tảng chat (Telegram/Zalo) khi có tin nhắn mới. |
| **Severity** | Mức độ nghiêm trọng của incident: Critical, High, Medium, Low. |
| **Group Chat** | Nhóm chat hỗ trợ khách hàng trên Telegram hoặc Zalo. |
| **Embedding** | Biểu diễn văn bản dưới dạng vector số để thực hiện so khớp ngữ nghĩa. |
| **Cosine Similarity** | Độ đo tương đồng giữa hai vector embedding (0 = khác hoàn toàn, 1 = giống hoàn toàn). |
| **Idempotency** | Tính chất đảm bảo cùng một thao tác thực hiện nhiều lần cho ra kết quả như nhau. |

---

### 1.4 Tài liệu tham khảo (References)

- IEEE Std 830-1998 – *IEEE Recommended Practice for Software Requirements Specifications.*
- Báo cáo sơ bộ: *"AI Incident Assistant – Ứng dụng AI trong Kinh doanh và Quản lý"* (2026) – Nhóm tác giả.
- Atlassian Jira REST API v3 Documentation – https://developer.atlassian.com/cloud/jira/
- Telegram Bot API Documentation – https://core.telegram.org/bots/api
- Zalo Official Account API Documentation – https://developers.zalo.me/
- OpenAI API Documentation – https://platform.openai.com/docs/

---

### 1.5 Tổng quan tài liệu (Overview)

Tài liệu được tổ chức theo cấu trúc chuẩn IEEE 830:

| Phần | Nội dung |
|---|---|
| Phần 2 | Mô tả tổng quan hệ thống: bối cảnh, tác nhân, chức năng tổng quát. |
| Phần 3 | Yêu cầu chức năng chi tiết theo 6 module (F1–F6). |
| Phần 4 | Yêu cầu phi chức năng: hiệu năng, tin cậy, bảo mật, khả năng mở rộng. |
| Phần 5 | Ràng buộc thiết kế và kiến trúc kỹ thuật đề xuất. |
| Phần 6 | Mô tả Use Case với luồng chính và luồng thay thế. |
| Phần 7 | Ma trận truy xuất yêu cầu (FR → Module → Use Case). |
| Phần 8 | Phụ lục: ví dụ hội thoại, schema JSON, danh sách lệnh bot, flow diagram. |

---

## 2. Mô tả tổng quan hệ thống

### 2.1 Bối cảnh hệ thống (System Context)

AIA hoạt động trong môi trường doanh nghiệp SME cung cấp phần mềm/dịch vụ số. Hệ thống đóng vai trò **lớp trung gian AI** kết nối ba thành phần chính:

```
┌─────────────────────┐       ┌──────────────────────┐       ┌────────────────┐
│   Kênh đầu vào      │       │   Lõi xử lý AI (AIA) │       │  Hệ thống đích │
│                     │       │                      │       │                │
│  • Telegram Bot     │──────▶│  • NLP / LLM Triage  │──────▶│  • Jira Cloud  │
│  • Zalo OA / Group  │       │  • Semantic Matching  │       │  • Jira Server │
│                     │◀──────│  • SLA Engine         │◀──────│                │
└─────────────────────┘       │  • Resource Advisor   │       └────────────────┘
                              └──────────────────────┘
```

**Vấn đề AIA giải quyết:** Khoảng trống giữa *"bug xuất hiện trong chat"* và *"bug được ghi nhận chính thức vào Jira"* — khoảng trống hiện tại đòi hỏi thao tác thủ công của nhân sự hỗ trợ và dễ dẫn đến bỏ sót hoặc phản hồi chậm.

---

### 2.2 Các tác nhân (Actors / Stakeholders)

| Tác nhân | Vai trò | Tương tác chính với AIA |
|---|---|---|
| **Khách hàng** (Customer) | Người sử dụng sản phẩm/dịch vụ, báo cáo lỗi trong group chat. | Gửi tin nhắn mô tả lỗi; nhận phản hồi xác nhận từ bot. |
| **Nhân viên hỗ trợ** (Support Staff) | Người trực tiếp trả lời khách hàng và xử lý ticket ban đầu. | Nhận nhắc nhở SLA; xác nhận hoặc bác bỏ đề xuất của bot. |
| **Kỹ sư kỹ thuật** (Engineer) | Người phân tích và sửa lỗi trên hệ thống. | Nhận gợi ý phân công; cập nhật trạng thái xử lý. |
| **Team Lead / Manager** | Người quản lý đội ngũ và giám sát quy trình vận hành. | Nhận báo cáo tổng hợp incident; phê duyệt điều phối nhân sự. |
| **Hệ thống Jira** | Hệ thống quản lý issue đích (bên ngoài). | Nhận issue mới; cập nhật comment; cung cấp trạng thái hiện tại. |
| **AIA Bot** | Tác nhân chính của hệ thống – chatbot AI. | Lắng nghe tin nhắn, xử lý AI, phản hồi, đồng bộ Jira. |

---

### 2.3 Chức năng tổng quát (General Functions)

AIA thực hiện sáu nhóm chức năng cốt lõi:

| Module | Tên | Mô tả ngắn |
|---|---|---|
| **F1** | Intake & Detection | Tiếp nhận tin nhắn từ group chat và nhận diện bug report. |
| **F2** | AI Triage & Extraction | Trích xuất thông tin có cấu trúc từ mô tả ngôn ngữ tự nhiên. |
| **F3** | Incident Matching | Phát hiện trùng lặp với incident đang mở bằng semantic matching. |
| **F4** | Jira Sync | Đồng bộ dữ liệu hai chiều với Jira (tạo mới / cập nhật issue). |
| **F5** | SLA Monitoring & Escalation | Theo dõi thời hạn phản hồi và leo thang khi cần thiết. |
| **F6** | Resource Coordination | Gợi ý điều phối nhân sự kỹ thuật khi quá tải. |

---

### 2.4 Đặc điểm người dùng (User Characteristics)

- **Khách hàng:** Không có kiến thức kỹ thuật chuyên sâu; giao tiếp bằng tiếng Việt hoặc tiếng Anh; quen dùng Telegram/Zalo; có xu hướng dùng ngôn ngữ không chính thức, viết tắt.
- **Nhân viên hỗ trợ:** Có kiến thức cơ bản về quy trình hỗ trợ; sử dụng Jira hàng ngày; cần phản hồi nhanh trong giờ làm việc.
- **Kỹ sư:** Hiểu biết kỹ thuật sâu; quan tâm đến chi tiết lỗi, module bị ảnh hưởng và mức ưu tiên.
- **Team Lead / Manager:** Cần cái nhìn tổng quan về tình trạng incident và năng lực đội ngũ; không muốn bị làm phiền bởi chi tiết kỹ thuật.

---

### 2.5 Ràng buộc tổng quát (General Constraints)

- Hệ thống phải tuân thủ **điều khoản sử dụng API** của Telegram và Zalo.
- Dữ liệu khách hàng phải được xử lý theo nguyên tắc **bảo mật tối thiểu** (minimal data retention).
- LLM được sử dụng phải **hỗ trợ song ngữ Việt – Anh** với độ chính xác chấp nhận được trên văn phong không chính thức.
- Hệ thống phải hoạt động ổn định **24/7** với downtime không quá **0.1% mỗi tháng** (≈ 43.8 phút/tháng).
- Chi phí vận hành LLM API phải nằm trong ngân sách cho phép của SME (ưu tiên giải pháp cost-effective).

---

### 2.6 Giả định và phụ thuộc (Assumptions and Dependencies)

**Giả định:**

- Doanh nghiệp đã có tài khoản Jira và ít nhất một project được cấu hình với các trạng thái Open/In Progress/Done.
- Doanh nghiệp đã có **Telegram Bot Token** hoặc **Zalo OA được phê duyệt** bởi Zalo.
- Nhân viên hỗ trợ được thêm vào các group chat cùng với khách hàng.
- Dữ liệu kỹ năng (skill) và lịch làm việc của nhân sự được duy trì trong hệ thống AIA.

**Phụ thuộc:**

- Khả dụng của Jira REST API, Telegram Bot API, Zalo OA API.
- LLM provider cung cấp API với độ trễ phù hợp (< 5 giây cho 95% request).
- Hạ tầng server có khả năng nhận HTTPS webhook công khai (hoặc sử dụng ngrok/reverse proxy cho môi trường dev).

---

## 3. Yêu cầu chức năng

> **Quy ước mức độ bắt buộc:**
> - **PHẢI (MUST):** Bắt buộc, hệ thống không hoạt động được nếu thiếu.
> - **NÊN (SHOULD):** Khuyến nghị mạnh, cần có trong phiên bản 1.0 nếu có thể.
> - **CÓ THỂ (MAY):** Tùy chọn, có thể triển khai sau.

---

### 3.1 Module F1 – Tiếp nhận & Nhận diện Bug (Intake & Detection)

#### 3.1.1 Kết nối đa nền tảng

**FR-F1-01:** Hệ thống **PHẢI** kết nối với Telegram thông qua **Telegram Bot API** sử dụng cơ chế **Webhook** (không dùng Long Polling trong môi trường production).

**FR-F1-02:** Hệ thống **PHẢI** kết nối với Zalo thông qua **Zalo Official Account API**, hỗ trợ cả Zalo OA message và Zalo Group Chat.

**FR-F1-03:** Hệ thống **PHẢI** nhận và xử lý tin nhắn văn bản. Hệ thống **NÊN** hỗ trợ nhận ảnh đính kèm (screenshot lỗi) trong phiên bản tương lai (v1.1+).

**FR-F1-04 (Đặc thù Telegram):** Hệ thống **PHẢI** xác thực tính xác thực của mỗi webhook request từ Telegram bằng chữ ký HMAC-SHA256 với Bot Secret Token.

**FR-F1-05 (Đặc thù Zalo):** Hệ thống **PHẢI** xác thực webhook từ Zalo theo chuẩn xác thực OA của Zalo (appId + secret-based verification).

#### 3.1.2 Kích hoạt bot

**FR-F1-06:** Hệ thống **PHẢI** nhận diện bug report khi người dùng sử dụng một trong các phương thức sau:

| Phương thức | Ví dụ | Platform hỗ trợ |
|---|---|---|
| Slash command | `/bug`, `/incident`, `/report` | Telegram |
| Mention bot | `@TenBot lỗi login không vào được` | Telegram, Zalo |
| Ngôn ngữ tự nhiên | `"app bên em bị lỗi từ sáng đến giờ"` | Telegram, Zalo (qua AI triage) |
| Tag người phụ trách kèm mô tả lỗi | `@support_nguyen check lỗi thanh toán` | Telegram, Zalo |

**FR-F1-07:** Hệ thống **PHẢI** ghi nhận metadata của mỗi tin nhắn đến:
- ID nhóm chat (group_id)
- ID người gửi (sender_id)
- Tên người gửi (sender_name)
- Nội dung tin nhắn (message_text)
- Timestamp UTC+7 (received_at)
- ID người được tag trong tin nhắn (mentioned_user_ids, nếu có)
- Platform nguồn (telegram / zalo)

**FR-F1-08:** Hệ thống **PHẢI** phản hồi xác nhận tiếp nhận trong vòng **5 giây** kể từ khi nhận được tin nhắn, ngay cả khi quá trình AI triage chưa hoàn tất.

#### 3.1.3 Bộ lọc và ghi nhận

**FR-F1-09:** Hệ thống **PHẢI** lọc và bỏ qua các tin nhắn không phải bug report (chào hỏi, thảo luận nội bộ, câu hỏi thông thường) sau khi AI triage xác nhận đây không phải incident.

**FR-F1-10:** Hệ thống **PHẢI** ghi log tất cả tin nhắn được nhận và quyết định phân loại (bug / không phải bug / không chắc chắn) kèm confidence score để phục vụ audit và cải thiện mô hình.

**FR-F1-11:** Hệ thống **CÓ THỂ** hỗ trợ chế độ "chỉ xử lý khi được mention" (mention-only mode) để giảm nhiễu trong các group có nhiều hội thoại không liên quan.

---

### 3.2 Module F2 – AI Triage & Trích xuất thông tin

#### 3.2.1 Phân loại bug

**FR-F2-01:** Hệ thống **PHẢI** sử dụng LLM để phân tích nội dung tin nhắn và xác định xác suất đây là một bug report. Ngưỡng phân loại (confidence threshold) **PHẢI** được cấu hình được (mặc định: **0.70**).

**FR-F2-02:** LLM **PHẢI** xử lý cả tiếng Việt và tiếng Anh, bao gồm:
- Văn phong không chính thức, khẩu ngữ.
- Viết tắt phổ biến (k = không, bth = bình thường, v = vậy).
- Code-switching (lẫn lộn Việt – Anh trong cùng một câu).
- Emoji và ký tự đặc biệt.

**FR-F2-03:** Trong trường hợp confidence score nằm trong khoảng [0.40, 0.70), hệ thống **NÊN** hỏi lại người dùng để xác nhận thay vì tự động quyết định:

> *"[AIA] Bot nhận thấy đây có thể là lỗi phần mềm. Bạn có muốn tạo ticket hỗ trợ không? (Trả lời 'có' / 'yes' để xác nhận)"*

#### 3.2.2 Trích xuất thông tin có cấu trúc

**FR-F2-04:** Khi xác nhận là bug report, hệ thống **PHẢI** trích xuất các trường thông tin sau:

| Trường | Tên tiếng Anh | Bắt buộc | Kiểu dữ liệu | Mô tả |
|---|---|---|---|---|
| Tiêu đề lỗi | `title` | ✅ Có | string (≤100 ký tự) | Tóm tắt ngắn gọn, rõ nghĩa. |
| Mô tả chi tiết | `description` | ✅ Có | string | Mô tả đầy đủ, giữ nguyên ngôn ngữ gốc. |
| Module liên quan | `component` | ❌ Không | string | Module/tính năng bị ảnh hưởng (Login, Payment, v.v.). |
| Mức độ nghiêm trọng | `severity` | ✅ Có | enum | Critical / High / Medium / Low. |
| Phạm vi ảnh hưởng | `impact_scope` | ✅ Có | object | Ước tính số người dùng bị ảnh hưởng. |
| Môi trường | `environment` | ❌ Không | string | Production / Staging / Dev (nếu đề cập). |
| Bước tái hiện | `steps_to_reproduce` | ❌ Không | string | Các bước để tái hiện lỗi. |
| Gợi ý phản hồi | `suggested_response` | ✅ Có | string | Câu trả lời gợi ý cho khách hàng do LLM tạo ra. |
| Ngôn ngữ nguồn | `source_language` | ✅ Có | enum | vi / en |

**FR-F2-05:** LLM **PHẢI** sử dụng cơ chế **function calling / structured output** (JSON mode) để đảm bảo đầu ra luôn theo schema định sẵn, tránh lỗi parsing.

#### 3.2.3 Phân loại mức độ nghiêm trọng

**FR-F2-06:** Hệ thống **PHẢI** phân loại severity theo ma trận sau:

| Mức độ | Màu | Tiêu chí nhận diện | SLA phản hồi ban đầu |
|---|---|---|---|
| 🔴 **Critical** | Đỏ | Hệ thống ngừng hoạt động hoàn toàn; ảnh hưởng toàn bộ người dùng; lỗi thanh toán; mất dữ liệu. | **15 phút** |
| 🟠 **High** | Cam | Chức năng cốt lõi bị lỗi; ảnh hưởng nhiều người dùng; không có workaround. | **1 giờ** |
| 🟡 **Medium** | Vàng | Chức năng phụ bị ảnh hưởng; ảnh hưởng một số người dùng; có workaround. | **4 giờ** |
| 🟢 **Low** | Xanh | Vấn đề nhỏ; ảnh hưởng hạn chế; không ảnh hưởng chức năng chính. | **24 giờ** (giờ làm việc) |

**FR-F2-07:** Hệ thống **PHẢI** tự động **nâng severity lên một cấp** nếu cùng một lỗi được báo cáo bởi từ **3 group chat khác nhau** trong vòng **1 giờ** (xem FR-F3-04 về cross-group aggregation).

**FR-F2-08:** Hệ thống **PHẢI** cho phép nhân viên hỗ trợ và team lead **ghi đè severity** thủ công thông qua lệnh `/severity PROJ-xxx High`.

---

### 3.3 Module F3 – Incident Matching (Phát hiện trùng lặp)

#### 3.3.1 Kiểm tra incident đang mở

**FR-F3-01:** Hệ thống **PHẢI** truy vấn danh sách incident đang mở trên Jira (trạng thái: Open, In Progress, Reopened) trước khi tạo issue mới. Kết quả truy vấn **NÊN** được cache trong tối đa **60 giây** để giảm tải API.

**FR-F3-02:** Hệ thống **PHẢI** chuyển đổi title và description của mỗi incident thành **embedding vector** và lưu vào vector store (FAISS hoặc tương đương) để tra cứu nhanh.

**FR-F3-03:** Hệ thống **PHẢI** sử dụng **cosine similarity** để tính điểm tương đồng giữa bug mới (sau khi extract) và các incident đang mở.

**FR-F3-04:** Ngưỡng trùng lặp (similarity threshold) **PHẢI** được cấu hình được (mặc định: **0.80**):
- Điểm tương đồng ≥ 0.80 → Xác định là **trùng lặp**.
- Điểm tương đồng ∈ [0.60, 0.80) → Hiển thị **gợi ý có thể trùng** để nhân sự xác nhận.
- Điểm tương đồng < 0.60 → Xử lý là **incident mới**.

#### 3.3.2 Xử lý trùng lặp

**FR-F3-05:** Nếu phát hiện trùng lặp, hệ thống **PHẢI**:
1. Gộp dữ liệu từ báo cáo mới vào incident hiện tại (thêm comment trên Jira).
2. Cập nhật `impact_scope` (phạm vi ảnh hưởng) của incident hiện tại.
3. Kiểm tra và áp dụng FR-F2-07 nếu số lượng group báo cáo vượt ngưỡng.
4. Thông báo cho nhóm chat kèm mã Jira issue của incident gốc và trạng thái hiện tại.

**FR-F3-06:** Nếu không tìm thấy incident trùng, hệ thống **PHẢI** tạo incident mới (xem Module F4).

**FR-F3-07:** Hệ thống **PHẢI** lưu bảng mapping `{message_id, chat_id, platform} → {incident_id, jira_issue_key}` để:
- Tránh xử lý trùng cùng một tin nhắn (idempotency).
- Truy xuất lịch sử của một incident từ nhiều nguồn.

**FR-F3-08:** Hệ thống **PHẢI** cập nhật embedding index khi có incident mới được tạo hoặc đóng, đảm bảo tính chính xác của semantic matching theo thời gian.

---

### 3.4 Module F4 – Đồng bộ với Jira

#### 3.4.1 Tạo Jira issue mới

**FR-F4-01:** Khi phát hiện incident mới, hệ thống **PHẢI** tự động tạo Jira issue với các trường sau:

| Trường Jira | Giá trị ánh xạ từ AIA |
|---|---|
| `summary` | `title` từ AI extraction |
| `description` | `description` + nguồn gốc (platform, group_id, sender) + timestamp |
| `issuetype` | Bug |
| `priority` | Ánh xạ từ `severity` (Critical→Highest, High→High, Medium→Medium, Low→Low) |
| `components` | `component` từ AI extraction (nếu có) |
| `labels` | `["aia-auto", "telegram"]` hoặc `["aia-auto", "zalo"]` |
| `customfield_*` | Trường tùy chỉnh theo cấu hình doanh nghiệp |

**FR-F4-02:** Hệ thống **PHẢI** lưu `jira_issue_key` (ví dụ: `PROJ-456`) ngay sau khi tạo thành công và liên kết với `incident_id` trong database nội bộ.

**FR-F4-03:** Hệ thống **PHẢI** phản hồi lại group chat với thông tin đầy đủ sau khi tạo Jira issue:

```
[AIA] ✅ Đã ghi nhận sự cố

📋 PROJ-456: Lỗi đăng nhập không vào được
🔴 Mức độ: High  
⏰ Phản hồi trong: 1 giờ (trước 10:35)
👤 Phụ trách: @nguyen_van_a
🔗 https://jira.company.com/browse/PROJ-456

💬 Phản hồi gợi ý: "Xin chào! Chúng tôi đã nhận được báo cáo và đang khẩn trương kiểm tra. Vui lòng chờ phản hồi trong 1 giờ."
```

**FR-F4-04:** Nếu Jira API không khả dụng, hệ thống **PHẢI**:
1. Lưu incident vào hàng đợi chờ (pending queue) trong database nội bộ.
2. Phản hồi nhóm chat thông báo đã ghi nhận nhưng đang chờ đồng bộ.
3. Retry tự động sau 30 giây, tối đa 3 lần trước khi gửi cảnh báo admin.

#### 3.4.2 Cập nhật Jira issue hiện có

**FR-F4-05:** Khi phát hiện incident trùng lặp, hệ thống **PHẢI** thêm comment vào Jira issue tương ứng với nội dung:
- Nguồn báo cáo mới (platform, tên nhóm chat, người gửi, timestamp).
- Mô tả bổ sung từ báo cáo mới.
- Cập nhật số lượng nhóm và người dùng bị ảnh hưởng.

**FR-F4-06:** Hệ thống **NÊN** nhận **Jira webhook** khi status của issue thay đổi và tự động thông báo cập nhật về group chat nguồn:

> *"[AIA] 🔄 Cập nhật PROJ-456: Trạng thái chuyển sang 'In Progress'. Kỹ sư @tran_quoc_dong đang xử lý."*

#### 3.4.3 Cấu hình kết nối Jira

**FR-F4-07:** Hệ thống **PHẢI** cho phép cấu hình các thông số Jira qua file cấu hình (không hard-code):
- `JIRA_BASE_URL`: URL của Jira instance.
- `JIRA_PROJECT_KEY`: Key của project (ví dụ: PROJ).
- `JIRA_AUTH_METHOD`: API Token hoặc OAuth 2.0.
- `JIRA_API_VERSION`: v2 (Server/DC) hoặc v3 (Cloud).
- `JIRA_PRIORITY_MAPPING`: JSON object ánh xạ severity → Jira priority.

**FR-F4-08:** Hệ thống **PHẢI** kiểm tra kết nối Jira khi khởi động (health check) và ghi cảnh báo log nếu không thể kết nối.

---

### 3.5 Module F5 – Theo dõi SLA & Escalation

#### 3.5.1 Theo dõi SLA

**FR-F5-01:** Hệ thống **PHẢI** bắt đầu đếm thời gian SLA ngay khi incident được tạo, sử dụng **timestamp của tin nhắn gốc** từ khách hàng (không phải thời điểm AIA xử lý xong hay tạo Jira issue).

**FR-F5-02:** Hệ thống **PHẢI** gửi cảnh báo nội bộ vào group chat hỗ trợ khi còn **20% thời hạn SLA**:

| Severity | SLA | Cảnh báo tại | Nội dung cảnh báo |
|---|---|---|---|
| Critical | 15 phút | 12 phút | `[SLA ⚠️] PROJ-456 (Critical) còn 3 phút. @support_nguyen phản hồi NGAY!` |
| High | 1 giờ | 48 phút | `[SLA ⚠️] PROJ-456 (High) còn 12 phút. @support_nguyen cần phản hồi.` |
| Medium | 4 giờ | 3h 12ph | `[SLA ⚠️] PROJ-456 (Medium) còn 48 phút.` |
| Low | 24 giờ | 19h 12ph | `[SLA ℹ️] PROJ-456 (Low) còn 4h 48ph.` |

**FR-F5-03:** Hệ thống **PHẢI** theo dõi trường hợp khách hàng đã **tag người phụ trách** nhưng chưa có phản hồi.

> **Định nghĩa "có phản hồi":** Nhân viên hỗ trợ (hoặc bất kỳ thành viên team nội bộ nào) gửi ít nhất một tin nhắn vào group chat sau khi khách hàng gửi báo cáo.

**FR-F5-04:** Hệ thống **PHẢI** tính SLA theo giờ thực (24/7) cho Critical và High, và theo **giờ làm việc** (cấu hình được) cho Medium và Low.

#### 3.5.2 Cơ chế Escalation

**FR-F5-05:** Hệ thống **PHẢI** thực hiện escalation theo trình tự sau khi vi phạm SLA:

```
Hết 100% SLA
    ↓
[Bước 1] Nhắc nhở người phụ trách qua tin nhắn direct (nếu kết nối được)
    ↓ (sau 10 phút không có phản hồi)
[Bước 2] Thông báo công khai vào group chat hỗ trợ
    ↓ (sau khi vượt 150% SLA)
[Bước 3] Gửi cảnh báo đến Team Lead (qua direct message)
```

**FR-F5-06:** Hệ thống **PHẢI** tạo **SLA breach log** cho mỗi lần vi phạm với các trường:
- `incident_id`, `jira_issue_key`
- `severity`, `sla_duration_minutes`
- `breach_at` (thời điểm vi phạm)
- `first_response_at` (thời điểm phản hồi đầu tiên, nếu có)
- `delay_minutes` (số phút trễ)
- `escalation_level` (1/2/3)

**FR-F5-07:** Hệ thống **PHẢI** cung cấp báo cáo SLA qua lệnh chat `/report sla [week|month]` với nội dung:
- Tổng số incident theo severity.
- Tỷ lệ tuân thủ SLA (%).
- Danh sách các vi phạm SLA.
- Trung bình thời gian phản hồi theo severity.

---

### 3.6 Module F6 – Gợi ý điều phối Nhân sự

#### 3.6.1 Điều kiện kích hoạt

**FR-F6-01:** Module điều phối nhân sự được kích hoạt khi một trong các điều kiện sau xảy ra:

- Tất cả kỹ sư được phân công cho incident đang bận với incident khác có severity ≥ High.
- Team Lead yêu cầu gợi ý bằng lệnh `/suggest PROJ-xxx` hoặc `/reassign PROJ-xxx`.
- Incident đạt mức **Critical** và chưa được phân công trong vòng **5 phút**.

#### 3.6.2 Thuật toán gợi ý

**FR-F6-02:** Hệ thống **PHẢI** xây dựng danh sách gợi ý nhân sự dựa trên các tiêu chí sau (thứ tự ưu tiên giảm dần):

| Thứ tự | Tiêu chí | Mô tả |
|---|---|---|
| 1 | Kỹ năng phù hợp | Có skill khớp với `component` của incident. |
| 2 | Workload thấp nhất | Số incident đang xử lý (trạng thái Open/In Progress) ít nhất. |
| 3 | Trạng thái sẵn sàng | Đang online / không trong giờ nghỉ theo lịch đã cấu hình. |
| 4 | Quyền truy cập | Có quyền truy cập vào hệ thống liên quan đến component bị lỗi. |

**FR-F6-03:** Hệ thống **PHẢI** hiển thị tối đa **3 gợi ý nhân sự** kèm lý do ngắn gọn:

```
[AIA] 💡 Gợi ý điều phối cho PROJ-456 (Login Module – High):

1. @le_thi_b — Kỹ năng: Auth/Login ⭐ | Workload: 1 incident | Sẵn sàng ✅
2. @pham_van_c — Kỹ năng: Backend ⭐ | Workload: 2 incidents | Sẵn sàng ✅  
3. @nguyen_thi_d — Kỹ năng: Fullstack | Workload: 0 incidents | Sẵn sàng ✅

👉 Team Lead vui lòng xác nhận phân công.
```

**FR-F6-04:** Hệ thống **KHÔNG ĐƯỢC** tự động phân công nhân sự. Mọi thay đổi phân công **PHẢI** được Team Lead xác nhận thông qua lệnh `/assign PROJ-xxx @username`.

**FR-F6-05:** Hệ thống **PHẢI** cập nhật dữ liệu workload theo thời gian thực khi trạng thái Jira issue thay đổi (qua Jira webhook).

**FR-F6-06:** Hệ thống **NÊN** lưu lịch sử phân công để tránh liên tục gợi ý cùng một nhân sự khi họ vừa xử lý nhiều incident liên tiếp (fatigue prevention).

---

## 4. Yêu cầu phi chức năng

### 4.1 Hiệu năng (Performance)

| ID | Yêu cầu | Chỉ số đo lường |
|---|---|---|
| NFR-P1 | Thời gian phản hồi xác nhận tiếp nhận | ≤ 5 giây kể từ khi nhận tin nhắn (P95). |
| NFR-P2 | Thời gian hoàn thành triage và tạo Jira | ≤ 30 giây kể từ khi nhận tin nhắn (P95). |
| NFR-P3 | Thời gian LLM xử lý một request | ≤ 5 giây (P95). Timeout sau 10 giây. |
| NFR-P4 | Throughput đồng thời | Xử lý ≥ 50 tin nhắn đồng thời từ các group khác nhau. |
| NFR-P5 | Độ trễ semantic matching | ≤ 2 giây cho tập tối đa 1.000 incident đang mở. |
| NFR-P6 | Thời gian phản hồi lệnh bot (/status, /report) | ≤ 3 giây (P95). |

---

### 4.2 Độ tin cậy (Reliability)

| ID | Yêu cầu | Chỉ số đo lường |
|---|---|---|
| NFR-R1 | Độ sẵn sàng hệ thống (Availability) | ≥ 99.9% uptime mỗi tháng (< 43.8 phút downtime/tháng). |
| NFR-R2 | Không mất dữ liệu tin nhắn | Queue tin nhắn chưa xử lý phải được bảo toàn khi restart (persistent queue). |
| NFR-R3 | Xử lý lỗi LLM / Jira API | Retry tự động 3 lần với exponential backoff trước khi ghi lỗi và cảnh báo admin. |
| NFR-R4 | Idempotency | Cùng một tin nhắn không tạo ra hai Jira issue khác nhau dù được xử lý nhiều lần. |
| NFR-R5 | Graceful degradation | Khi LLM API không khả dụng, hệ thống vẫn ghi nhận tin nhắn và thông báo xử lý thủ công. |

---

### 4.3 Bảo mật (Security)

| ID | Yêu cầu | Chi tiết |
|---|---|---|
| NFR-S1 | Xác thực Webhook Telegram | Xác thực chữ ký HMAC-SHA256 với Bot Secret Token trên mỗi request. |
| NFR-S2 | Xác thực Webhook Zalo | Xác thực theo chuẩn Zalo OA (appId + HMAC verification). |
| NFR-S3 | Không lưu nội dung tin nhắn lâu dài | Nội dung tin nhắn thô chỉ được lưu **30 ngày**; sau đó chỉ lưu metadata và dữ liệu có cấu trúc. |
| NFR-S4 | Mã hóa dữ liệu nhạy cảm | API keys, tokens phải được lưu trữ mã hóa (AES-256) và không được hard-code trong source code. |
| NFR-S5 | Phân quyền lệnh bot | Chỉ nhân viên có quyền mới được dùng lệnh admin (`/report`, `/suggest`, `/assign`, `/config`). |
| NFR-S6 | Kiểm toán (Audit Log) | Mọi hành động tạo/cập nhật Jira issue, escalation và phân công đều được ghi log kèm timestamp và user ID. |
| NFR-S7 | Không lưu Jira credentials trong chat | Không bao giờ hiển thị API token hoặc password trong phản hồi group chat. |

---

### 4.4 Khả năng bảo trì & Mở rộng (Maintainability & Scalability)

- **NFR-M1:** Kiến trúc hệ thống **PHẢI** theo dạng **modular/plugin**, cho phép thêm platform mới (Slack, Microsoft Teams) mà không ảnh hưởng đến các module hiện có. Mỗi platform là một adapter riêng biệt.

- **NFR-M2:** LLM provider **PHẢI** được cấu hình động và có thể thay thế (OpenAI GPT-4o, Anthropic Claude, Google Gemini, v.v.) mà không cần code change, chỉ thay đổi file config.

- **NFR-M3:** Tất cả các ngưỡng (SLA duration, similarity threshold, severity criteria, escalation timing) **PHẢI** được cấu hình qua file config (YAML/JSON/ENV), không hard-code.

- **NFR-M4:** Hệ thống **PHẢI** hỗ trợ **horizontal scaling**: chạy nhiều instance song song với shared message queue (Redis Streams hoặc RabbitMQ) mà không gây xử lý trùng lặp.

- **NFR-M5:** Hệ thống **NÊN** cung cấp **health check endpoint** (`GET /health`) để tích hợp với load balancer và monitoring tools (Prometheus, Grafana).

- **NFR-M6:** Code **PHẢI** có coverage test tối thiểu **70%** cho các module F1–F5. Module F2 (AI logic) **NÊN** có test với golden dataset gồm ≥ 100 mẫu tin nhắn.

---

### 4.5 Khả năng sử dụng (Usability)

- **NFR-U1:** Bot **PHẢI** phản hồi bằng **cùng ngôn ngữ** với tin nhắn gốc của khách hàng (tiếng Việt hoặc tiếng Anh).

- **NFR-U2:** Phản hồi của bot trong group chat **PHẢI** ngắn gọn, rõ ràng, **không quá 10 dòng** để không làm ngập group chat.

- **NFR-U3:** Mỗi phản hồi **PHẢI** bao gồm đủ ba yếu tố: (1) xác nhận hành động đã thực hiện, (2) mã Jira hoặc lý do không tạo, (3) bước tiếp theo rõ ràng.

- **NFR-U4:** Bot **PHẢI** sử dụng emoji một cách nhất quán để truyền đạt trạng thái nhanh: ✅ thành công, ⚠️ cảnh báo, 🔴 critical, 🟠 high, 🔄 đang xử lý, ❌ lỗi.

---

## 5. Ràng buộc thiết kế và kiến trúc

### 5.1 Kiến trúc đề xuất

Hệ thống AIA được xây dựng theo kiến trúc **event-driven**, bao gồm các lớp chính:

```
                    ┌──────────────────────────────────────────────┐
                    │               AIA System                     │
                    │                                              │
  Telegram ─────── │ ┌─────────┐   ┌──────────────────────────┐  │
                    │ │Gateway  │──▶│      Message Queue        │  │
  Zalo ──────────── │ │(Webhook │   │   (Redis Streams /        │  │
                    │ │ Layer)  │   │    RabbitMQ)              │  │
                    │ └─────────┘   └──────────┬───────────────┘  │
                    │                          │                   │
                    │               ┌──────────▼───────────────┐  │
                    │               │     AI Processing Layer   │  │
                    │               │  • F1: Intake/Detection   │  │
                    │               │  • F2: Triage/Extraction  │  │
                    │               │  • F3: Incident Matching  │  │
                    │               └──────────┬───────────────┘  │
                    │                          │                   │
                    │         ┌────────────────┼──────────────┐   │
                    │         │                │              │   │
                    │  ┌──────▼──────┐  ┌──────▼──────┐  ┌───▼──┐│
                    │  │ Jira        │  │ SLA Engine  │  │ Data ││
                    │  │ Integration │  │ (F5 Sched.) │  │ Store││
                    │  │ Layer (F4)  │  │             │  │ (PG) ││
                    │  └─────────────┘  └─────────────┘  └──────┘│
                    └──────────────────────────────────────────────┘
                              │                   │
                           Jira API           Resource
                                              Advisor (F6)
```

---

### 5.2 Công nghệ gợi ý

| Thành phần | Công nghệ gợi ý | Lý do |
|---|---|---|
| Backend runtime | Python 3.11+ | Hệ sinh thái AI/ML phong phú; async với FastAPI/asyncio. |
| Web framework | FastAPI | Async, tự động OpenAPI docs, type hints. |
| LLM API | OpenAI GPT-4o / Anthropic Claude 3.5 Sonnet | Hỗ trợ tiếng Việt, function calling cho structured output. |
| Embedding | OpenAI `text-embedding-3-small` | Chi phí thấp, chất lượng tốt cho tiếng Việt và Anh. |
| Vector store | FAISS (in-memory) / Qdrant (production) | Semantic matching nhanh, dễ tích hợp. |
| Message Queue | Redis Streams | Lightweight, at-least-once delivery, tích hợp với cache. |
| Cache | Redis | Cache Jira API response, session state. |
| Database | PostgreSQL 15+ | Lưu incident mapping, SLA log, workload, audit log. |
| Scheduler | APScheduler (Python) | Theo dõi SLA theo interval, in-process. |
| Container | Docker + Docker Compose | Dễ triển khai, horizontal scaling, environment isolation. |
| Monitoring | Prometheus + Grafana | Metrics: latency, throughput, SLA compliance rate. |

---

### 5.3 Ràng buộc tích hợp nền tảng

**Telegram:**
- Tuân thủ rate limit: **30 msg/giây** (global), **20 msg/phút** cho một chat.
- Webhook URL phải là HTTPS với certificate hợp lệ.
- Timeout Telegram webhook: 60 giây — hệ thống phải trả HTTP 200 nhanh, xử lý bất đồng bộ.

**Zalo:**
- Tuân thủ rate limit Zalo OA API theo tier đăng ký.
- Hệ thống **PHẢI** implement exponential backoff khi nhận HTTP 429 (rate limit).
- Zalo OA phải được phê duyệt bởi Zalo trước khi nhận webhook.

**Jira:**
- Hỗ trợ cả **Jira Cloud** (REST API v3) và **Jira Server/Data Center** (REST API v2) với cấu hình chuyển đổi.
- Sử dụng **API Token** (Cloud) hoặc **Personal Access Token** (Server/DC) — không dùng username/password.
- Tuân thủ rate limit Jira: thông thường 100 requests/phút (Cloud), có thể cao hơn tùy cấu hình.

---

## 6. Mô tả Use Case

### 6.1 Danh sách Use Case

| UC ID | Tên Use Case | Tác nhân chính | Module |
|---|---|---|---|
| UC-01 | Báo cáo lỗi qua group chat Telegram | Khách hàng | F1, F2, F3, F4 |
| UC-02 | Báo cáo lỗi qua Zalo Group | Khách hàng | F1, F2, F3, F4 |
| UC-03 | Phát hiện và gộp incident trùng lặp | AIA Bot | F3, F4 |
| UC-04 | SLA vi phạm và leo thang | AIA Bot, Team Lead | F5 |
| UC-05 | Gợi ý điều phối nhân sự khi quá tải | Team Lead | F6 |
| UC-06 | Xem báo cáo SLA tuần/tháng | Manager | F5 |

---

### 6.2 UC-01 – Báo cáo lỗi qua Telegram

| Trường | Chi tiết |
|---|---|
| **Use Case ID** | UC-01 |
| **Tên** | Báo cáo lỗi qua group chat Telegram |
| **Tác nhân** | Khách hàng (người báo), AIA Bot, Nhân viên hỗ trợ, Jira |
| **Tiền điều kiện** | AIA Bot đã được thêm vào Telegram group. Jira đã được cấu hình. Khách hàng là thành viên group. |
| **Kích hoạt** | Khách hàng gửi tin nhắn mô tả lỗi (tự nhiên, mention bot, hoặc dùng /bug). |

**Luồng chính (Happy Path):**

1. Khách hàng gửi tin nhắn: *"App login bị lỗi, nhiều user không vào được từ sáng đến giờ @support_nguyen"*
2. Telegram gửi webhook event đến AIA server.
3. AIA Gateway nhận và validate webhook signature, đưa vào message queue.
4. AI Processor lấy message từ queue, gửi xác nhận: *"[AIA] ✅ Đã nhận báo cáo. Đang phân tích..."*
5. LLM phân tích: xác định đây là bug report (confidence = 0.92).
6. LLM trích xuất: `title="Lỗi đăng nhập"`, `severity=High`, `component="Login"`, `impact_scope={estimated_users: ">10"}`.
7. Semantic matching: không tìm thấy incident trùng (max similarity = 0.45).
8. AIA tạo Jira issue: `PROJ-456` (Priority: High).
9. SLA Engine bắt đầu đếm: deadline = 1 giờ từ timestamp tin nhắn gốc.
10. AIA phản hồi group chat với thông tin đầy đủ (xem FR-F4-03).

**Luồng thay thế:**

- **4a. Tin nhắn không phải bug report** (confidence < 0.40): Bot bỏ qua và ghi log.
- **4b. Không chắc chắn** (confidence ∈ [0.40, 0.70)): Bot hỏi lại xác nhận. Nếu người dùng xác nhận → tiếp tục bước 5. Nếu phủ nhận → ghi log, kết thúc.
- **7a. Tìm thấy incident trùng** (PROJ-123, similarity = 0.87): Bot gộp vào PROJ-123, cập nhật comment, thông báo group kèm link PROJ-123.
- **8a. Jira API lỗi**: AIA lưu vào pending queue, phản hồi *"[AIA] Đã ghi nhận. Đang chờ đồng bộ hệ thống."* Retry sau 30 giây.

**Hậu điều kiện:** Jira issue được tạo/cập nhật. SLA bắt đầu đếm. Incident được lưu trong database AIA. Nhân viên phụ trách nhận thông báo (nếu được mention).

---

### 6.3 UC-02 – Báo cáo lỗi qua Zalo

| Trường | Chi tiết |
|---|---|
| **Use Case ID** | UC-02 |
| **Tên** | Báo cáo lỗi qua Zalo Group |
| **Khác biệt so với UC-01** | Sử dụng Zalo OA API thay vì Telegram Bot API; xác thực Zalo khác; phản hồi có thể có giới hạn ký tự khác. |

Luồng tương tự UC-01, với các điểm khác biệt sau:

- Bước 2: Zalo gửi webhook event theo chuẩn Zalo OA.
- Bước 3: AIA validate theo chuẩn Zalo (appId + HMAC), lấy `sender_id` từ Zalo user object.
- Label trên Jira issue: `["aia-auto", "zalo"]` thay vì `"telegram"`.

---

### 6.4 UC-03 – Phát hiện và gộp incident trùng lặp

| Trường | Chi tiết |
|---|---|
| **Use Case ID** | UC-03 |
| **Tên** | Phát hiện và gộp incident trùng lặp |
| **Tác nhân** | AIA Bot, Jira |
| **Tiền điều kiện** | Đã có ít nhất một incident đang mở trên Jira được AIA tạo ra. |
| **Kích hoạt** | Khách hàng (cùng group hoặc group khác) báo cáo lỗi tương tự. |

**Luồng chính:**

1. Khách hàng ở Group 2 (Zalo) báo: *"Bên tôi cũng không login được app từ khoảng 8h sáng."*
2. AIA trích xuất thông tin → `title="Không login được"`, `component="Login"`, `severity=High`.
3. Semantic matching: tìm thấy PROJ-456 với similarity = 0.89 ≥ 0.80.
4. AIA thêm comment vào PROJ-456: *"Báo cáo trùng lặp từ Zalo Group 2 (08:22): 'Bên tôi cũng không login được app từ khoảng 8h sáng.' — 2 nhóm báo cáo."*
5. AIA kiểm tra: đây là nhóm thứ 2 báo cáo → chưa đủ 3 nhóm để nâng severity.
6. AIA phản hồi Group 2 (Zalo): *"[AIA] 🔄 Sự cố này trùng với PROJ-456 đang xử lý (High). Team kỹ thuật đang làm việc. Cập nhật tiếp theo trong vòng 30 phút."*

**Luồng thay thế:**

- **5a. Đây là nhóm thứ 3 trở lên** báo cáo trong vòng 1 giờ: AIA nâng severity PROJ-456 từ High lên Critical, cập nhật Jira priority, gửi cảnh báo Team Lead.

---

### 6.5 UC-04 – SLA vi phạm và leo thang

| Trường | Chi tiết |
|---|---|
| **Use Case ID** | UC-04 |
| **Tên** | SLA vi phạm và leo thang |
| **Tác nhân** | AIA Bot (SLA Engine), Nhân viên hỗ trợ, Team Lead |
| **Tiền điều kiện** | Incident PROJ-456 (High, SLA 1 giờ) đã được tạo lúc 09:00. Nhân viên @support_nguyen được tag nhưng chưa phản hồi. |

**Luồng chính:**

1. 09:48 (còn 12 phút – 80% SLA): SLA Engine gửi cảnh báo vào group:
   > *"[SLA ⚠️] PROJ-456 (High) còn 12 phút phản hồi. @support_nguyen cần phản hồi ngay!"*

2. 10:00 (100% SLA – vi phạm): Không có phản hồi. AIA:
   - Ghi SLA breach log.
   - Gửi direct message nhắc nhở @support_nguyen (Bước escalation 1).
   - Cập nhật comment Jira: *"[AIA] SLA breach: chưa có phản hồi sau 1 giờ."*

3. 10:10 (vẫn không phản hồi): AIA thông báo công khai vào group (Bước escalation 2):
   > *"[SLA ❌] PROJ-456 đã vượt quá thời hạn phản hồi 10 phút. Team hỗ trợ cần xử lý ngay."*

4. 10:30 (150% SLA = 1h30ph): AIA gửi cảnh báo đến Team Lead (Bước escalation 3):
   > *"[AIA Escalation] PROJ-456 (High) chưa được phản hồi sau 1h30ph. Đề nghị Team Lead can thiệp."*

**Hậu điều kiện:** SLA breach log được ghi. Jira được cập nhật comment. Team Lead đã nhận được cảnh báo.

---

### 6.6 UC-05 – Gợi ý điều phối nhân sự

| Trường | Chi tiết |
|---|---|
| **Use Case ID** | UC-05 |
| **Tên** | Gợi ý điều phối nhân sự khi quá tải |
| **Tác nhân** | Team Lead, AIA Bot |
| **Tiền điều kiện** | PROJ-456 (Critical) vừa được tạo. Kỹ sư phụ trách đang bận với 3 incident High khác. |

**Luồng chính:**

1. Team Lead gửi lệnh: `/suggest PROJ-456`
2. AIA tra cứu: component = Login, kỹ năng cần thiết = Auth/Backend.
3. AIA tính điểm cho từng kỹ sư dựa trên 4 tiêu chí.
4. AIA phản hồi danh sách 3 gợi ý (xem FR-F6-03).
5. Team Lead xác nhận: `/assign PROJ-456 @le_thi_b`
6. AIA cập nhật Jira assignee và workload counter của @le_thi_b.
7. AIA thông báo: *"[AIA] ✅ Đã phân công PROJ-456 cho @le_thi_b."*

---

### 6.7 UC-06 – Xem báo cáo SLA

| Trường | Chi tiết |
|---|---|
| **Use Case ID** | UC-06 |
| **Tên** | Xem báo cáo SLA tuần/tháng |
| **Tác nhân** | Manager |
| **Kích hoạt** | Manager gửi lệnh `/report sla week` hoặc `/report sla month` |

**Luồng chính:**

1. Manager gửi: `/report sla week`
2. AIA truy vấn SLA log từ PostgreSQL cho 7 ngày gần nhất.
3. AIA tính toán và phản hồi:

```
📊 Báo cáo SLA – 7 ngày (24/04 – 30/04/2026)

Tổng incidents: 47
┌─────────┬──────┬────────────┬──────────────┐
│Severity │ Số lượng │ Đúng SLA  │ Tỷ lệ      │
├─────────┼──────┼────────────┼──────────────┤
│Critical │  3   │    3       │  100%  ✅    │
│High     │ 12   │   10       │   83%  ⚠️   │
│Medium   │ 21   │   19       │   90%  ✅    │
│Low      │ 11   │   11       │  100%  ✅    │
└─────────┴──────┴────────────┴──────────────┘

⏱ Avg response time:
• Critical: 8 phút | High: 52 phút | Medium: 2h 15ph | Low: 6h

⚠️ Vi phạm SLA: 2 incident High (PROJ-441, PROJ-449)
```

---

## 7. Ma trận truy xuất yêu cầu

| FR ID | Mô tả tóm tắt | Module | Use Case liên quan | Độ ưu tiên |
|---|---|---|---|---|
| FR-F1-01 | Kết nối Telegram qua Webhook | F1 | UC-01 | Must |
| FR-F1-02 | Kết nối Zalo OA/Group | F1 | UC-02 | Must |
| FR-F1-03 | Nhận tin nhắn văn bản | F1 | UC-01, UC-02 | Must |
| FR-F1-04 | Xác thực Webhook Telegram HMAC | F1 | UC-01 | Must |
| FR-F1-05 | Xác thực Webhook Zalo | F1 | UC-02 | Must |
| FR-F1-06 | Nhận diện phương thức kích hoạt bot | F1 | UC-01, UC-02 | Must |
| FR-F1-07 | Ghi nhận metadata tin nhắn | F1 | UC-01, UC-02 | Must |
| FR-F1-08 | Phản hồi xác nhận trong 5 giây | F1 | UC-01, UC-02 | Must |
| FR-F1-09 | Lọc tin nhắn không liên quan | F1 | UC-01, UC-02 | Should |
| FR-F1-10 | Ghi log quyết định phân loại | F1 | — | Must |
| FR-F2-01 | Phân loại bug bằng LLM | F2 | UC-01, UC-02 | Must |
| FR-F2-02 | Xử lý song ngữ Việt – Anh | F2 | UC-01, UC-02 | Must |
| FR-F2-03 | Hỏi lại khi không chắc chắn | F2 | UC-01, UC-02 | Should |
| FR-F2-04 | Trích xuất thông tin có cấu trúc | F2 | UC-01, UC-02 | Must |
| FR-F2-05 | Structured output / function calling | F2 | UC-01, UC-02 | Must |
| FR-F2-06 | Phân loại severity 4 cấp | F2 | UC-01, UC-04 | Must |
| FR-F2-07 | Tự động nâng severity theo số nhóm báo cáo | F2 | UC-03 | Should |
| FR-F2-08 | Ghi đè severity thủ công | F2 | — | Should |
| FR-F3-01 | Truy vấn incident đang mở từ Jira | F3 | UC-03 | Must |
| FR-F3-02 | Chuyển đổi sang embedding vector | F3 | UC-03 | Must |
| FR-F3-03 | Cosine similarity matching | F3 | UC-03 | Must |
| FR-F3-04 | Ngưỡng trùng lặp cấu hình được | F3 | UC-03 | Must |
| FR-F3-05 | Xử lý gộp incident trùng | F3 | UC-03 | Must |
| FR-F3-06 | Tạo incident mới nếu không trùng | F3 | UC-01, UC-02 | Must |
| FR-F3-07 | Lưu mapping message → incident | F3 | UC-03 | Must |
| FR-F4-01 | Tạo Jira issue tự động | F4 | UC-01, UC-02 | Must |
| FR-F4-02 | Lưu Jira issue key | F4 | UC-01, UC-02 | Must |
| FR-F4-03 | Phản hồi group chat sau khi tạo Jira | F4 | UC-01, UC-02 | Must |
| FR-F4-04 | Xử lý khi Jira API lỗi (pending queue) | F4 | UC-01, UC-02 | Must |
| FR-F4-05 | Thêm comment Jira khi trùng lặp | F4 | UC-03 | Must |
| FR-F4-06 | Nhận Jira webhook khi status thay đổi | F4 | UC-01, UC-02 | Should |
| FR-F4-07 | Cấu hình kết nối Jira | F4 | — | Must |
| FR-F5-01 | Bắt đầu đếm SLA từ timestamp gốc | F5 | UC-04 | Must |
| FR-F5-02 | Cảnh báo tại 80% SLA | F5 | UC-04 | Must |
| FR-F5-03 | Theo dõi tag mà chưa phản hồi | F5 | UC-04 | Must |
| FR-F5-04 | SLA theo giờ làm việc cho Medium/Low | F5 | UC-04 | Should |
| FR-F5-05 | Escalation 3 cấp | F5 | UC-04 | Must |
| FR-F5-06 | SLA breach log | F5 | UC-04, UC-06 | Must |
| FR-F5-07 | Báo cáo SLA qua lệnh chat | F5 | UC-06 | Should |
| FR-F6-01 | Điều kiện kích hoạt điều phối | F6 | UC-05 | Should |
| FR-F6-02 | Thuật toán gợi ý 4 tiêu chí | F6 | UC-05 | Should |
| FR-F6-03 | Hiển thị tối đa 3 gợi ý | F6 | UC-05 | Should |
| FR-F6-04 | Không tự động phân công | F6 | UC-05 | Must |
| FR-F6-05 | Cập nhật workload real-time | F6 | UC-05 | Should |
| FR-F6-06 | Fatigue prevention | F6 | UC-05 | May |

---

## 8. Phụ lục

### 8.1 Ví dụ luồng tin nhắn mẫu

#### Kịch bản 1 – Báo cáo lỗi bằng tiếng Việt (Telegram, incident mới)

```
[09:00] Khách hàng A:
  Anh ơi app bên em login không được, nhiều user bị từ sáng đến giờ rồi,
  check giúp với ạ @support_nguyen 🙏

[09:00] AIA Bot:
  [AIA] ✅ Đã nhận báo cáo. Đang phân tích sự cố...

[09:01] AIA Bot:
  [AIA] 🟠 Đã ghi nhận sự cố mới

  📋 PROJ-456: Lỗi đăng nhập – nhiều người dùng bị ảnh hưởng
  Mức độ: High | Module: Login
  ⏰ Phản hồi trong: 1 giờ (trước 10:01)
  👤 Phụ trách: @support_nguyen
  🔗 https://jira.company.com/browse/PROJ-456

  💬 Gợi ý phản hồi khách hàng:
  "Xin chào! Chúng tôi đã nhận được báo cáo và đang khẩn trương điều tra.
  Vui lòng chờ phản hồi trong vòng 1 giờ. Cảm ơn sự kiên nhẫn của bạn!"
```

#### Kịch bản 2 – Incident trùng lặp từ Zalo Group khác

```
[09:22] Khách hàng B (Zalo Group 2):
  Cho hỏi bên mình đang bị không login được vào app ah,
  từ khoảng 8h sáng, khách hàng phản ánh nhiều

[09:22] AIA Bot (Zalo):
  [AIA] ✅ Nhận báo cáo. Đang phân tích...

[09:23] AIA Bot (Zalo):
  [AIA] 🔄 Đây là sự cố đã được ghi nhận

  PROJ-456: Lỗi đăng nhập (High) – đang xử lý
  Team kỹ thuật đang làm việc khắc phục.
  ⏰ Cập nhật tiếp theo: trước 10:01
  🔗 https://jira.company.com/browse/PROJ-456
```

#### Kịch bản 3 – SLA cảnh báo và leo thang

```
[09:48] AIA Bot (nhắc nhở SLA):
  [SLA ⚠️] PROJ-456 (High) còn 13 phút phản hồi!
  @support_nguyen vui lòng phản hồi khách hàng sớm.

[10:01] AIA Bot (vi phạm SLA):
  [SLA ❌] PROJ-456 đã vượt thời hạn phản hồi 1 giờ.
  @support_nguyen cần xử lý ngay. Đã ghi nhận vi phạm SLA.

[10:11] AIA Bot:
  [SLA Escalation] PROJ-456 (High) chưa có phản hồi sau 70 phút.
  Đã thông báo Team Lead.
```

#### Kịch bản 4 – Báo cáo bằng tiếng Anh

```
[14:30] Customer C (Telegram):
  Hi, payment is failing for our users since 2pm, getting 500 error

[14:30] AIA Bot:
  [AIA] ✅ Report received. Analyzing...

[14:31] AIA Bot:
  [AIA] 🔴 Critical incident logged

  📋 PROJ-460: Payment failure – 500 error (Critical)
  ⏰ Response required within: 15 minutes (before 14:46)
  👤 Assigned: @payment_team
  🔗 https://jira.company.com/browse/PROJ-460

  💬 Suggested response:
  "Hi! We've received your report about the payment issue and our team
  is investigating with highest priority. We'll update you in 15 minutes."
```

---

### 8.2 Schema JSON – Incident Object

```json
{
  "incident_id": "INC-20260415-001",
  "title": "Lỗi đăng nhập – nhiều người dùng bị ảnh hưởng",
  "description": "App không login được, nhiều user bị từ sáng đến giờ. Báo cáo từ Group Telegram #support-acme lúc 09:00 ngày 15/04/2026.",
  "severity": "High",
  "status": "Open",
  "component": "Login",
  "environment": "Production",
  "source_language": "vi",
  "impact_scope": {
    "estimated_users": "nhiều (>10)",
    "groups_reported": 2,
    "platforms": ["telegram", "zalo"]
  },
  "jira_issue_key": "PROJ-456",
  "jira_issue_url": "https://jira.company.com/browse/PROJ-456",
  "platform_sources": [
    {
      "platform": "telegram",
      "group_id": "-100123456789",
      "group_name": "Support ACME",
      "sender_id": "user_12345",
      "sender_name": "Nguyen Van A",
      "message_id": "msg_98765",
      "received_at": "2026-04-15T09:00:12+07:00",
      "mentioned_users": ["support_nguyen"]
    },
    {
      "platform": "zalo",
      "group_id": "zalo_group_xyz",
      "group_name": "Zalo Support Group 2",
      "sender_id": "zalo_user_456",
      "sender_name": "Tran Thi B",
      "message_id": "zalo_msg_11111",
      "received_at": "2026-04-15T09:22:07+07:00",
      "mentioned_users": []
    }
  ],
  "sla": {
    "severity_sla_minutes": 60,
    "started_at": "2026-04-15T09:00:12+07:00",
    "deadline_at": "2026-04-15T10:00:12+07:00",
    "warning_sent_at": "2026-04-15T09:48:00+07:00",
    "first_response_at": null,
    "breached": true,
    "breach_at": "2026-04-15T10:00:12+07:00",
    "escalation_level": 2
  },
  "assigned_to": null,
  "suggested_assignees": ["le_thi_b", "pham_van_c", "nguyen_thi_d"],
  "ai_extraction": {
    "confidence_score": 0.92,
    "model_used": "gpt-4o",
    "extracted_at": "2026-04-15T09:00:17+07:00"
  },
  "created_at": "2026-04-15T09:00:17+07:00",
  "updated_at": "2026-04-15T10:05:30+07:00"
}
```

---

### 8.3 Danh sách lệnh Bot

| Lệnh | Quyền sử dụng | Mô tả |
|---|---|---|
| `/bug [mô tả]` | Tất cả | Báo cáo lỗi trực tiếp với mô tả (tùy chọn). |
| `/incident [mô tả]` | Tất cả | Alias của `/bug`. |
| `/status PROJ-xxx` | Tất cả | Xem trạng thái hiện tại của incident. |
| `/list` | Support, Manager | Liệt kê các incident đang mở theo severity. |
| `/severity PROJ-xxx [level]` | Support, Team Lead | Ghi đè mức severity của incident. |
| `/assign PROJ-xxx @user` | Team Lead, Manager | Phân công incident cho nhân sự. |
| `/suggest PROJ-xxx` | Team Lead, Manager | Xem gợi ý điều phối nhân sự. |
| `/report sla [week\|month]` | Support, Manager | Xem báo cáo SLA. |
| `/ack PROJ-xxx` | Support, Engineer | Xác nhận đã tiếp nhận và đang xử lý. |
| `/resolve PROJ-xxx` | Support, Engineer | Đánh dấu incident đã được giải quyết. |
| `/config` | Admin | Xem cấu hình hiện tại của AIA. |
| `/help` | Tất cả | Xem danh sách lệnh và hướng dẫn sử dụng. |

---

### 8.4 Luồng hoạt động tổng quát (Flow Diagram)

```
Khách hàng gửi tin nhắn
          │
          ▼
┌─────────────────────┐
│  Gateway nhận       │
│  Webhook (TG/Zalo)  │
│  Validate signature │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│  Ghi metadata &     │
│  đưa vào Queue      │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐       ┌────────────────────┐
│  Phản hồi xác nhận  │       │  "Đã nhận báo cáo. │
│  tiếp nhận (≤5s)    │──────▶│   Đang phân tích…" │
└──────────┬──────────┘       └────────────────────┘
           │
           ▼
┌─────────────────────┐
│  F2: LLM Triage     │
│  Confidence Score?  │
└──────────┬──────────┘
           │
    ┌──────┼──────────┐
    │      │          │
  <0.40  [0.40,     >=0.70
    │     0.70)       │
    ▼      │          ▼
 Ignore   Hỏi lại  ┌──────────────────┐
  + log   xác nhận │  F2: Extract     │
           │        │  Structured Info │
           └───────▶│  (title, severity│
                    │  component, ...)  │
                    └────────┬─────────┘
                             │
                             ▼
                    ┌──────────────────┐
                    │  F3: Semantic    │
                    │  Matching        │
                    │  vs Open Issues  │
                    └────────┬─────────┘
                             │
                   ┌─────────┴─────────┐
                   │                   │
              Trùng lặp           Incident mới
           (sim ≥ 0.80)          (sim < 0.60)
                   │                   │
                   ▼                   ▼
          ┌──────────────┐    ┌──────────────────┐
          │ F4: Update   │    │ F4: Create Jira  │
          │ Jira Comment │    │ Issue + Label    │
          └──────┬───────┘    └────────┬─────────┘
                 │                     │
                 └──────────┬──────────┘
                            │
                            ▼
                   ┌──────────────────┐
                   │ Phản hồi Group   │
                   │ (Jira key, SLA,  │
                   │  suggested reply)│
                   └────────┬─────────┘
                            │
                            ▼
                   ┌──────────────────┐
                   │ F5: SLA Engine   │
                   │ Bắt đầu đếm giờ │
                   └────────┬─────────┘
                            │
               ┌────────────┼────────────────┐
               │            │                │
           80% SLA       100% SLA        150% SLA
               │            │                │
               ▼            ▼                ▼
          Cảnh báo     Escalation       Escalation
          group chat   Level 1 & 2      Level 3
                                      (Team Lead)
```

---

*— Hết tài liệu SRS AI Incident Assistant v1.0 —*

*Tài liệu này được soạn thảo theo chuẩn IEEE 830-1998. Mọi thay đổi cần được phê duyệt bởi nhóm phát triển và cập nhật vào bảng Lịch sử thay đổi.*
