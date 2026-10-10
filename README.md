# K4-L3-DAY23-NguyenVanAn-2A202602776-AIProductGrowth

**Họ tên:** Nguyễn Văn An · **MSSV:** 2A202602776 · **Ngày làm:** 10/10/2026 (GMT+7)

**Sản phẩm:** P-100 — AI Agent Chăm sóc sau bán & Lập kế hoạch bảo dưỡng xe điện.

**Câu chốt loại:** P-100 chọn B2B2C: đại lý/xưởng là bên dự kiến trả phí, chủ xe là người nhận kế hoạch và đặt lịch trực tiếp qua ứng dụng Owner mang tên sản phẩm, còn Cố vấn dịch vụ xác nhận lịch qua cổng xưởng.

Phân loại do tác giả chọn cho bài lab; PRD xác nhận hai bề mặt Owner/Advisor, chưa chứng minh có hợp đồng trả phí hay pilot thương mại. VinFast Aftersales là kênh tiếp cận tiềm năng, không được tính là partner đã ký. Một partner trong dashboard là một đại lý/xưởng có thỏa thuận pilot riêng.

## Bài nộp

- [dashboard.pdf](dashboard.pdf): trang 1 Operating Dashboard; trang 2 phụ lục phép tính [MH].
- [dashboard.md](dashboard.md): nội dung dashboard theo đúng 3 tầng.
- [worksheet.md](worksheet.md): số đầu vào, 9 nhóm đèn B2B2C, 7 thẻ đèn, ngưỡng, phép tính và 5 luật.

## Cách dùng số liệu

Theo yêu cầu của tác giả, dùng Day22 làm giả định tài chính và tự bổ sung kịch bản CAC/runway để hoàn thành lab. Mọi số mô hình là **kế hoạch**, không phải doanh thu, chi phí hay tiền mặt đã đo. Ngưỡng [TB] là ngưỡng thử nghiệm có lịch lấy baseline; không có benchmark [BM] được dùng trong dashboard.

Chốt mức Hybrid **1.500.000đ/tháng/đại lý + 20.000đ/booking xác nhận**, theo quyết định tại `3_Value_Metric!B31:B32`. Mức 35.000đ/job tại `2_Pricing!B19` là phương án khác, không trộn vào phép tính. Cost/Job được tính lại và bổ sung khoản DMS/Zalo OA mà critique log đã đề nghị nhưng Excel chưa đưa vào. Các khoản này là dự phòng tài chính cho pilot, không khẳng định P-100 đã tích hợp DMS/Zalo thật.

Giữ đúng PRD: Rule Engine quyết định hạng mục; DB tính giá; RAG giải thích có nguồn; chủ xe đồng ý gửi yêu cầu và Cố vấn dịch vụ xác nhận. Xác nhận chuẩn không phải escalation. Chi phí bảo dưỡng khách trả cho xưởng không phải ARPU của phần mềm.

## Nguồn và quyết định của tác giả

1. PRD P-100: `Project/P-100/docs/ba/02-prd.md`, bản cập nhật 04/10/2026; đọc ngày 10/10/2026, §§1–2, FR-04/05/06/24, BR-01/02/03, §6. Đây là yêu cầu thiết kế, chưa phải kiểm chứng runtime.
2. `TongHop_LAB/Track1_Day22_2A202602776_NguyenVanAn/NguyenVanAn_Day22_model.xlsx`, đọc ngày 10/10/2026; ô nguồn và phép tính nằm trong worksheet.
3. Critique log cùng thư mục Day22, ngày 08/10/2026: đề nghị bổ sung DMS, Zalo OA và monitoring.
4. [HANDBOOK Day23](https://github.com/VinUni-AI20k/K4-L3-Day23-AI-Product-Growth/blob/main/HANDBOOK.md), §§2 và 3.3; [Rubric](https://github.com/VinUni-AI20k/K4-L3-Day23-AI-Product-Growth/blob/main/RUBRIC.md). Đối chiếu ngày 10/10/2026. Các mốc [TB] trong sổ tay được dùng như giả thuyết ban đầu, không gắn nhãn benchmark.

AI hỗ trợ trích dữ liệu, kiểm tra phép tính và soạn bản làm việc. Tác giả đã chọn P-100, B2B2C, dùng Day22 làm giả định và bổ sung kịch bản tài chính. Ngưỡng, luật và cổng trong bản này là đề xuất để tác giả đọc và viết lại theo lời mình trước khi nộp, đúng quy định dùng AI của đề bài.

Số tiền là giả định bài tập, không phải số liệu mật của doanh nghiệp; không áp dụng scale. Mốc bắt đầu kế hoạch là 10/10/2026, các cổng cố định 09/11/2026, 09/12/2026 và 08/01/2027; FIX không tự dời hạn KILL.
