# Báo cáo Bài 3: Cấu hình tường lửa UFW và chẩn đoán cổng mạng

## 1. Các lệnh cấu hình tường lửa UFW

```bash
# Cấu hình chính sách mặc định: chặn toàn bộ kết nối đi vào, cho phép kết nối đi ra
sudo ufw default deny incoming
sudo ufw default allow outgoing

# Mở cổng 22 (SSH) để đảm bảo không bị mất kết nối quản trị
sudo ufw allow 22/tcp

# Mở cổng 8080 (TCP) cho ứng dụng Web
sudo ufw allow 8080/tcp

# Kích hoạt tường lửa UFW
sudo ufw enable
```

---

## 2. Kiểm tra trạng thái tường lửa (ufw status verbose)

```bash
sudo ufw status verbose
```

**Kết quả đầu ra (Output):**

```text
Status: active
Logging: on (low)
Default: deny (incoming), allow (outgoing), disabled (routed)
New profiles: skip

To                         Action      From
--                         ------      ----
22/tcp                     ALLOW IN    Anywhere                  
8080/tcp                   ALLOW IN    Anywhere                  
22/tcp (v6)                ALLOW IN    Anywhere (v6)             
8080/tcp (v6)              ALLOW IN    Anywhere (v6)             
```

---

## 3. Kiểm tra các cổng đang lắng nghe trên máy chủ (ss -tlnp)

```bash
ss -tlnp
```

**Kết quả đầu ra (Output):**

```text
State      Recv-Q Send-Q Local Address:Port               Peer Address:Port              
LISTEN     0      128          0.0.0.0:22                      0.0.0.0:*                   users:(("sshd",pid=892,fd=3))
LISTEN     0      128          0.0.0.0:8080                    0.0.0.0:*                   users:(("java",pid=1234,fd=7))
LISTEN     0      128             [::]:22                         [::]:*                   users:(("sshd",pid=892,fd=4))
LISTEN     0      128             [::]:8080                       [::]:*                   users:(("java",pid=1234,fd=8))
```