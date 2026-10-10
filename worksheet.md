# Worksheet — P-100

Nguyễn Văn An · 2A202602776 · 10/10/2026 (GMT+7)

## Số liệu đầu vào — kịch bản pilot B2B2C

Các số dưới đây là giả định tài chính cho lab. Một đơn vị khách trả tiền là **đại lý/xưởng**, không phải chủ xe. Kịch bản chuẩn: 500 phiên thử/tháng/partner, 400 booking được xưởng xác nhận; rev-share = 0% trong pilot bán trực tiếp. Hợp đồng có chia sẻ doanh thu phải tính lại ngưỡng trước khi áp dụng.

| Đầu vào | Giá trị dùng trong lab | Nguồn / cách xác định |
|---|---|---|
| ARPU | 9.500.000đ/partner/tháng | 1.500.000 + 20.000 × 400; `3_Value_Metric!B31:B32`; thay ô ARPU rời rạc `4_Channel_Fit!B5` bằng phép tính nhất quán |
| GM mục tiêu / GM mô hình | ≥60% / 74,43199% sau rev-share giả định 0% | Mục tiêu `2_Pricing!B32`; GM tính lại từ Hybrid và COGS bổ sung |
| CAC pilot giả định | 3.759.200đ/partner trả phí mới | 12 giờ founder × 9 USD/giờ + 40 USD đi lại; mức 9 USD/giờ từ `1_Cost_Job!B50`, 12 giờ và 40 USD là giả định bổ sung |
| Payback mục tiêu | ≤12 tháng; mô hình khoảng 0,532 tháng | `4_Channel_Fit!B7:B8` chọn SMB; dùng như chính sách của mô hình, không như benchmark đã xác minh |
| Runway | 6 tháng nếu 2 pilot miễn phí, không có doanh thu | Giả định quỹ pilot 90.107.531đ / burn 15.017.922đ/tháng; MH-5 |
| Value Metric | Hybrid: phí nền + booking lần đầu được Cố vấn dịch vụ xác nhận | `3_Value_Metric!B31:B32`, điều chỉnh điều kiện hoàn tất theo PRD FR-06 |
| Cost/Job gốc / điều chỉnh | 5.333,23đ / 6.072,40đ mỗi booking xác nhận | Tự tính công thức `1_Cost_Job!B66:B69`; thêm DMS 10 USD/tháng và Zalo OA 41.667đ/tháng từ critique log |
| Overhead | 10.160.000đ/tháng toàn dự án | `1_Cost_Job!B59 = 400 USD`, tỷ giá mô hình `B68 = 25.400đ/USD`; R&D/Sales là OPEX, không đưa vào GM |

CAC 32.000 USD trong `4_Channel_Fit!B20:B22` chỉ là kịch bản sales (8.000/25%), không phải CAC thực đo. Không dùng GM 84,8% theo mức giá 35.000đ/job cho mô hình Hybrid. Không coi tỷ giá, giá API, SMS hay hợp tác VinFast trong Day22 là dữ kiện hiện hành đã xác minh.

**Định nghĩa job:** một `booking_id` thật chuyển lần đầu sang Confirmed bởi Cố vấn dịch vụ, sau khi chủ xe đã chọn hạng mục và gửi yêu cầu. Đếm một lần; loại seed/test, booking trùng, lượt gửi notification, Pending và booking bị hủy trước xác nhận. Không đặt điều kiện SMS thành công vì kênh thông báo trong PRD còn mở. Hủy sau xác nhận được ghi vào chất lượng và xử lý đối soát hóa đơn; chưa có hợp đồng thì doanh thu chỉ là mô hình.

400/500 = 80% là giả định tỷ lệ xác nhận, **không** khẳng định AI tự hoàn tất 80% không có người. Hai xác nhận chuẩn của PRD không tính vào tỷ lệ escalation. Chi phí thời gian xác nhận tại xưởng do partner chịu trong biến thể A; nếu P-100 gánh nhân sự đó thì phải thêm vào COGS.

