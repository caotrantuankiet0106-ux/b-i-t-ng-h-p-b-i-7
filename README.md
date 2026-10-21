# Phần 1 – Đọc và định vị tệp tin
Lệnh đọc log: Get-Content logs\server.log

Lý do treo máy (Notepad vs Terminal): Notepad tải toàn bộ file 500 MB vào RAM cùng lúc gây cạn kiệt tài nguyên; trong khi PowerShell đọc dữ liệu theo từng dòng (streaming) giúp tiết kiệm RAM tối đa.

Lệnh tìm file .log đệ quy: Get-ChildItem -Filter "*.log" -Recurse

# Phần 2 – Lọc dữ liệu và Pipe
Lệnh lọc ERROR: Get-Content logs\server.log | Select-String "ERROR"

Bảng phân biệt:

Tìm vị trí file: Get-ChildItem -Filter "server.log" -Recurse

Tìm nội dung chứa 404: Select-String "404" logs\server.log

Lệnh kết hợp Pipe lọc 404: Get-Content logs\server.log | Select-String "404"

Lệnh tìm file log và lọc bỏ dòng chứa INFO: Get-ChildItem -Filter "*.log" -Recurse | Get-Content | Select-String "INFO" -NotMatch

# Phần 3 – Toán tử chuyển hướng > và >>
Lệnh ghi đè (>): Get-Content logs\server.log | Select-String "404" > reports\daily_report.txt

Lệnh ghi nối (>>): Get-Content logs\server.log | Select-String "404" >> reports\daily_report.txt

Hậu quả dùng nhầm >: Báo cáo cũ bị xóa sạch hoàn toàn và thay thế bằng kết quả mới nhất.

# Phần 4 – Shell Script và lệnh echo
Lệnh thông báo và tiêu đề:

Thông báo: Write-Output "Dang loc log..."

Tiêu đề: Write-Output "=== LOG REPORT ===" > reports\daily_report.txt

Nội dung file scripts\auto_report.ps1:

PowerShell
# Script tu dong loc log 404
Write-Output "Bat dau chay tien trinh xu ly log..."
Get-Content logs\server.log | Select-String "404" >> reports\daily_report.txt
# Phần 5 – Viết, chạy và thẩm định Script AI
Quy trình thực thi:

(a) Lệnh chạy: .\scripts\auto_report.ps1

(b) Lệnh kiểm tra: Get-Content reports\daily_report.txt

Thẩm định Script AI:

(a) Dòng lệnh nguy hiểm: Remove-Item -Recurse -Force C:\* 
→
→ Xóa toàn bộ file hệ thống ổ C, dẫn đến sập hệ thống/mất dữ liệu vĩnh viễn.

(b) Sửa đường dẫn an toàn: Thay bằng Remove-Item -Recurse -Force temp\*.
