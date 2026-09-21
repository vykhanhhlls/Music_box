# Music Box - Hệ thống Quản lý Phòng

Web app quản lý phòng Music Box.

## File quan trọng

| File | Mục đích |
|------|----------|
| `index.html` | Giao diện chính |
| `config.json` | **Cấu hình chính** – giá giờ, mã thẻ từng phòng, danh sách món |

## Cách sửa cấu hình (config.json)

Mở file `config.json` bằng Notepad / VS Code:

```json
{
  "ratePerHour": 100000,          // Giá mỗi giờ (VND) – ĐỔI TẠI ĐÂY
  "minMinutes": 60,               // Làm tròn tối thiểu (phút)
  "cards": {                      // Mã thẻ cố định từng BOX
    "1": "11111",
    "2": "22222",
    "3": "33333",
    "4": "44444",
    "5": "55555",
    "6": "66666"
  },
  "menu": [                       // Thêm / bớt / sửa món tại đây
    { "id": "cam", "name": "Nước cam ép", "price": 25000 },
    { "id": "dau", "name": "Sữa đậu", "price": 10000 },
    { "id": "ngo", "name": "Sữa ngô", "price": 20000 },
    { "id": "chanh", "name": "Trà chanh", "price": 10000 },
    { "id": "quat", "name": "Trà quất", "price": 10000 },
    { "id": "dao", "name": "Trà đào", "price": 15000 }
  ]
}
```

### Thêm món mới
```json
{ "id": "coca", "name": "Coca Cola", "price": 15000 }
```
Thêm vào mảng `menu`, lưu file, **tải lại trang**.

### Đổi mã thẻ
Sửa số trong `"cards"`, ví dụ BOX 1 dùng thẻ `99999`:
```json
"1": "99999"
```

### Đổi giá giờ mặc định
Sửa `"ratePerHour": 80000` (ví dụ 80.000đ/giờ).

---

## Cách hoạt động quẹt thẻ

- Mỗi BOX có **1 mã thẻ cố định** (định nghĩa trong `config.json`).
- Quẹt thẻ `11111` → vào/ra **BOX 1**.
- Quẹt thẻ `22222` → vào/ra **BOX 2**.
- ...
- Phòng trống → quẹt thẻ → chuyển **đỏ** + hiện mã thẻ trên ô.
- Phòng đang đỏ → quẹt lại cùng thẻ → mở màn hình **Thanh toán**.

## Deploy GitHub Pages

1. Tạo repo mới trên GitHub.
2. Upload cả 2 file: `index.html` + `config.json`.
3. Settings → Pages → Source: branch `main`.
4. Truy cập `https://username.github.io/tên-repo/`.

## Liên kết Google Sheet

Có thể dùng Google Apps Script làm backend. Nếu cần code sẵn, hãy yêu cầu.

---

Phát triển bởi Grok • 2026