## Trạm 1 — Loại mô hình

- **Ai trả tiền:** đại lý/xưởng, theo kịch bản thương mại Day22; chưa dùng làm bằng chứng khách đã trả tiền.
- **Ai dùng:** chủ xe điện nhận kế hoạch/đặt lịch; Cố vấn dịch vụ nhận và xác nhận booking, chuẩn bị phụ tùng/cập nhật tiến độ.
- **Chạm end-user:** tài khoản Owner và luồng AI hỗ trợ trong ứng dụng P-100; cần quyền đo event và nhận diện partner theo thỏa thuận pilot. Mô hình giả định giữ bề mặt/thương hiệu P-100, không white-label ẩn hoàn toàn.

**Câu chốt loại:** P-100 chọn B2B2C vì đại lý/xưởng dự kiến trả phí, chủ xe là khách của xưởng và dùng trực tiếp ứng dụng Owner P-100 để hiểu kế hoạch rồi đặt lịch, còn xưởng xử lý trên cổng Advisor.

PRD cho thấy mô hình tương tác; lựa chọn B2B2C do tác giả xác nhận ngày 10/10. Tài liệu chưa chứng minh quan hệ thương mại hôm nay. Nếu pilot chỉ cung cấp phần mềm cho nhân viên xưởng, không cho tiếp cận/đo người dùng cuối thì phải chuyển bảng B2B.

**Toàn bộ bảng §3.3:** không có đèn được đánh ✅ chỉ từ PRD hay smoke test. 🔧 nghĩa là có cách thu trong pilot, không bảo đảm đã có cohort đủ tuổi.

| Đèn trong HANDBOOK | Trạng thái | Cần gì / lịch có số |
|---|---|---|
| Partner activation rate | 🔧 | `partner_id`, ngày go-live, end-user thật; hai cohort 30 ngày, baseline 09/12/2026 |
| End-user reach trong partner | 🔧 | Danh sách khách đủ điều kiện có đồng ý, event xem kế hoạch; 2 tuần baseline 24/10, đánh đỏ sau 60 ngày |
| Time-to-first-end-user | 🔧 | Ngày ký và event chủ xe thật đầu tiên; ghi cả partner chưa activate, baseline 09/12 |
| Volume volatility | 🔧 | Phiên thử theo partner; 2 tháng đủ lịch 09/12; không chọn trong 7 đèn vì cửa sổ dài ở pilot |
| GM sau rev-share | 🔧 | Doanh thu đối soát, điều khoản chia, COGS riêng partner; thiết lập sổ chi phí 24/10, số tháng đầu 09/11 |
| Inference / doanh thu từng partner | 🔧 | Trace token/model/retry theo partner + giá hóa đơn; thiết lập 24/10, tháng đầu 09/11 |
| Tập trung volume | 🔧 | Booking confirmed theo partner, loại seed; 24/10; chưa chọn vì 1–2 pilot làm tỷ lệ tự nhiên rất cao |
| Chất lượng nhìn từ end-user | 🔧 | Đối soát Confirmed/Completed/hủy, phản hồi có consent; 24/10; bắt buộc kiểm tra nguồn theo PRD |
| Doanh thu/partner · NRR · GM tổng | 🔧 / ❌ | ARPU và GM tháng: sổ đối soát 09/11; NRR: ❌ chưa có cohort hợp đồng gia hạn hoặc lịch ký để định ngày đo |

## Trạm 2 — 7 thẻ đèn / đúng 3 tầng

**North Star:** D1 Partner activation rate trong 30 ngày. Hiện tại chưa có số pilot được cung cấp; mục tiêu thử nghiệm ≥60%. Chuỗi: kích hoạt xưởng → chủ xe thật → booking xác nhận → doanh thu/partner → CAC payback.

