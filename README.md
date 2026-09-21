# Hướng dẫn liên kết Google Sheet với Music Box

## Bước 1: Tạo Google Sheet

1. Vào https://sheets.google.com → **Blank spreadsheet**
2. Đặt tên sheet (ví dụ: `MusicBox Data`)
3. Tạo 3 sheet (tab phía dưới):
   - `Rooms`
   - `Bookings`
   - `Invoices`  
   (Script sẽ tự tạo header nếu chưa có)

## Bước 2: Cài Apps Script

1. Trong Google Sheet: **Extensions → Apps Script**
2. Xóa hết code mặc định
3. Mở file `GoogleAppsScript.js` (trong thư mục dự án) → **Copy toàn bộ** → Dán vào Apps Script
4. Bấm **Save** (Ctrl+S), đặt tên project tùy ý

## Bước 3: Deploy Web App

1. Trong Apps Script: **Deploy → New deployment**
2. Bấm biểu tượng bánh răng → chọn **Web app**
3. Cấu hình:
   - **Description**: Music Box API
   - **Execute as**: Me
   - **Who has access**: **Anyone**
4. Bấm **Deploy**
5. Lần đầu sẽ hỏi quyền → **Authorize access** → chọn tài khoản Google → Advanced → Go to ... → Allow
6. **Copy URL** (dạng):
   ```
   https://script.google.com/macros/s/AKfycbxxxxxxx/exec
   ```

## Bước 4: Dán URL vào config.json

Mở file `config.json`, sửa dòng:

```json
"sheetApiUrl": "https://script.google.com/macros/s/AKfycbxxxxxxx/exec"
```

Lưu file → **tải lại trang web**.

Khi thấy dòng trạng thái có **Google Sheet: ON** là đã kết nối.

## Bước 5: Kiểm tra

- Vào **Cài đặt** → bấm **Đồng bộ lên Sheet** hoặc **Tải từ Sheet**
- Hoặc thao tác bình thường (quẹt thẻ, đặt phòng, thanh toán) → dữ liệu tự gửi lên Sheet

## Dữ liệu được lưu

| Sheet | Nội dung |
|-------|----------|
| **Rooms** | Trạng thái 6 phòng, mã thẻ, giờ vào, món đã gọi |
| **Bookings** | Lịch đặt phòng |
| **Invoices** | Mỗi lần thanh toán: thời gian, tiền phòng (ban ngày/đêm), món, tổng tiền |

## Lưu ý quan trọng

- App vẫn lưu **localStorage** trước. Google Sheet là bản sao / backup / báo cáo.
- Nếu nhiều máy dùng chung 1 Sheet: nên bấm **Tải từ Sheet** khi mở app để lấy trạng thái mới nhất.
- URL Web App phải để **Anyone**, nếu không trình duyệt không gọi được.
- Khi sửa code Apps Script → Deploy lại (Manage deployments → Edit → New version).

## Gỡ lỗi

- Mở F12 → tab Console xem log lỗi.
- Thử mở URL `...?action=ping` trên trình duyệt, phải thấy `{"ok":true,...}`.
- Nếu CORS lỗi: Script đã dùng `mode: 'no-cors'` cho POST (không đọc được response nhưng dữ liệu vẫn được ghi).

