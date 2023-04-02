# Chương 1 Tổng quan
* Dịch vụ an toàn
    - Bí mật
    - Xác thực
    - Toàn vẹn
    - Sẵn sàng
    - Chống chối bỏ
* Kỹ thuật an toàn
    - Ngăn cản vật lý
    - Định danh
    - Cấp quyền
    - Xác thực
    - Mã hóa
    - Ký số
* Giao thức mạng là tập hợp các quy tắc và quy ước điều khiển việc trao đổi thông tin giữa các hệ thống máy tính.
* Giao thức an toàn mạng là một giao thức mật mã được sử dụng để bảo vệ dữ liệu trên máy tính và dữ liệu truyền thông.
![](https://i.imgur.com/nkWGCyo.png)
* Giao thức xác thực: PAP/CHAP, Kerberos,EAP
* Các giao thức an toàn ở tầng Application và Transport: S/MIME, SSH, SSL/TLS
* Giao thức an toàn ở Network: IPsec
* Giao thức an toàn ở tầng Datalink: WEP, WPA, WPA2

# Chương 2 Các giao thức xác thực
## 2.1 
* Xác thực là hành vi xác nhận sự thật một thuộc tính của một đối tượng hoặc một chủ thể: 
    - Xác thực thông điệp là một cơ chế cho phép khẳng định rằng thông điệp không bị thay đổi trong quá trình truyền và bên nhận có thể kiểm tra được nguồn gốc của thông điệp.
    - Xác thực thực thể là một thủ tục mà qua đó, một thực thể thiết lập một tính chất được yêu cầu cho một thực thể khác. Thực thể: người dùng, tiến trình, client, server / Tính chất được yêu cầu: có mật khẩu đúng, có nắm giữ khóa bí mật...
* Ký hiệu quy ước
     - Alice (A), Bob (B)... là tên của thực thể;
    - Alice -> Bob: m: Alice gửi m đến Bob;
    - {m}K: mã hóa m bởi khóa K;
    - PA: : mật khẩu của A
    - KPA : Khóa công khai của A
    - Khóa công khai của A;
    - TA: tem thời gian tạo bởi thực thể A;
    - NA: số ngẫu nhiên tạo bởi thực thể A;
    - sigA (m): chữ ký số tạo bởi thực thể A trên thông báo m;
* Nonce 
    - là một đại lượng được sinh ngẫu nhiên, sao cho không bao giờ lặp lại
    - Để không lặp lại, nonce thường có kích thước lớn (~128 bít)
    - Việc nonce không lặp lại giúp đảm bảo tính tươi của thông điệp (thông điệp chỉ được sử dụng 1 lần) trong xác thực
    - Nonce luôn được sinh bởi bên xác thực (authentication server).
* Timestamp
    - đại lượng chỉ thời gian trên đồng hồ của mỗi bên tham gia xác thực.
    - Luôn có sự sai lệch giữa đồng hồ của các bên nên phải xác định một sai số chấp nhận được
    - Mỗi timestamp sẽ hợp lệ trong một khoảng thời gian nhất định -> để chống tấn công phát lại (replay attack) bên xác thực cần có cơ chế đảm bảo mỗi timestamp chỉ được sử dụng một lần (ví dụ: ghi nhớ timestamp gần nhất được sử dụng bởi mỗi thực thể)

## 2.2
* Supplicant (hoặc Peer) Bên được xác thực
* Authenticator: Bên xác thực
* Authentication Server (AS): Máy chủ xác thực
* Network Access Server (NAS): Máy chủ truy cập
### PAP và CHAP
* PAP và CHAP là 2 giao thức xác thực được sử dụng trong giao thức PPP 
* PAP (0xC023) và CHAP (0xC223) đều sử dụng mật khẩu để xác thực
    - PAP (RFC 1334, Password Authentication Protocol) truyền mật khẩu dạng rõ
    - CHAP (RFC 1994, Challenge Handshake Authentication Protocol) sử dụng cơ chế thách đố, giải đố
#### PAP (Password Authentication Protocol)
Là giao thức bắt tay 2 bước (2-way)
* Xác thực bằng mật khẩu
    - Mật khẩu truyền ở dạng rõ
    - Có thể bị chặn thu trên đường truyền
#### CHAP (Challenge Handshake Authentication Protocol)
Là giao thức bắt tay 3 bước (3-way)
• Xác thực sử dụng mật khẩu
• Không truyền mật khẩu dạng rõ (nhưng vẫn lưu mật khẩu dạng rõ)

### KERBEROS 
* Mục tiêu: xác thực hai chiều trong mô hình client-server
* Dựa trên giao thức Needham-Schroeder
* Sử dụng mật mã đối xứng; có bên thứ ba tin cậy là “Trung tâm phân phối khóa” (Key distribution Center).
* Là giao thức Single Sign-On (SSO)
* Có nhiều phiên bản: 1, 2, 3 và 4, 5
* Giao thức Needham-Schroeder
    - Alice và Bob cùng tin tưởng Sandy
    - Alice và Sandy chia sẻ khóa KAS;
    - Bob và Sandy chia sẻ KBS;
* AS: Authentication Server
* TGS: Ticket Granting Server
* KDC (= AS+TGS): Key Distribution Center
* SS: Service Server
* TGT: Ticket Granting Ticket
* ST: Service Ticket

* Giao thức Kerberos: Nguyên lý chung
    - Client yêu cầu truy cập ( gửi tới AS ) (1)
    - KDC (AS) cấp một phiếu truy cập (TGT) cho Client (2)
    - Client Sử dụng TGT để yêu cầu truy cập một dịch vụ cụ thể (TGS) (3)
    - TGS Cấp phiếu truy cập dịch vụ (ST) cho Client (4)
    - Client sử dụng ST để yêu cầu phục vụ SS (5)
    - SS Đáp ứng yêu cầu của Client (6)
![](https://i.imgur.com/BxBTNQu.png)


![](https://i.imgur.com/NjmGzvv.png)
![](https://i.imgur.com/EFqzEqx.png)
![](https://i.imgur.com/8JYgzwf.png)
![](https://i.imgur.com/jvPQL9x.png)
![](https://i.imgur.com/e7amjZP.png)
![](https://i.imgur.com/PXPjb0V.png)


### EAP, 802.1x và RADIUS
* EAP Extensible Authentication Protocol
    - RFC 3748
    - Không cố định phương thức xác thực
* 802.1x
    - 802: IEEE standards for networking protocols
    - 802.11: wireless LAN protocols and standard
    - 802.1: general concepts relating to LANs/WANs
    - “802.1X” (not 802.11X): standards for LANs
    - 802.1X (EAPOL) là chuẩn quy định sử dụng EAP qua môi trường LAN (ở tầng MAC) EAPOL
* RADIUS
    - Remote Authentication Dial-In User Service
     - RFCs: 2865, 2866, 3579... 
     - Được thiết kế theo kiến trúc AAA (Authentication-Authorization-Accouting)
     - Xác thực: EAP, PAP, CHAP...
![](https://i.imgur.com/SnWhmfw.png)

# Chương 3
## 3.1
* Giao thức HTTP HyperText Transfer Protocol
    - Cổng 80 TCP
    - Là giao thức chủ đạo cho web
    - Phiên bản
        + Ver 0.9, 1.0: thuần túy văn bản
        + Ver 1.1: hỗ trợ "application/octet-stream"
        + Ver 2: chủ yếu là binary
    - Request – Response (Yêu cầu – Đáp ứng)
    - Không trạng thái
    - Vấn đề an toàn HTTP
        + Client không thể xác thực Server
        + Client có thể được xác thực bởi
        + Web Server: Basic, Digest... nhưng hiếm khi được sử dụng
        + Web Application: username/password (KHÔNG thuộc phạm vi giao thức HTTP)
        + Ngoài một vài cơ chế xác thực, HTTP không cung cấp dịch vụ an toàn nào khác (bí mật, toàn vẹn)
    - HTTPS = HTTP over TLS 
    - Sử dụng TLS : 
        + Kích hoạt TLS trước khi bắt đầu HTTP
        + Gọi TLS như là một dịch vụ tùy chọn(Alternative Services) của HTTP: 
                - RFC 7838: HTTP Alternative Services
                - RFC 8164: Opportunistic Security for HTTP/2


