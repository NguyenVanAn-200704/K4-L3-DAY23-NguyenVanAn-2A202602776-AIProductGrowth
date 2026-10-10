# OPERATING DASHBOARD — P-100

**Nguyễn Văn An · 2A202602776 · B2B2C · 09/10/2026.** Xưởng dự kiến trả phí; chủ xe dùng Owner P-100, Cố vấn dịch vụ dùng Advisor. **North Star: D1 activation ≥60%.** Số hiện tại “—” là chưa có dữ liệu pilot, không phải 0; màu chỉ bật khi đủ kỳ/mẫu. Tài chính là giả định Day22 đã tính lại, không phải kết quả vận hành.

### Leading — hằng tuần

| Đèn / hiện tại | 🟢 | 🟡 | 🔴 | Nguồn và lý do / báo trước |
|---|---|---|---|---|
| D1 Activation / — | ≥60% | 30–<60% | <30% | [TB] Ưu tiên xưởng có chủ xe thật; 2 cohort30 ngày, baseline 08/12 → D6; R1 |
| D2 Reach mỗi xưởng / — | ≥15% | 5–<15% | <5% sau 60 ngày | [TB] Đo phân phối trước thêm feature; 2 tuần, baseline 23/10 → D6; R2 |
| D3 First end-user / — | <30 ngày | 30–60 ngày | >60 ngày | [TB] Không để pilot mất 2/3 kỳ chỉ để cài đặt; baseline 08/12 → D1/D6; R3 |

### Operating — kiểm tuần, chốt tháng

| Đèn / hiện tại | 🟢 | 🟡 | 🔴 | Nguồn và lý do / báo trước |
|---|---|---|---|---|
| D4 Inference/R mỗi xưởng / — | ≤8,24% | >8,24–≤16,48% | >16,48% | [MH] COGS khác 2,234 tr; trần AI 1,566 tr/R9,5 tr để GM≥60% → D5/D7; R4 |
| D5 GM sau share / — | ≥74,43199% | 60–<74,43199% | <60% | [MH] Xanh theo Hybrid đã bổ sung COGS; đỏ sàn kinh tế 60% → D7; R5 |

### Lagging — tháng / kiểm quý

| Đèn / hiện tại | 🟢 | 🟡 | 🔴 | Nguồn và lý do |
|---|---|---|---|---|
| D6 ARPU/xưởng/tháng / — | ≥9,5 tr | ≥6.072.403đ–<9,5 tr | <6.072.403đ | [MH] 400 job×20 k+1,5 tr; sànCOGS/40% (229 job); đỏ: dừng mở rộng tại xưởng |
| D7 CAC payback ước tính / — | ≤10,8 tháng | >10,8–≤12 tháng | >12 tháng; GP≤0 | [MH] Mục tiêu12, giữ 10% buffer; đỏ: đóng băng tăng chi acquisition |

### 5 luật quyết định (⏹ = dừng; An kích hoạt)

1. **⏹ R1:** **NẾU** D1<30%, **TRONG** 2 tuần liên tiếp, **VÀ** ≥2 xưởng đủ 30 ngày, **THÌ** dừng tuyển partner14 ngày, An sửa onboarding ngày kế tiếp. **KHÔNG THÌ** không tăng số ký để bù activation.
2. **R2:** **NẾU** D2<5%, **TRÊN** 2 lần đo tuần sau ngày 60, **VÀ** ≥100 chủ xe/cohort, **THÌ** An+xưởng đổi một điểm nhúng trong 2 ngày. **KHÔNG THÌ** không thêm feature để thay phân phối.
3. **⏹ R3:** **NẾU** D3>60 ngày, **TRÊN** 1 partner đã đối soát ngày ký, **THÌ** An dừng mở rộng tại xưởng ngày kế tiếp, thu pilot về 1 ca/nhóm xe trong 14 ngày. **KHÔNG THÌ** không thêm tích hợp/quảng bá.
4. **⏹ R4:** **NẾU** D4>16,48%, **TRONG** 2 tuần dự báo, **VÀ** ≥100 phiên thật/tuần, cost/R đủ, **THÌ** An dừng campaign, bật trần inference, đổi model sau QA trong 1 ngày. **KHÔNG THÌ** không tăng volume/bán unlimited.
5. **⏹ R5:** **NẾU** D5<60%, **TRONG** 2 tháng đầy đủ cùng xưởng, **VÀ** đối soát COGS/share xong, **THÌ** An dừng bán thêm, đàm phán giá/share trong 7 ngày hoặc rút pilot. **KHÔNG THÌ** không che lỗ bằng xưởng khác.

### Cổng gác 90 ngày — GO chỉ khi có bằng chứng

| Ngày | Một metric / ngưỡng GO | Bằng chứng phải tồn tại | Nếu trượt |
|---|---|---|---|
| 30 · 08/11/2026 | Phỏng vấn/test hiểu kế hoạch ≥8 chủ xe (4 O2O+4 cá nhân) | evidence/day30-owner-study.md: consent, mã ẩn danh, quan sát | FIX 1 lần một điểm khó hiểu; không tiếp cận được user thì PIVOT |
| 60 · 08/12/2026 | Partner activate ≥2 | evidence/day60-activation.csv: partner, ngày, event user thật | FIX 1 lần onboarding đến 07/01; đã FIX vẫn trượt → KILL |
| 90 · 07/01/2027 | GM sau share thấp nhất của 2 partner ≥60% | evidence/day90-unit-economics.csv + invoice, share, QA/support | PIVOT giả định giá sai; đã FIX kinh tế vẫn trượt → KILL |

**KILL:** Ngày07/01/2027, sau 1 lần FIX vẫn <2 partner activate hoặc GM thấp nhất<60% thì dừng hướng pilot này. FIX chỉ1 lần/vấn đề, không dời hạn KILL. Thiếu chứng cứ không GO. Nguồn kỹ thuật sai: chặn ca, chuyển người theo PRD ngay.

**CHƯA ĐO ĐƯỢC:** funnel user thật (baseline 23/10; cohort08/12); cost/R/share/CAC thực (đối soát08/11 và08/12); NRR chờ cohort gia hạn, không dùng trong 90 ngày. An+xưởng thu log có consent và invoice.

**Giả định:** Hybrid 1,5 tr+20 k/job; 400 job/500 phiên; Cost/Job6.072đ; rev-share0%; CAC3,759 tr; runway 6 tháng. [TB] là giả thuyết chờ 2 chu kỳ, không phải BM. Nguồn: PRD 04/10, Excel/critique Day22 đọc 09/10; chi tiết và định nghĩa trong worksheet; phép tính ở trang2.
