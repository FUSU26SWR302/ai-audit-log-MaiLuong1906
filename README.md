# BÀI TẬP CÁ NHÂN — SWR302 (Chương 16 & 17)

> **Trường Đại học FPT Đà Nẵng** | Môn: Software Requirements (SWR302)

| Họ và tên | Mai Văn Lượng |
|---|---|
| Mã số sinh viên | DE190512 |
| Lớp | SE20A07 |
| Ngày nộp | 16/06/2026 |

---

## Mục lục

- [Bài 1 — Phân loại MoSCoW và Phân tích Ưu tiên](#bài-1--phân-loại-moscow-và-phân-tích-ưu-tiên)
  - [1a. Phân loại và Giải thích](#phần-1a--phân-loại-và-giải-thích)
  - [1b. Câu hỏi "Games People Play"](#phần-1b--câu-hỏi-games-people-play)
  - [1c. Điều chỉnh khi Deadline rút ngắn](#phần-1c--điều-chỉnh-khi-deadline-rút-ngắn)
- [Bài 2 — Phân biệt Validation và Verification](#bài-2--phân-biệt-validation-và-verification)
  - [2a. Phân tích 5 Tình huống](#phần-2a--phân-tích-5-tình-huống)
  - [2b. Phân tích sâu TH5](#phần-2b--phân-tích-sâu-tình-huống-th5)
- [Bài 3 — Viết Acceptance Criteria](#bài-3--viết-acceptance-criteria)
  - [3a. Acceptance Criteria (Given–When–Then)](#phần-3a--acceptance-criteria-givenwhen-then)
  - [3b. AC dễ bị bỏ sót](#phần-3b--ac-dễ-bị-bỏ-sót)
  - [3c. Thiết kế Test Case](#phần-3c--thiết-kế-test-case)

---

## Bài 1 — Phân loại MoSCoW và Phân tích Ưu tiên

*(Chương 16 — 35 điểm)*

**Ngữ cảnh:** Ứng dụng đặt lịch khám bệnh trực tuyến tại phòng khám tư nhân Đà Nẵng. Deadline 8 tuần, nhóm 3 developer.

---

### Phần 1a — Phân loại và Giải thích

| Mã | Mô tả Requirement | Phân loại MoSCoW |
|---|---|---|
| R01 | Bệnh nhân đăng ký lịch khám bằng số điện thoại và OTP | 🔴 **Must Have** |
| R02 | Bác sĩ xem lịch khám trong ngày trên app mobile | 🔴 **Must Have** |
| R03 | Hệ thống tự động gửi SMS nhắc lịch khám trước 2 giờ | 🟡 **Should Have** |
| R04 | Bệnh nhân xem lịch sử khám và đơn thuốc cũ | 🔵 **Could Have** |
| R05 | Giám đốc xem báo cáo doanh thu theo tháng (biểu đồ) | ⚫ **Won't Have** |
| R06 | Hệ thống cho phép đặt lịch tại 3 cơ sở khác nhau của phòng khám | 🔴 **Must Have** |
| R07 | Tích hợp thanh toán trực tuyến (VNPay, MoMo) | 🟡 **Should Have** |
| R08 | Bác sĩ ghi chú điện tử thay vì hồ sơ giấy | 🔵 **Could Have** |
| R09 | Bệnh nhân đánh giá dịch vụ sau khi khám (1–5 sao) | ⚫ **Won't Have** |
| R10 | Hệ thống hiển thị thời gian chờ dự kiến theo thời gian thực | ⚫ **Won't Have** |

#### Giải thích các Must Have Requirements

**R01 — Đăng ký lịch khám bằng số điện thoại và OTP**

Đây là điểm khởi đầu của toàn bộ luồng nghiệp vụ. Nếu bỏ requirement này, hệ thống không thể xác định danh tính bệnh nhân, không có cơ chế đặt lịch và mọi tính năng còn lại đều vô nghĩa. Bệnh nhân không thể tạo bất kỳ cuộc hẹn nào — mục đích chính của ứng dụng hoàn toàn sụp đổ.

**R02 — Bác sĩ xem lịch khám trong ngày trên app mobile**

Nếu bác sĩ không thể xem lịch khám, toàn bộ dữ liệu do bệnh nhân nhập vào không có giá trị sử dụng ở phía vận hành phòng khám. Hệ thống chỉ thu thập dữ liệu một chiều mà không phục vụ được bên tiếp nhận — đây là thất bại vận hành nghiêm trọng, không thể bàn giao sản phẩm.

**R06 — Đặt lịch tại 3 cơ sở khác nhau**

Ngữ cảnh đã nêu rõ đây là phòng khám tư nhân có 3 cơ sở. Nếu thiếu requirement này, bệnh nhân không biết đặt lịch ở cơ sở nào, bác sĩ ở các cơ sở khác nhau không nhận được đúng lịch của mình. Toàn bộ hệ thống sẽ gây nhầm lẫn vận hành và không phản ánh đúng thực tế kinh doanh của phòng khám.

---

### Phần 1b — Câu hỏi "Games People Play"

#### Should Have thứ 1: R03 — Hệ thống tự động gửi SMS nhắc lịch khám trước 2 giờ

1. Nếu hệ thống chưa gửi được SMS tự động, phòng khám có thể nhờ nhân viên lễ tân gọi điện nhắc bệnh nhân thủ công không? Chi phí thêm nhân lực đó có đáng kể hơn chi phí phát triển tính năng SMS trong 8 tuần đầu không?

2. Tỉ lệ bệnh nhân quên lịch hoặc đến trễ hiện tại là bao nhiêu phần trăm? Nếu chỉ gửi nhắc nhở qua ứng dụng (push notification) thay vì SMS, tỉ lệ đó có giảm đủ để chấp nhận được không?

3. Đăng ký dịch vụ SMS Brandname với nhà mạng tại Việt Nam cần duyệt hồ sơ 7–10 ngày. Nếu tính năng này chưa sẵn sàng lúc ra mắt, phòng khám có chấp nhận dùng ứng dụng trước rồi bổ sung SMS sau khi đã hoàn tất đăng ký không?

#### Should Have thứ 2: R07 — Tích hợp thanh toán trực tuyến (VNPay, MoMo)

1. Hiện tại phòng khám xử lý thanh toán như thế nào? Nếu giữ nguyên hình thức trả tiền mặt tại quầy sau khi khám, liệu trải nghiệm bệnh nhân có bị ảnh hưởng đủ nghiêm trọng để ưu tiên tính năng này ngay trong phiên bản đầu tiên không?

2. Tích hợp cổng thanh toán yêu cầu ký hợp đồng doanh nghiệp với VNPay/MoMo và xử lý hoàn tiền, tranh chấp giao dịch. Phòng khám đã chuẩn bị quy trình nghiệp vụ nội bộ cho những tình huống này chưa, hay vẫn cần thêm thời gian?

3. Nếu phát sinh lỗi giao dịch trong quá trình đặt lịch (ví dụ: bệnh nhân bị thu tiền nhưng lịch không được tạo), phòng khám có đội ngũ kỹ thuật hỗ trợ hoặc quy trình xử lý khiếu nại 24/7 không? Đây có phải rủi ro vận hành có thể chấp nhận ngay từ ngày đầu không?

---

### Phần 1c — Điều chỉnh khi Deadline rút ngắn còn 5 tuần

Khi deadline giảm từ 8 tuần xuống còn 5 tuần, nhóm mất đi **37.5% thời gian phát triển**. Với đội ngũ 3 developer, cần loại bỏ ngay các tính năng có độ phức tạp kỹ thuật cao hoặc phụ thuộc vào bên thứ ba.

**R03 (Should Have → Won't Have)**

SMS nhắc lịch yêu cầu tích hợp với nhà cung cấp dịch vụ SMS bên ngoài, đăng ký Brandname với nhà mạng (7–10 ngày riêng cho thủ tục hành chính), và xử lý lỗi gửi tin. Với 5 tuần, thời gian này chiếm tỉ lệ quá cao. Giải pháp thay thế tạm thời là gửi push notification qua app, hoàn toàn khả thi với nguồn lực hiện có.

**R07 (Should Have → Won't Have)**

Tích hợp thanh toán trực tuyến là tính năng phức tạp nhất về kỹ thuật (xử lý callback, hoàn tiền, bảo mật giao dịch) và cả về pháp lý (hợp đồng với VNPay/MoMo). Cắt tính năng này giải phóng khoảng 30–40% công sức dev trong giai đoạn nước rút, đồng thời tránh rủi ro ra mắt sản phẩm có tính năng thanh toán chưa được kiểm tra kỹ — điều cực kỳ nguy hiểm đối với uy tín phòng khám.

---

## Bài 2 — Phân biệt Validation và Verification

*(Chương 17 — 30 điểm)*

---

### Phần 2a — Phân tích 5 Tình huống

---

#### TH1: Tester kiểm tra chức năng đăng nhập theo SRS

| | |
|---|---|
| **Loại** | ✅ **VERIFICATION** |
| **Giải thích** | Tester đối chiếu hành vi hệ thống với tài liệu SRS đã được phê duyệt — đây là hoạt động kiểm tra *"Are we building the product right?"*. Không có sự tham gia của người dùng cuối hay đánh giá nhu cầu thực tế, chỉ đảm bảo phần mềm hoạt động đúng đặc tả kỹ thuật. |

---

#### TH2: BA mời 3 bác sĩ dùng thử prototype và hỏi về sự phù hợp quy trình

| | |
|---|---|
| **Loại** | ✅ **VALIDATION** |
| **Giải thích** | BA đang kiểm tra xem sản phẩm có giải quyết đúng vấn đề thực tế của người dùng (bác sĩ) không — đây là câu hỏi *"Are we building the right product?"*. Việc dùng prototype để thu thập phản hồi từ người dùng cuối trong bối cảnh công việc thực của họ là hoạt động Validation điển hình, không liên quan đến đặc tả kỹ thuật. |

---

#### TH3: Team review SRS để đảm bảo mỗi use case có ít nhất 1 acceptance test

| | |
|---|---|
| **Loại** | ✅ **VERIFICATION** |
| **Giải thích** | Hoạt động này kiểm tra tính nhất quán và đầy đủ trong nội bộ tài liệu — đảm bảo SRS được xây dựng đúng quy trình (mỗi use case phải có test tương ứng). Đây là kiểm tra chất lượng của artifact (tài liệu), không phải kiểm tra xem tài liệu đó có phản ánh đúng nhu cầu người dùng không — đặc trưng của Verification. |

---

#### TH4: PM so sánh business requirements với software requirements để tìm chỗ "dịch" sai

| | |
|---|---|
| **Loại** | ✅ **CẢ HAI (Verification + Validation)** |
| **Giải thích** | *Về Verification:* PM kiểm tra xem software requirements có được chuyển dịch đúng từ business requirements không (tính nhất quán giữa các tài liệu). *Về Validation:* Đồng thời hành động này kiểm tra xem các yêu cầu phần mềm có phản ánh trung thực nhu cầu nghiệp vụ thực sự của phòng khám không. Đây là hoạt động tracing ngược (traceability review) có tính hai chiều. |

---

#### TH5: 200 automated tests PASS nhưng giám đốc từ chối nghiệm thu

| | |
|---|---|
| **Loại** | ⚠️ **VERIFICATION PASS — VALIDATION FAIL** |
| **Giải thích** | Tất cả 200 test pass chứng minh hệ thống làm đúng những gì SRS quy định (Verification thành công). Tuy nhiên bản thân SRS đã ghi sai nhu cầu thực tế — bắt buộc nhập cả CMND lẫn thẻ BHYT là yêu cầu sai so với thực tế vận hành. Validation không được thực hiện sớm nên lỗi sai nhu cầu không bị phát hiện cho đến khi demo. |

---

### Phần 2b — Phân tích sâu Tình huống TH5

#### 1. Điều gì đã xảy ra?

Đây là trường hợp kinh điển của lỗi Validation mà Verification không thể bắt được. Hệ thống đã trải qua toàn bộ vòng đời phát triển với đặc tả sai nhưng không ai phát hiện vì sai sót nằm ở tầng yêu cầu, không phải tầng code.

Verification trả lời câu hỏi: *"Phần mềm có làm đúng những gì SRS yêu cầu không?"* — và câu trả lời là CÓ, 200 test đều pass. Nhưng không ai hỏi câu hỏi Validation: *"SRS có phản ánh đúng nhu cầu thực sự của phòng khám không?"* Kết quả là nhóm xây đúng thứ sai — họ xây chính xác một hệ thống không ai cần theo cách đó.

Nguồn gốc lỗi nằm ở giai đoạn elicitation: BA đã không xác nhận lại với giám đốc rằng yêu cầu nhập đồng thời cả CMND lẫn BHYT là quy định bắt buộc hay chỉ là ý muốn tạm thời. Nếu đã hỏi, giám đốc chắc chắn sẽ nói rằng thực tế bệnh nhân thường chỉ có một trong hai.

#### 2. Nếu là BA, tôi đã ngăn chặn như thế nào?

**Giai đoạn Elicitation (sớm nhất):** Tổ chức workshop với giám đốc và ít nhất 2–3 nhân viên lễ tân để thu thập yêu cầu. Không chỉ nghe ý kiến giám đốc mà còn quan sát trực tiếp quy trình đăng ký tại phòng khám để hiểu những trường hợp ngoại lệ (bệnh nhân không có BHYT, bệnh nhân cấp cứu...).

**Giai đoạn SRS Review (trước khi đóng băng):** Tổ chức buổi Validation Review: mời giám đốc và đại diện người dùng cuối (bác sĩ, lễ tân) đọc qua SRS và xác nhận từng yêu cầu. Đặc biệt yêu cầu họ ký tên xác nhận vào mục liên quan đến xác thực danh tính bệnh nhân.

**Giai đoạn Prototype (sprint 1–2):** Xây dựng clickable prototype cho luồng đặt lịch và demo cho giám đốc trước khi viết một dòng code thật. Sai sót yêu cầu được phát hiện ở giai đoạn này chỉ tốn vài giờ sửa wireframe, thay vì tốn hàng tuần rewrite code sau khi đã build xong.

#### 3. Hai hoạt động Validation cụ thể trước khi bàn giao

**User Acceptance Testing (UAT) có kiểm soát:** Tổ chức 2–3 buổi UAT với người dùng thực: bệnh nhân thử đặt lịch trên thiết bị thật, bác sĩ thử xem lịch và xác nhận cuộc hẹn. BA quan sát và ghi nhận mọi điểm người dùng bị lúng túng hoặc không hiểu, sau đó tổng hợp danh sách cần điều chỉnh trước khi nghiệm thu chính thức.

**Pilot Run giới hạn (vận hành thử):** Trước khi bàn giao toàn bộ, chạy thử hệ thống với một cơ sở nhỏ nhất trong 1 tuần với 20–30 bệnh nhân tình nguyện. Theo dõi số liệu thực tế: tỉ lệ đặt lịch thành công, số cuộc gọi nhầm, phản hồi bác sĩ. Kết quả pilot là bằng chứng Validation mạnh nhất để giám đốc tự tin ký nghiệm thu.

---

## Bài 3 — Viết Acceptance Criteria

*(Chương 17 — 35 điểm)*

> **User Story:** *"Là bệnh nhân, tôi muốn đặt lịch khám trực tuyến qua điện thoại để không cần đến phòng khám chỉ để lấy số thứ tự."*

---

### Phần 3a — Acceptance Criteria (Given–When–Then)

#### AC1 — Đặt lịch thành công (Happy Path)

| | |
|---|---|
| **Given** | Bệnh nhân đã cài đặt ứng dụng, đăng nhập thành công bằng số điện thoại và OTP. Cơ sở khám còn ít nhất 1 slot trống trong khung giờ bệnh nhân chọn. |
| **When** | Bệnh nhân chọn cơ sở, chọn bác sĩ, chọn ngày và giờ, nhấn nút "Xác nhận đặt lịch". |
| **Then** | Hệ thống tạo mã đặt lịch duy nhất (ví dụ: DN-2026-001234), hiển thị màn hình xác nhận với đầy đủ thông tin (tên bác sĩ, cơ sở, ngày giờ, mã lịch). Slot vừa đặt bị ẩn khỏi danh sách trống cho người dùng khác trong vòng 5 giây. |

#### AC2 — Đặt lịch thất bại do slot đã đầy

| | |
|---|---|
| **Given** | Bệnh nhân đã đăng nhập. Bác sĩ A tại cơ sở B vào lúc 9:00 ngày X đã có bệnh nhân khác đặt trước. |
| **When** | Bệnh nhân cố gắng chọn đúng slot 9:00 của bác sĩ A và nhấn "Xác nhận đặt lịch". |
| **Then** | Hệ thống hiển thị thông báo lỗi rõ ràng: *"Khung giờ này đã được đặt. Vui lòng chọn khung giờ khác."* Hệ thống đề xuất tự động 3 slot gần nhất còn trống với cùng bác sĩ hoặc bác sĩ khác tại cùng cơ sở. Không có bất kỳ giao dịch đặt lịch nào được tạo ra trong hệ thống. |

#### AC3 — Xác thực OTP thất bại quá 3 lần

| | |
|---|---|
| **Given** | Bệnh nhân vừa yêu cầu gửi OTP đến số điện thoại đã đăng ký. OTP có hiệu lực trong 5 phút. |
| **When** | Bệnh nhân nhập sai mã OTP 3 lần liên tiếp trong phiên đăng nhập hiện tại. |
| **Then** | Sau lần thứ 3 nhập sai, hệ thống khóa phiên đăng nhập hiện tại và hiển thị thông báo: *"Bạn đã nhập sai OTP 3 lần. Vui lòng yêu cầu mã mới sau 10 phút."* Nút "Gửi lại OTP" bị vô hiệu hóa trong 10 phút. Không có phiên đăng nhập nào được tạo ra. |

#### AC4 — Giới hạn số lịch đặt trong ngày (Anti-spam)

| | |
|---|---|
| **Given** | Bệnh nhân đã đăng nhập và trong ngày hôm đó đã có 2 lịch khám đang hoạt động (chưa bị hủy, chưa qua ngày khám). |
| **When** | Bệnh nhân cố gắng đặt thêm lịch khám thứ 3 trong cùng ngày bằng cách chọn slot và nhấn "Xác nhận đặt lịch". |
| **Then** | Hệ thống từ chối yêu cầu và hiển thị thông báo: *"Bạn đã đặt tối đa 2 lịch hẹn trong hôm nay. Vui lòng hủy một lịch hiện tại hoặc đặt lịch vào ngày khác."* Không có lịch mới nào được tạo ra trong cơ sở dữ liệu. |

---

### Phần 3b — AC dễ bị bỏ sót

#### 1. AC nào dễ bị bỏ sót nhất?

**AC4 — giới hạn số lịch đặt trong ngày** là AC dễ bị bỏ sót nhất trong thực tế. Khi team tiếp nhận user story "muốn đặt lịch trực tuyến", suy nghĩ đầu tiên của tất cả mọi người là luồng đặt thành công và các lỗi kỹ thuật thông thường (slot đầy, OTP sai). Không ai tự nhiên nghĩ đến kịch bản một người đặt nhiều lịch để "chiếm chỗ" hoặc cò mồi spam hệ thống — đó là tư duy về hành vi người dùng xấu, cần kinh nghiệm thực tế mới nhận ra.

#### 2. Tại sao AC này quan trọng?

Nếu thiếu AC này, hệ thống không có bất kỳ giới hạn nào về số lịch đặt per ngày per user. Hậu quả thực tế:

- Cò mồi hoặc đối thủ cạnh tranh có thể dùng script tự động đặt hàng chục lịch rồi hủy sát giờ, khiến các slot trông như đã đầy và bệnh nhân thật không đặt được.
- Trong mùa dịch hoặc cao điểm, một bệnh nhân thiếu ý thức có thể đặt 5–6 slot ở nhiều cơ sở cùng lúc "cho chắc" rồi chỉ đến 1 chỗ, làm tổn thất doanh thu phòng khám.
- Phòng khám mất khả năng dự báo lượng bệnh nhân thực sự trong ngày, ảnh hưởng đến bố trí nhân sự và y dụng cụ.

#### 3. AC này ngăn chặn lỗi phát triển như thế nào?

Khi AC4 tồn tại trong đặc tả, developer sẽ viết business logic kiểm tra số lượng active booking của user trong ngày **trước** khi tạo record mới. QA sẽ viết Negative Test Case: *"Đặt lịch thứ 3 trong ngày phải bị từ chối"* và chạy test đó trong mỗi sprint. Nếu không có AC này, cả developer lẫn QA đều không biết đây là yêu cầu — không ai implement, không ai test, và bug này chỉ lộ ra khi hệ thống đã live và bị khai thác.

---

### Phần 3c — Thiết kế Test Case

| | |
|---|---|
| **AC được chọn** | AC1 — Đặt lịch thành công: Bệnh nhân đăng nhập thành công và còn slot trống → hệ thống tạo mã lịch và hiển thị màn hình xác nhận. |
| **Tên test case** | `TC_BOOKING_001`: Đặt lịch khám trực tuyến thành công với đầy đủ điều kiện hợp lệ |
| **Điều kiện tiên quyết** | 1. Bệnh nhân có tài khoản hợp lệ với số điện thoại `0901234567` <br>2. Đã đăng nhập thành công (OTP đúng) <br>3. Bác sĩ Nguyễn Văn A tại cơ sở Đà Nẵng 1 còn slot trống lúc 10:00 ngày 20/06/2026 <br>4. Trong ngày 20/06/2026, bệnh nhân chưa có lịch khám nào |
| **Các bước thực hiện** | 1. Mở ứng dụng và đăng nhập <br>2. Chọn "Đặt lịch khám mới" <br>3. Chọn cơ sở: "Phòng khám Đà Nẵng 1" <br>4. Chọn bác sĩ: "Nguyễn Văn A" <br>5. Chọn ngày: 20/06/2026 <br>6. Chọn giờ: 10:00 <br>7. Nhấn nút "Xác nhận đặt lịch" <br>8. Chụp màn hình kết quả |
| **Dữ liệu thử** | Tài khoản: `0901234567` / OTP: `123456` <br>Cơ sở: Đà Nẵng 1 \| Bác sĩ: Nguyễn Văn A <br>Ngày: 20/06/2026 \| Giờ: 10:00 AM |
| **Kết quả mong đợi** | • Màn hình xác nhận hiển thị trong vòng 3 giây <br>• Mã lịch được tạo đúng định dạng: `DN-2026-XXXXXX` <br>• Thông tin hiển thị: Bác sĩ Nguyễn Văn A, Cơ sở Đà Nẵng 1, 10:00 ngày 20/06/2026 <br>• Slot 10:00 biến mất khỏi danh sách trống trong vòng 5 giây trên thiết bị khác <br>• Bệnh nhân nhận được push notification xác nhận trong vòng 1 phút |
| **Kết quả thực tế** | *(Để trống — tester điền sau khi chạy test)* |

---

*Họ và tên: Mai Văn Lượng | MSSV: DE190512 | Lớp: SE20A07 | SWR302 — Chương 16 & 17 | 16/06/2026*
