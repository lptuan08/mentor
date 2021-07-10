# Cài đặt các phần mềm khác

## Postman:

Postman là phần mềm giao diện với chức năng chính là API Testing

Cài đặt postman:

1. Chạy lệnh: `flatpak install postman` và xác nhận để cài đặt Postman từ flatpak
2. Kiểm tra Postman đã có trên trong App Launcher chưa

## MongoDB Compass

1. Download deb package của MongoDB Compass từ [trang chủ](https://www.mongodb.com/try/download/compass). Chọn dòng Ubuntu 16+ để tải về
2. Trỏ đến thư mục Downloads bằng lệnh: ```cd ~/Downloads```
3. Thực thi lệnh: 
```bash
    sudo dpkg -i <file-name>.deb
```
(Nếu câu lệnh trên fail, chạy ```sudo apt install -f``` và chạy lại lệnh trên một lần nữa)

4. Kiểm tra MongoDB Compass đã có trong App Launcher chưa