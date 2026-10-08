# Bài 3: Thiết lập Cơ sở dữ liệu và Tự cấu hình dịch vụ Systemd cho Spring Boot

## 1. Khởi tạo Cơ sở dữ liệu và User MySQL

```sql
-- Đăng nhập MySQL: sudo mysql -u root -p
CREATE DATABASE springboot_db;
CREATE USER 'spring-admin'@'localhost' IDENTIFIED BY 'SpringSecure@123';
GRANT ALL PRIVILEGES ON springboot_db.* TO 'spring-admin'@'localhost';
FLUSH PRIVILEGES;
```

## 2. Tạo User hệ thống Linux

```bash
sudo useradd -r -s /usr/sbin/nologin spring-runner
```

## 3. Cấu hình dịch vụ Systemd

File `spring-app.service` đã được tạo tại: `/etc/systemd/system/spring-app.service`.
Các lệnh để kích hoạt dịch vụ:
```bash
sudo systemctl daemon-reload
sudo systemctl start spring-app
sudo systemctl enable spring-app
```

## 4. Kết quả kiểm tra

### Trạng thái dịch vụ:
Kết quả của lệnh `sudo systemctl status spring-app.service`:
*(Chèn ảnh chụp màn hình hoặc copy paste kết quả có chữ active (running) tại đây)*

### Kiểm tra cổng lắng nghe:
Kết quả của lệnh `sudo ss -tlnp | grep 8082`:
*(Chèn ảnh chụp màn hình hoặc copy paste kết quả hiển thị tiến trình java đang lắng nghe cổng 8082 dưới quyền spring-runner)*