| ID / Tầng | Đèn và định nghĩa (đếm / loại) | Công thức | Nhịp / người lấy | Báo trước cho / khi đỏ |
|---|---|---|---|---|
| D1 / L | Partner activation: partner go-live có ≥1 chủ xe thật xem kế hoạch đúng context trong 30 ngày đầu; loại nhân viên/test | Trong các partner đủ 30 ngày, số đã đạt điều kiện trong 30 ngày đầu / tổng partner đủ 30 ngày; mẫu 0 → không tính tỷ lệ | Tuần / An | D6 doanh thu/partner trong 2–4 tuần; R1 |
| D2 / L | Reach riêng từng partner: khách đủ điều kiện đã xem kế hoạch P-100; khử trùng owner_id, không đếm mở trang đăng nhập | Chủ xe thật đã xem kế hoạch / cơ sở khách đủ điều kiện có consent tại go-live; bổ sung danh sách phải tạo cohort mới | Tuần / An + đầu mối xưởng | D6 doanh thu/partner trong 2–4 tuần; R2 |
| D3 / L | Time-to-first-end-user: ngày từ ký pilot đến chủ xe thật đầu tiên xem kế hoạch; không phải cài xong, không loại partner chưa có user | Ngày event đầu − ngày ký; partner chưa có event dùng tuổi từ ngày ký và gắn “đang chờ” | Tuần / An | D1 activation → D6 doanh thu; R3 |
| D4 / O | Inference/doanh thu từng partner: LLM + embedding truy vấn + retry + gọi lỗi có tính phí; không trộn các partner | Tổng inference trong tháng / doanh thu phần mềm tháng cùng partner; doanh thu 0 có cost → đỏ | Tuần dự báo, tháng chốt / An | D5 GM sau rev-share → D7 payback; R4 |
| D5 / O | GM sau rev-share từng partner: biên gộp phần mềm; COGS có infra, messaging, DMS vận hành, QA/support và inference; loại R&D/Sales OPEX | (Doanh thu − rev-share − COGS) / doanh thu; doanh thu 0 → không tính % | Tháng / An, xưởng đối soát | D7 payback; R5 |
| D6 / G | ARPU thực thuần từng partner: doanh thu đã ghi nhận, trừ giảm giá/hoàn tiền; không phải hóa đơn bảo dưỡng của xưởng | Phí nền + đơn giá × booking tính tiền − giảm giá/hoàn; tháng đủ kỳ, không bình quân che partner yếu | Tháng / An | Bảng điểm của D1–D3, đầu vào D5/D7; đỏ: An dừng mở rộng quảng bá tại partner, đối soát phễu trong 2 ngày |
| D7 / G | CAC payback ước tính cập nhật: số tháng cần từ lãi gộp thực đo; chưa phải bằng chứng đã thu hồi CAC | CAC gồm giờ bán + chi phí kênh / lãi gộp tháng trung bình 2 tháng của cohort partner mới; lãi gộp ≤0 → vô hạn | Tháng, kiểm quý / An | Bảng điểm của D4–D6, quyết định ngân sách; đỏ: An đóng băng tăng chi acquisition trong 1 ngày |

3 Leading, 2 Operating, 2 Lagging; D4 bắt chi phí AI trước khi GM chốt. Lagging là kết quả của chuỗi, không gắn nhãn “báo trước” giả tạo. Bảo hành/kỹ thuật bịa nguồn kích hoạt chặn ca và chuyển người ngay theo NFR-01/BR-03, không chờ mẫu lớn hay tối ưu cost.

## Trạm 3 — Ngưỡng có nguồn

[TB] dưới đây là “chưa có chuẩn, đo 2 chu kỳ rồi lấy làm baseline”; số ban đầu dùng từ khung §3.3 như giả thuyết thử nghiệm. Không gọi chúng là benchmark. Lưu phiên bản ngưỡng trước pilot; không đổi hồi tố để biến ca đỏ thành xanh. Với màu vàng, An phải điều tra và chốt sửa một nguyên nhân trong 14 ngày.

