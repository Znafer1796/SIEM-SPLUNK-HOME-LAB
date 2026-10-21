# SIEM Splunk Home Lab

Dự án thực hành **Hệ thống quản lý thông tin và sự kiện an toàn thông tin (SIEM)**, tập trung vào thu thập log tập trung từ firewall, giám sát an ninh mạng và điều tra sự kiện bảo mật.

## Tổng quan

Dự án tìm hiểu cách triển khai giải pháp SIEM trong môi trường máy ảo nhằm thu thập, tìm kiếm và phân tích log từ firewall.

Mô hình lab sử dụng Splunk Enterprise chạy trên Windows 10, OPNsense làm firewall và Kali Linux làm máy kiểm thử. Hệ thống mạng ảo VMware cung cấp môi trường kết nối và thực hiện các bài kiểm thử bảo mật có kiểm soát.

Mục tiêu chính là tìm hiểu quy trình thu thập log, phân tích sự kiện và phát triển các kỹ năng thực hành liên quan đến Blue Team và quy trình vận hành của Trung tâm Điều hành An ninh mạng (SOC).

## Mục tiêu dự án

- Triển khai Splunk Enterprise trên Windows 10.
- Cấu hình OPNsense ghi log firewall và chuyển tiếp log đến Splunk.
- Phân tích sự kiện thu thập được bằng Splunk Search Processing Language (SPL).
- Tạo lưu lượng mạng có kiểm soát từ Kali Linux để phục vụ kiểm thử.
- Đối chiếu hoạt động kiểm thử với các log firewall tương ứng.
- Ghi lại kiến trúc hệ thống, quá trình cấu hình và kết quả điều tra.

## Kiến trúc hệ thống

Lab bao gồm ba máy ảo chính:

- **Windows 10:** Chạy Splunk Enterprise, thực hiện tiếp nhận, tìm kiếm và phân tích log.
- **OPNsense:** Thực thi các chính sách firewall và tạo log lưu lượng mạng.
- **Kali Linux:** Tạo lưu lượng mạng có kiểm soát để kiểm thử và giám sát.

Quy trình hoạt động dự kiến là chuyển tiếp log phù hợp từ OPNsense đến Splunk, tìm kiếm các sự kiện đã thu thập và điều tra hoạt động phát sinh trong quá trình kiểm thử.

Cấu hình cụ thể của các giao diện mạng, địa chỉ IP, định tuyến và giao thức truyền log được trình bày cùng với bằng chứng triển khai thực tế.

![Sơ đồ kiến trúc hệ thống SIEM Splunk Home Lab](https://github.com/user-attachments/assets/e9c6ce62-4944-48a9-bc98-088cbf4dd10a)

## Kế hoạch triển khai

### 1. Cấu hình mạng ảo

- Cấu hình các card mạng ảo cho từng máy.
- Kiểm tra kết nối giữa các thành phần cần thiết trong lab.
- Ghi lại cấu hình mạng VMnet2 và NAT.

### 2. Cấu hình OPNsense

- Kiểm tra các giao diện mạng và luật firewall.
- Cấu hình các thiết lập ghi log cần thiết.
- Thiết lập chuyển tiếp log đến Splunk Receiver khi phù hợp.

### 3. Triển khai Splunk

- Cài đặt Splunk Enterprise trên Windows 10.
- Cấu hình cổng tiếp nhận log phù hợp.
- Kiểm tra kết nối và xác nhận dữ liệu log được gửi đến Splunk.

### 4. Thu thập và điều tra log

- Tìm kiếm các sự kiện OPNsense được gửi đến Splunk.
- Kiểm tra các trường dữ liệu và dấu thời gian của sự kiện.
- Xây dựng truy vấn SPL để lọc, phân loại và tổng hợp các sự kiện liên quan.

### 5. Kiểm thử bảo mật có kiểm soát

- Tạo lưu lượng kiểm thử được cho phép từ Kali Linux.
- Kiểm tra các sự kiện firewall tương ứng.
- Ghi nhận kết quả, phân tích log và đánh giá những gì dữ liệu thu thập được thể hiện.

## Phân tích log

Phần này trình bày các truy vấn SPL đã được kiểm chứng và những tình huống điều tra sự kiện cụ thể.

Mỗi tình huống phân tích bao gồm:

- **Mục tiêu:** Hành vi hoặc sự kiện cần điều tra.
- **Phương pháp:** Quy trình kiểm thử và truy vấn SPL được sử dụng.
- **Bằng chứng:** Các sự kiện liên quan được ghi nhận trên Splunk.
- **Phân tích:** Ý nghĩa của các trường log và những gì có thể kết luận từ dữ liệu.
- **Giới hạn:** Những nội dung chưa thể xác định chắc chắn từ dữ liệu hiện có.

## Kỹ năng thực hành

- Triển khai và quản trị SIEM ở mức cơ bản.
- Cấu hình firewall và hệ thống ghi log.
- Thu thập log tập trung.
- Tìm kiếm và phân tích sự kiện bằng SPL.
- Khắc phục sự cố mạng ảo.
- Điều tra sự kiện an toàn thông tin.
- Viết tài liệu kỹ thuật và thu thập bằng chứng kiểm thử.

## Hướng phát triển

- Tích hợp log bảo mật Windows và dữ liệu Sysmon.
- Xây dựng dashboard giám sát hoạt động firewall.
- Phát triển các luật cảnh báo cho những sự kiện được lựa chọn.
- Mở rộng các tình huống phân tích log và phát hiện hành vi đáng ngờ.
- Xây dựng quy trình điều tra phù hợp với hoạt động SOC.

## Tuyên bố miễn trừ trách nhiệm

Dự án phục vụ mục đích học tập và thực hành trong môi trường lab được kiểm soát. Mọi hoạt động kiểm thử bảo mật chỉ được thực hiện trên các hệ thống và mạng đã được cấp quyền sử dụng hoặc kiểm thử.
