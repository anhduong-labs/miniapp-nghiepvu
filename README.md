# Lark Procurement Mini App — Sơ Đồ & Luồng Nghiệp Vụ Cốt Lõi

Kho lưu trữ tài liệu trực quan hóa kiến trúc và sơ đồ luồng nghiệp vụ tương tác bằng công nghệ **Archify** cho hệ thống **Lark Procurement Mini App** (Ứng dụng Mini Mua sắm Nội bộ trên nền tảng Lark Suite). 

Hệ thống được thiết kế để chuẩn hóa, giám sát và tối ưu hóa toàn bộ hoạt động mua sắm & luân chuyển hàng hóa giữa **8 tòa nhà cơ sở** và **Head Office (Kho Tổng)**.

---

## 📑 Danh Mục Bản Vẽ & File Trực Quan

| File | Tên Nghiệp Vụ / Bản Vẽ | Mô Tả Tóm Tắt |
| :--- | :--- | :--- |
| **`index.html`** / **`quy-trinh-mua-sam.html`** | 🏢 **Trung Tâm Điều Phối 3 Quy Trình Cốt Lõi** | Trang điều khiển tích hợp cả 3 quy trình chính dạng Tab chọn, hỗ trợ chế độ xem Fullscreen (Toàn màn hình), đổi giao diện Sáng/Tối. |
| **`workflows/technical.html`** | 🔧 **Nghiệp Vụ 1: Mua Sắm Vật Tư Kỹ Thuật & Dịch Vụ** | Quy trình phân rã kỹ thuật, cân đối Kho Tổng vs Mua Mới NCC (**Bước 03: Miễn duyệt BOD nếu 100% xuất kho**), giao nhận kép và nghiệm thu 2 tầng. |
| **`workflows/stationery.html`** | 📦 **Nghiệp Vụ 2: Mua Sắm Văn Phòng Phẩm (VPP)** | Quy trình gom lô định kỳ hàng tháng ngày 25, bỏ qua BM rà soát hiện trường, nhập Kho Tổng Head Office rồi phân bổ 2 chặng về 8 tòa. |
| **`workflows/consumables.html`** | 🧹 **Nghiệp Vụ 3: Mua Sắm Vật Tư Tiêu Hao (VTTH)** | Quy trình kiểm soát ma trận định mức chuẩn (18 danh mục x 8 tòa nhà), cảnh báo lệch định mức 2 tháng liên tiếp và kích hoạt Khóa sổ cứng (Hard-Lock). |
| **`enterprise-architecture.html`** | 🏛️ **Kiến Trúc Nghiệp Vụ Tổng Thể & Mối Liên Kết** | Bản đồ tương tác giữa các vai trò (Requester, Building Manager, P. Mua hàng, Kế toán, BOD, Thủ kho) và hệ sinh thái Lark Base/Lark Bot. |
| **`workflows/procurement-flow.html`** | 🔄 **Sơ Đồ Luồng Xử Lý Mua Sắm Đầy Đủ** | Bản vẽ chi tiết các điểm rẽ nhánh và cơ chế kiểm soát chất lượng từ khâu tạo đề xuất đến thanh toán. |

---

## 🔍 Chi Tiết 3 Quy Trình Nghiệp Vụ Cốt Lõi

### 1. Vật Tư Kỹ Thuật & Dịch Vụ Bảo Dưỡng (`workflows/technical.html`)
- **Khởi tạo & Rà soát:** Kỹ thuật viên tòa nhà lập phiếu đề xuất kèm hình ảnh hiện trường, mã tài sản và mức độ khẩn cấp. Quản lý tòa nhà (BM) kiểm tra thực địa trong vòng 24h.
- **Bước 03 cốt lõi — Lựa Chọn Nguồn Cung Ứng (Kho vs Mua Mới):**
  - **Trường hợp 1 (Tồn kho đủ 100%):** Tự động phát hành Lệnh cấp phát Kho. Đơn hàng được **MIỄN DUYỆT BAN GIÁM ĐỐC (BOD)** và bỏ qua bước lấy 3 báo giá cạnh tranh. Thủ kho xuất hàng ngay trong 24h.
  - **Trường hợp 2 (Cần mua mới NCC một phần hoặc toàn bộ):** Bộ phận mua sắm lấy tối thiểu 3 báo giá cạnh tranh, lập bảng so sánh và trình Giám đốc (BOD) ký duyệt số qua Lark Approval.