| ID | 🟢 | 🟡 | 🔴 | Nguồn / lý do / lịch baseline |
|---|---|---|---|---|
| D1 | ≥60% | 30% đến <60% | <30% | [TB], ưu tiên kích hoạt thay vì ký thêm, khung §3.3; 2 cohort 30 ngày, 09/12 |
| D2 | ≥15% | 5% đến <15% | <5% khi partner đủ 60 ngày | [TB], thử phễu tiếp cận trước khi thêm feature; 2 chu kỳ tuần 24/10, đỏ chỉ ở cohort đủ tuổi |
| D3 | <30 ngày | 30–60 ngày | >60 ngày | [TB], giới hạn thời gian học trước khi mất 2/3 chiến dịch; 2 cohort, 09/12; chưa có user vẫn tăng tuổi chờ |
| D4 | ≤8,24% | >8,24% đến ≤16,48% | >16,48% | [MH] MH-2, dành nửa ngân sách inference làm vùng an toàn; trần đỏ làm tròn xuống để giữ GM ≥60% |
| D5 | ≥74,43199% | ≥60% đến <74,43199% | <60% | [MH] MH-1, xanh bám GM mô hình Hybrid, đỏ đúng mục tiêu kinh tế; rev-share thực phải đưa vào |
| D6 | ≥9.500.000đ | ≥6.072.403đ đến <9.500.000đ | <6.072.403đ | [MH] MH-3, xanh tại 400 job, sàn bảo vệ GM 60% với ngân sách 500 phiên thử |
| D7 | ≤10,8 tháng | >10,8 đến ≤12 tháng | >12 tháng hoặc lãi gộp ≤0 | [MH] MH-4, 10,8 = 90% mục tiêu 12 để giữ buffer thời gian 10%; đây là chính sách giả định, không phải BM |

Mẫu pilot thiếu không được tô xanh. D1/D2 phải hiển thị tử/mẫu; trước khi đủ tuổi chỉ báo đang hình thành cohort. D4 cảnh báo theo dự báo cả tháng cùng kỳ doanh thu, không chia chi phí lũy kế tuần cho doanh thu một tháng đầy đủ. D5/D6 xét partner riêng và cùng kỳ, không áp sàn tháng đầy cho partner mới chạy vài ngày.

### Phụ lục [MH] — đầu vào / phép tính / kết quả

**MH-1 — Giá Hybrid, Cost/Job và GM (D5)**

```text
Nguồn Excel: 1_Cost_Job!B9:B10, B15:B22, B41, B46, B50:B52, B68;
3_Value_Metric!B31:B32; 2_Pricing!B32.
Phiên thử = 500; booking confirmed = 500 × 80% = 400.
LLM/phiên = 2.800×1,25/1.000.000 + 4×2.800×0,10/1.000.000
          + 5×700×1/1.000.000 + 5×250×5/1.000.000 = 0,01437 USD.
Retry/phiên = 0,01437 × 7% = 0,0010059 USD.
Infra = 500 × 0,0836 = 41,8 USD/tháng.
QA = 500 × 5% × 9,2/60 × 9 = 34,5 USD/tháng.
COGS gốc = 500 × (0,01437 + 0,0010059) + 41,8 + 34,5 = 83,98795 USD.
Cost/Job gốc = 83,98795 / 400 × 25.400 = 5.333,234825đ.
Thêm DMS = 10 USD/tháng; Zalo OA = 41.667đ/tháng (critique log, giả định).
COGS điều chỉnh = (83,98795 + 10) × 25.400 + 41.667 = 2.428.960,93đ.
Cost/Job = 2.428.960,93 / 400 = 6.072,402325đ.
ARPU = 1.500.000 + 20.000 × 400 = 9.500.000đ/partner/tháng.
GM sau rev-share r=0 = 1 − 2.428.960,93 / 9.500.000 = 74,43199021%.
Xanh ≥74,43199%; vàng 60% đến <74,43199%; đỏ <60%.
GM thực = (R − share − COGS)/R; mọi khoản COGS mới phải cập nhật.
```

