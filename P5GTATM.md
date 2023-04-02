
802.11
– WEP (Wired Equivalent Privacy): (1997)
+ CRC-32
+ RC4

802.11i
– WPA (Wi-fi Protected Access): (2003)
+ TKIP (Temporal Key Integrity Protocol), Michael-64
+ RC4
+ 802.1x/EAP

– WPA2 = RSN:(2004)
+ CCMP (Counter Mode CBC-MAC Protocol)
+ AES/TKIP (RC4, Michael)
+ 802.1X/EAP (TKIP, EAP-TLS)
# Chương 5 An toàn trong WLAN 


# Giao thức an toàn WEP
* Chuẩn 802.11 
* Mã hóa: 
     - Sử dụng RC4, Khóa dài 40 bit, hoặc 104 bit
     - IV dài 24 bit
* Xác thực: Mở / Khóa chia sẻ
* Kiểm tra toàn vẹn CRC-32
* Quản lí khóa: Sử dụng khóa chia sẻ trước, không có trao đổi khóa tự động, không có cách quản lý cơ sở khóa an toàn, không làm mới khóa một cách an toàn.
* Không chống được tấn công phát lại
# Giao thức an toàn WPA
* Gồm 2 chế độ hoạt động
    - WPA doanh nghiệp: TKIP/MIC ; 802.1X/EAP
    - WPA cá nhân: TKIP/MIC; PSK
* Mã hóa 
    - Sử dụng TKIP (bắt buộc) để mã hóa
    - Thuật toán mã: RC4 => Đã vá những lỗ hổng của WEP / IV dài hơn (48 bit) + Hàm trộn khóa (Lấy ra một khóa cho mỗi gói tin) + MIC (8 byte => Michael)
* Xác thực và quản lí khóa
    - 802.1x kết hợp với EAP, PSK
* Kiểm tra toàn vẹn: Michael => MIC
* Chống tấn công phát lại: 48bit bộ đếm chuỗi TKIP (TSC)
# Giao thức an toàn WPA2 = RSN
* Mã hóa: 
    - Sử dụng thuật toán AES
    - Giao thức TKIP 
* Xác thực:
    - 802.1X/EAP (TKIP, EAP-TLS), PSK
* Toàn vẹn: 
    - CCMP (Counter Mode CBC-MAC Protocol) = CRT + CBC-MAC
* Chống tấn công phát lại
     - Dùng số thứ tự gói tin (48 bit) – PN để ngăn chặn tấn công phát lại

|                    | WEP   | WPA       |   WPA2          |
| --------------------- | ------ | ----------- | ----------- |
| Thuật toán mã hóa     | RC4    | RC4(TKIP)   | AES-CCMP    |
| Kiểm tra toàn vẹn     | CRC-32 | Michael     | CCMP        |
| Phân phối khóa        | Manual | 802.1x(EAP) | 802.1x(EAP) |
| Ad-hoc Security (P2P) | No     | No          | Yes(IBSS)   |
| Pre - authentication  | No     | No          | Yes(EAPOL)  |