- **Bàn giao & Giao nhận Kép (Dual-Stream):** Hỗ trợ phiếu đơn có 2 dòng cung ứng song song: Hàng xuất từ Kho Tổng + Hàng giao từ Nhà cung cấp ngoài.
- **Nghiệm thu 2 tầng:** Biên bản nghiệm thu kỹ thuật tại tòa nhà kết hợp hồ sơ chứng từ tài chính (Hóa đơn VAT, Phiếu xuất kho, Hợp đồng).

### 2. Định Kỳ Văn Phòng Phẩm (VPP) (`workflows/stationery.html`)
- **Tối giản quy trình:** Tự động **BỎ QUA** bước Quản lý tòa nhà rà soát hiện trường (do VPP mang tính chất hành chính định kỳ).
- **Gom lô định kỳ ngày 25:** Hệ thống tự động khóa đề xuất vào 17:00 ngày 25 hàng tháng, tổng hợp nhu cầu toàn bộ 8 tòa nhà thành 1 đơn hàng tập trung (Consolidated Batch).
- **Đàm phán số lượng lớn:** Phòng Cung Ứng làm việc với NCC khung theo đơn giá chiết khấu số lượng lớn, giảm chi phí từ 15-25%.
- **Mô hình luân chuyển 2 chặng:**
  - *Chặng 1:* NCC bàn giao toàn bộ đơn hàng về Kho Tổng Head Office kiểm đếm.
  - *Chặng 2:* Đội ngũ vận hành nội bộ chia gói theo từng cơ sở và vận chuyển phân bổ về 8 tòa nhà.

### 3. Định Kỳ Vật Tư Tiêu Hao (VTTH) (`workflows/consumables.html`)
- **Ma trận định mức chuẩn:** Kiểm soát chặt chẽ 18 nhóm mặt hàng tiêu hao chủ lực (hóa chất vệ sinh, giấy vệ sinh, túi rác...) cho 8 tòa nhà dựa trên diện tích sàn và lưu lượng khách.
- **Phát hiện bất thường 2 tháng liên tiếp:** Nếu một cơ sở đề xuất vượt ngưỡng định mức liên tục 2 tháng, hệ thống tự động gắn cờ **CẢNH BÁO ĐỎ** và yêu cầu BM giải trình nguyên nhân (rò rỉ, sự kiện đột xuất, thất thoát).
- **Cơ chế Khóa sổ cứng (Hard-Lock):** Sau ngày 25 hàng tháng, cổng nộp đề xuất VTTH tự động khóa cứng; mọi đề xuất phát sinh sau mốc này phải chuyển sang quy trình mua bổ sung đột xuất có phê duyệt đặc biệt.

---

## 🚀 Hướng Dẫn Mở & Xem Bản Vẽ

### Cách 1: Xem trực tiếp trên máy cục bộ (Offline)
1. Tải repository về máy hoặc clone qua Git:
   ```bash
   git clone https://github.com/anhduong-labs/miniapp-nghiepvu.git
   cd miniapp-nghiepvu
   ```
2. Mở file `index.html` bằng trình duyệt bất kỳ (Google Chrome, Safari, Microsoft Edge, Firefox):
   - **macOS:** Chạy lệnh `open index.html` trong Terminal hoặc nhấp đúp vào file.
   - **Windows:** Chạy lệnh `start index.html` hoặc nhấp đúp chuột.

### Cách 2: Bật GitHub Pages để xem Online
1. Truy cập vào kho GitHub: `https://github.com/anhduong-labs/miniapp-nghiepvu`.
2. Vào tab **Settings** -> mục **Pages** (ở cột bên trái).
3. Tại phần **Build and deployment** -> **Source**: Chọn `Deploy from a branch`.
4. Chọn nhánh `main` và thư mục `/(root)` -> Nhấn **Save**.
5. Sau 1-2 phút, trang web sẽ được kích hoạt tại địa chỉ:
   ```
   https://anhduong-labs.github.io/miniapp-nghiepvu/
   ```

---

## ⌨️ Phím Tắt Tiện Ích Khi Xem Sơ Đồ Archify

- **`0`**: Đặt lại góc nhìn mặc định (Reset zoom/fit).
- **`+` / `-`**: Phóng to / Thu nhỏ sơ đồ.
- **Kéo chuột trái**: Di chuyển (Pan) tự do trên canvas.
- **`S`**: Chuyển đổi giao diện màu sắc / Presets (Signal Flow, Editorial, Technical).
- **`T`**: Đổi chế độ Sáng / Tối (Dark mode / Light mode).
- **`/`**: Tìm kiếm nhanh tên bước hoặc thực thể nghiệp vụ trên sơ đồ.

---
*Bản quyền tài liệu thuộc về Bộ phận Vận Hành & Phát Triển Ứng Dụng Lark Miniapp.*
