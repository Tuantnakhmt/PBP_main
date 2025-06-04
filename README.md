# 📊 Phân tích Dữ liệu và Đặc trưng cho Dự đoán Mua Gói

## 🎯 Mục tiêu dự án
Dự án tập trung phân tích hành vi của thuê bao nhằm dự đoán khả năng **mua gói cước viễn thông**, từ đó hỗ trợ đề xuất chiến lược chăm sóc và tối ưu hóa doanh thu.
📂 Dữ liệu: Thông tin hành vi tiêu dùng, gọi, nhắn tin, data, dịch vụ đăng ký của thuê bao qua nhiều tháng.  
📅 Mốc phân tích: Tháng 9/2024 với dữ liệu lịch sử từ T6 đến T9.

## 🧹 Tiền xử lý dữ liệu
- **Loại bỏ cột không cần thiết**: `idnumber`, `ngay_sinh`, `co_goi`, `PTC`, v.v.
- **Chuẩn hóa dữ liệu giới tính** và bổ sung `notKnown`, `notIncluded` cho các trường thiếu.
- **Chuyển đổi đơn vị**:
  - Tài chính → nghìn đồng (`TKC`, `NAP_THE`, `TKC_DATA`, ...)
  - Data → GB (`LL_DATA_*`)
- **Tạo đặc trưng mới** từ ngày tháng:
  - `interval_activate`, `interval_topay`, `interval_tolock`, `interval_tocancel`

## 📈 Phân tích dữ liệu
- **Phân phối lệch trái** và nhiều giá trị ngoại lai ở các trường tài chính và lưu lượng.
- Nhóm mua gói có:
  - Số ngày kích hoạt gần hơn.
  - Lưu lượng Data tháng 7–8 cao hơn.
  - Số dư tài khoản sau sử dụng cao hơn.
  - Tỷ lệ chi tiêu trên mỗi GB cao hơn.
- **Tình trạng hoạt động** liên tục 3 tháng là yếu tố quan trọng cho hành vi mua gói.
- **Đặc trưng TKC_DATA và số gói đã mua** có mối tương quan thuận mạnh mẽ.

## 🔄 Tương quan đáng chú ý
- `LL_SMS_ONNET` ↔ `TKC_SMS`,  
- `LL_OFFNET_OG` ↔ `TKC_THOAI_OFFNET`,  
- Số gói mua ↔ Tiền dùng trong `TKC_DATA`,  
- Chu kỳ gói ↔ Giá trị lợi nhuận.

## ✅ Tổng kết đặc trưng hữu ích
- `interval_activate`
- `TKC_DATA` (và độ giảm từ tháng trước)
- `LL_DATA_T7`, `LL_DATA_T8`
- `sum_voice`, `voice_di_nm`
- `hoạt động_tháng_9`, `khong_hd_thang_9`
- `so_goi_mua`, `chu_ky_goi`