**MH-2 — Ngân sách inference từng partner (D4)**

```text
Inference = 500 × (0,01437 + 0,0010059) × 25.400 = 195.273,93đ/tháng.
COGS ngoài inference = 2.428.960,93 − 195.273,93 = 2.233.687đ/tháng.
COGS tối đa để GM≥60% = 9.500.000 × (1−60%) = 3.800.000đ.
Inference tối đa = 3.800.000 − 2.233.687 = 1.566.313đ.
Trần inference/R = 1.566.313 / 9.500.000 = 16,48750526%.
Đỏ >16,48% (làm tròn xuống); vàng >8,24% đến ≤16,48%; xanh ≤8,24%.
8,24% = một nửa trần đỏ; dành nửa còn lại cho spike và giá API đổi.
Khi có rev-share r, trần mới = (1−60%−r) − COGS ngoài AI/R.
Embedding/gọi lỗi thực đo phải cộng vào inference; đây chưa phải hóa đơn AI.
```

**MH-3 — Sàn doanh thu/partner (D6)**

```text
Giữ ngân sách 500 phiên thử/tháng và COGS 2.428.960,93đ.
R tối thiểu = 2.428.960,93 / (1−60%) = 6.072.402,325đ.
Làm tròn lên sàn 6.072.403đ; đỏ R < sàn này.
Booking cần = (6.072.402,325−1.500.000)/20.000 = 228,62011625 → 229 job.
Xanh R≥9.500.000 (400 job); vàng sàn đến <9.500.000.
Giới hạn: COGS hiện giữ theo 500 phiên thử; volume/QA tăng phải tính lại sàn.
Không ngoại suy Cost/Job 6.072đ như một biến phí cố định ở mọi volume.
```

**MH-4 — CAC và payback (D7)**

```text
Giả định mới: 12 giờ bán/partner; 9 USD/giờ (Excel B50); đi lại 40 USD.
CAC = (12×9 + 40)×25.400 = 3.759.200đ, không phải CAC đã đo.
Lãi gộp mô hình = 9.500.000−2.428.960,93 = 7.071.039,07đ/tháng.
Payback mô hình = 3.759.200/7.071.039,07 = 0,531633 tháng.
CAC tối đa ở GM mục tiêu 60%, payback12 = 9.500.000×60%×12 = 68.400.000đ.
Xanh payback≤10,8 (=12×90%); vàng >10,8 đến ≤12; đỏ >12 hoặc GP≤0.
Chỉ tăng ngân sách sau khi có GP thực và giờ bán đầy đủ; không lấy CAC trần làm mục tiêu chi.
Chi phí founder được tính kinh tế trong CAC; khi tính cash burn không cộng lại lần nữa.
```

**MH-5 — Runway và giới hạn pilot**

```text
OPEX toàn dự án = 400 USD×25.400 = 10.160.000đ/tháng (Excel B59/B68).
Giả định 2 pilot chưa trả phí: burn = 10.160.000 + 2×2.428.960,93
                                   = 15.017.921,86đ/tháng.
Giả định quỹ = burn×6 = 90.107.531,16đ → runway 6 tháng.
90 ngày ≈3 tháng, dùng khoảng45.053.766đ → còn khoảng3 tháng ở burn này.
Không gọi đây là vốn thật. Chi phí setup một lần 100 USD/partner từ khoảng50–100
trong critique log: 2×100×25.400 = 5.080.000đ; dự phòng ngoài quỹ vận hành.
Nếu lấy setup từ cùng quỹ, runway giảm còn khoảng5,66 tháng.
Monitoring khi >5 partner: thêm29 USD/tháng toàn hệ thống theo critique log,
phân bổ theo workload; cập nhật GM/sàn trước cổng90, không bỏ khỏi hóa đơn thực.
```

## Trạm 4 — 5 luật quyết định

