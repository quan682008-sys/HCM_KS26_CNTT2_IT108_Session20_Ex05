# HCM_KS26_CNTT2_IT108_Session20_Ex05
# Bài 5: Xây dựng cơ chế xác thực an toàn cho Crypto Wallet

## 1. Thiết kế kiến trúc

Sơ đồ 3 lớp bảo vệ:

```text
Lớp 1: Mật khẩu (Something you know)
         |
   Nhập mật khẩu
         |
   Hacker có mật khẩu
   → Vượt qua lớp 1
         |
         v
Lớp 2: OTP (Something you have)
         |
   Nhập mã từ Google Authenticator
         |
   Hacker không có thiết bị
   → Nhập sai mã → Bị chặn
         |
         v
Lớp 3: Sinh trắc học (Something you are)
         |
   Face ID / Vân tay
         |
   Không xác thực được
   → Bị chặn giao dịch
```

Giải thích: Dù hacker biết mật khẩu, họ vẫn cần mã OTP từ thiết bị và xác thực sinh trắc học mới có thể hoàn tất giao dịch. Ba lớp bảo vệ giúp giảm nguy cơ bị chiếm đoạt ví.

## 2. Xử lý Edge Case

Nếu người dùng đang trên máy bay, không có Internet hoặc sóng điện thoại thì lấy OTP bằng cách nào?

- Sử dụng ứng dụng Google Authenticator với thuật toán TOTP.
- TOTP không cần Internet hoặc SIM để tạo mã.
- Mã được tạo dựa trên khóa bí mật đã thiết lập và thời gian hiện tại, thường thay đổi sau mỗi 30 giây.
- Khi bật chế độ máy bay, ứng dụng vẫn tạo mã OTP bình thường.

Lưu ý: Thiết bị cần có thời gian chính xác để mã khớp với máy chủ. Người dùng vẫn cần kết nối mạng khi gửi yêu cầu giao dịch đến máy chủ.
