# LAB 3 - MÃ HÓA KHÓA CÔNG KHAI

- **MSSV:** 1150080104
- **Lớp:** 11-ĐH-THMT
- **Học phần:** An toàn và Bảo mật thông tin
---
## 1. Cấu trúc thư mục
- `pom.xml`: Cấu hình Maven (JDK 17, Oracle JDBC `ojdbc11`, lớp chính `week_03.frm_Menu`).
- `03_ORACLE/`:
  - `01_Tao_User_Oracle.sql`: Tạo tài khoản `lab3_user` trong Oracle PDB `FREEPDB1`.
  - `02_Tao_Bang_Oracle.sql`: Tạo bảng `History` trong schema `lab3_user`.
  - `03_KiemTra_LichSu_Oracle.sql`: Kiểm tra dữ liệu lịch sử đã lưu và thống kê số lần theo thuật toán/thao tác.
- `src/main/java/week_03/`:
  - Dùng chung & CSDL: `CryptoSupport.java`, `FileTextIO.java`, `DbConfig.java`, `HistoryDao.java`.
  - Thuật toán & Console: `RSACipher.java`, `RSADemo.java` (Bài 3.1), `ECCCipher.java` (Bài 3.3), `RSA_AES_Cipher.java` (Bài 3.4), `ECCSignature.java` (Bài 3.5).
  - Giao diện Swing: `frm_Menu.java`, `frm_KetNoiSQL.java`, `frm_LichSu.java`, `frm_RSA.java`, `frm_ECC.java`, `frm_RSA_AES.java`, `frm_ECC_Signature.java`.
---
## 2. Yêu cầu môi trường
- **JDK 17** trở lên
- **Apache NetBeans** (bản 20 trở lên)
- **Oracle Database** (đang chạy PDB `FREEPDB1`, cổng `1521`) + SQL Developer hoặc SQL*Plus
---
## 3. Hướng dẫn chuẩn bị cơ sở dữ liệu Oracle
1. Mở SQL Developer (hoặc SQL*Plus), kết nối vào PDB `FREEPDB1` bằng tài khoản quản trị (`SYS` / `SYSTEM`).
2. Mở và chạy script `03_ORACLE/01_Tao_User_Oracle.sql` (bấm **F5 - Run Script**) để tạo user `lab3_user` với mật khẩu `LabUser@2026`.
3. Tạo kết nối mới bằng tài khoản `lab3_user` (Hostname: `127.0.0.1`, Port: `1521`, Service Name: `FREEPDB1`, Password: `LabUser@2026`).
4. Mở và chạy script `03_ORACLE/02_Tao_Bang_Oracle.sql` (bấm **F5**) để tạo bảng `lab3_user.History`.
---
## 4. Hướng dẫn chạy chương trình Java (NetBeans)
1. Mở NetBeans → **File → Open Project...** → chọn thư mục `LAB3_MaHoaKhoaCongKhai`.
2. Nhấp phải tên project → **Clean and Build (`Shift + F11`)** để Maven tải thư viện `ojdbc11` rồi biên dịch.
3. **Chạy Bài 3.1 (Console):** Nhấp phải tệp `RSADemo.java` → **Run File (`Shift + F6`)**, nhấp chuột vào cửa sổ Output để nhập kích thước khóa (`2048` hoặc `3072`) và bản rõ (`HELLO RSA`).
4. **Chạy toàn bộ chương trình:** Nhấp phải tên project → **Run (`F6`)** để mở cửa sổ chính `frm_Menu`.
5. Trên `frm_Menu`:
   - Bấm **Kết nối Oracle** → nhập Password `LabUser@2026` → **Test Connection** (thông báo thành công là có thể lưu lịch sử thao tác).
   - Chọn lần lượt các bài:
     - **3.2 RSA (Swing)**: Tạo cặp khóa 2048/3072 bit, mã hóa/giải mã `HELLO RSA`.
     - **3.3 ECC**: Tạo/lưu/nạp cặp khóa `secp256r1`, mã hóa/giải mã `HELLO ECC`, thử giải mã sai khóa.
     - **3.4 RSA + AES**: Mã hóa/giải mã văn bản dài trên 1 000 ký tự, thử **Sửa 1 ký tự bản mã** để kiểm tra phát hiện sai lệch của AES-GCM.
     - **3.5 Chữ ký ECDSA**: Ký và xác minh thông điệp `THONG DIEP A` (`VALID`), sửa thông điệp hoặc đổi khóa để kiểm tra `INVALID`.
   - Bấm **Xem lịch sử** (hoặc chạy `03_ORACLE/03_KiemTra_LichSu_Oracle.sql`) để kiểm tra dữ liệu lưu trong Oracle.