An chịu trách nhiệm kích hoạt luật trong ngày phát hiện; đầu mối Cố vấn dịch vụ phối hợp phần vận hành. ⏹ là dừng một hoạt động; không dừng phục vụ lịch đã xác nhận. Vế KHÔNG THÌ là phản xạ bị cấm khi điều kiện xảy ra, không phải hành động cho trường hợp đèn xanh.

1. **⏹ R1:** **NẾU** D1 <30%, **TRONG** 2 lần họp tuần liên tiếp, **VÀ** mỗi lần có ≥2 partner đủ 30 ngày, **THÌ** An dừng tuyển partner mới 14 ngày và trực tiếp sửa onboarding ở partner cũ ngay ngày làm việc kế tiếp. **KHÔNG THÌ** không tăng mục tiêu ký xưởng để bù thiếu activation.
2. **R2:** **NẾU** D2 <5%, **TRÊN** 2 lần đo tuần liên tiếp sau ngày 60 của partner, **VÀ** cohort có ≥100 chủ xe đủ điều kiện, **THÌ** An cùng xưởng đổi đúng một điểm nhúng: đặt link P-100 trong nhắc hẹn được khách đồng ý nhận, triển khai trong 2 ngày. **KHÔNG THÌ** không làm thêm feature theo yêu cầu xưởng đó để thay cho phân phối.
3. **⏹ R3:** **NẾU** D3 >60 ngày, **TRÊN** một partner có ngày ký và tuổi chờ được đối soát, **THÌ** An dừng mở rộng pilot tại partner đó ngay ngày kế tiếp, thu hẹp về một ca/nhóm xe trong 14 ngày. **KHÔNG THÌ** không thêm tích hợp DMS hoặc chi phí quảng bá cho partner chưa đưa được user thật vào.
4. **⏹ R4:** **NẾU** D4 >16,48%, **TRONG** 2 tuần dự báo liên tiếp, **VÀ** có ≥100 phiên thật/partner/tuần và đối soát đầy đủ cost/revenue, **THÌ** An dừng campaign tạo thêm phiên, bật trần chi inference và chuyển workload ít cấp thiết sang model rẻ sau QA trong 1 ngày. **KHÔNG THÌ** không tăng volume hay bán gói không giới hạn để bù chi phí.
5. **⏹ R5:** **NẾU** D5 <60%, **TRONG** 2 tháng đầy đủ liên tiếp của cùng partner, **VÀ** hóa đơn/chiết khấu/share/COGS đã chốt, **THÌ** An dừng bán thêm tại partner đó và đàm phán lại giá hoặc share trong 7 ngày; không đạt sàn thì rút khỏi pilot sau khi xử lý lịch còn tồn. **KHÔNG THÌ** không lấy lợi nhuận partner khác để che partner này rồi mở rộng cùng điều khoản.

Kiểm tra phản biện: R1 không coi partner mới go-live là thất bại; R2 không chia cho tất cả khách chưa consent; R3 không bỏ các partner chưa có event khỏi mẫu; R4 không dùng trung bình toàn mạng; R5 không lấy tháng triển khai nửa kỳ. R4/R5 luôn nhường ưu tiên cho xử lý ca sai nguồn kỹ thuật theo PRD.

## Trạm 5 — Cổng gác và bằng chứng

Ngày0 = 10/10/2026. GO khi đúng metric qua ngưỡng và có file bằng chứng. Nếu biết rõ nguyên nhân có thể FIX **một lần** trong 30 ngày, ghi vấn đề/người làm trong nhật ký; nếu giả định sai thì PIVOT; hết lần FIX vẫn không qua thì KILL. Không dời hạn 08/01/2027.

