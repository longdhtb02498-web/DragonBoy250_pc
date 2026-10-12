# DragonBoy250 PC - Kênh Phân Phối Cập Nhật Tự Động (Auto-Update Distribution)

Kho lưu trữ chuyên dụng lưu trữ gói phân phối cập nhật tự động (Auto-Update Hot-Swap) cho Sendo QLTK Panel (.NET 8 WinForms) và DragonBoy250 PC Client (Unity Mono).

Kho lưu trữ này được thiết lập ở chế độ **Private (100% riêng tư)**, đồng bộ trực tiếp với `DefaultUpdateUrl` trong `Panel.exe`.

---

## 1. Cấu Trúc Phát Hành (Release Artifacts)

```
├── README.md
└── dist/
    ├── version.json    # Manifest định tuyến phiên bản & kiểm tra toàn vẹn SHA256
    └── patch.zip       # Gói nén nhị phân Hot-Swap (Panel.exe + Assembly-CSharp.dll)
```

- **`dist/version.json`**:
  * Chứa số hiệu phiên bản mới nhất (`version`), URL tải về (`download_url`), mã băm mật mã SHA256 (`sha256`) và nhật ký thay đổi (`changelog`).
- **`dist/patch.zip`**:
  * Chứa bản cập nhật nhị phân đã biên dịch và làm rối (Obfuscated) hoàn chỉnh:
    - `Panel.exe` (Single-File bundle độc lập, .NET 8 WinForms)
    - `DragonBoy250_Data\Managed\Assembly-CSharp.dll` (Obfuscated client assembly)

---

## 2. Thông Tin Phiên Bản Hiện Tại (v2.5.1)

- **Phiên bản (SemVer)**: `2.5.1`
- **Mã băm SHA256**: `98EE657721540F40654D4093A1DD734E1C79A463692961D26FE0C52676E4E440`
- **Nhật ký thay đổi (Changelog)**:
  * Tự động kiểm tra và cập nhật phiên bản Hot-Swap.
  * Tương thích nền tảng bảo mật đa tầng Single-File & Obfuscar.
  * Bảo toàn 100% tài khoản và cấu hình trong thư mục `Data`.

---

## 3. Quy Trình Cập Nhật Khép Kín (Update Flow)

1. `Panel.exe` khởi chạy, gửi yêu cầu GET tới `DefaultUpdateUrl`:
   `https://raw.githubusercontent.com/longdhtb02498-web/DragonBoy250_pc/main/dist/version.json`
2. Hệ thống so sánh SemVer (`2.5.1` vs phiên bản hiện tại).
3. Nếu có bản cập nhật mới:
   - Tải `dist/patch.zip` về thư mục tạm `Data/temp_update/`.
   - Xác thực mã băm SHA256 theo thuật toán Wycheproof Constant-Time so khớp.
   - Giải nén bản vá và thực hiện Hot-Swap thay thế tệp an toàn (Transactional Rollback nếu lỗi).
   - Bảo toàn nguyên vẹn thư mục `Data/` (tài khoản, proxy, cấu hình máy chủ).

---

## 4. Bảo Mật & Riêng Tư (Security & Privacy)

- **Trạng thái**: GitHub Private Repository.
- **Không chứa mã nguồn**: Repo này chỉ đóng vai trò phân phối gói cập nhật nhị phân đã kiểm duyệt.
- **Không chứa bí mật**: 0% tài khoản người dùng, API key hay thông tin nhạy cảm.