| Cổng / ngày | Một metric | Ngưỡng GO / lý do | Bằng chứng phải có | Nếu trượt |
|---|---|---|---|---|
| 30 / 09/11/2026 | Số phỏng vấn chủ xe thật hoàn tất bài test “hiểu kế hoạch rồi chọn lịch” | ≥8; [TB] 4 O2O +4 cá nhân để học chỗ khó hiểu ở 2 scenario, không suy thành tỷ lệ thị trường | `evidence/day30-owner-study.md`, 8 mã ẩn danh, consent, quan sát lỗi và trích đoạn câu trả lời | FIX một lần: sửa một điểm khó hiểu, kiểm lại 09/12; không tuyển được chủ xe thật thì PIVOT cách tiếp cận |
| 60 / 09/12/2026 | Số partner đã activate | ≥2; [MH] 2 pilot là đơn vị của kịch bản burn, cần lặp giá trị ở hơn một xưởng | `evidence/day60-activation.csv`, partner_id, ngày ký/go-live, owner_id ẩn danh, event thật có timestamp | FIX onboarding/phân phối đến 08/01 nếu chưa dùng FIX cho vấn đề đó; đã FIX thất bại thì KILL |
| 90 / 08/01/2027 | GM sau share thấp nhất trong 2 partner đã activate | ≥60% với tháng đối soát đầy đủ; [MH] GM mục tiêu, không lấy trung bình che lỗ | `evidence/day90-unit-economics.csv`, doanh thu, refund/share, invoice inference, infra, QA/support và monitoring phân bổ | PIVOT giá/đối tác nếu mới xác định giả định sai; đã FIX kinh tế một lần vẫn <60% thì KILL |

**KILL CRITERIA:** Đến 08/01/2027, dừng hướng pilot B2B2C này nếu sau một lần FIX cho vấn đề tương ứng vẫn có <2 partner activate hoặc GM thấp nhất của 2 partner <60%; nếu không có dữ liệu đối soát để tính cổng90 thì không GO và dừng cấp ngân sách mở rộng cho đến khi đổi phương án có thể kiểm chứng.

Các tên file evidence là đầu ra phải thu trong pilot, **không** khẳng định file đang tồn tại. Không tạo log giả để làm bằng chứng. Nếu thiếu mẫu ở ngày cổng, cổng chưa qua; thiếu dữ liệu là lỗi thiết kế pilot cần FIX/PIVOT theo quy tắc, không được coi là xanh.

**Chưa đo được:** chỉ gói trong 3 nhóm: (1) funnel/event partner và chủ xe thật, baseline tuần 24/10 và cohort30/60 ngày 09/12; (2) doanh thu/share, invoice AI, QA/support, giờ bán/CAC, đối soát đầu09/11 và đủ 2 tháng 09/12; (3) NRR cần hợp đồng gia hạn, không dùng làm đèn trong 90 ngày. An sở hữu sổ đo; đầu mối xưởng cấp dữ liệu có consent. Không có giá trị thiếu nào được thay bằng0.

### Nguồn lưu vết

- PRD: `Project/P-100/docs/ba/02-prd.md`, cập nhật04/10, đọc 10/10/2026; đặc biệt §1, §2, FR-06, BR-01, §6 và C-02.
- Day22: `Track1_Day22_2A202602776_NguyenVanAn/NguyenVanAn_Day22_model.xlsx`; SHA256 `01a77513aea22b2e00c9488ad6eec16e0b197657224778f4fb7b473a450549db`. Đọc công thức và tự tính, không dựa vào cache Excel. Không sửa workbook nguồn.
- Critique log ngày 08/10: DMS10 USD/tháng, OA 41.667đ/tháng, setup50–100 USD, monitoring29 USD/tháng. Đây là giả định nguồn của bài trước, không phải báo giá kiểm tra hôm nay.
- HANDBOOK §§2/3.3 kiểm tra 10/10: https://github.com/VinUni-AI20k/K4-L3-Day23-AI-Product-Growth/blob/main/HANDBOOK.md
- AI hỗ trợ dự thảo và phản biện; tác giả cần đọc, chốt ngưỡng/luật/cổng bằng lời mình. Không tự chấm điểm hoặc khẳng định pilot được nghiệm thu.
