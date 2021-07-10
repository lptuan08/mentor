# Setup Github với SSH

## SSH là gì?

Đọc bài viết này: [SSH là gì và cách sử dụng SSH cho người mới bắt đầu](https://www.hostinger.vn/huong-dan/ssh-la-gi-va-cach-su-dung-ssh-cho-nguoi-moi-bat-dau)

## Config git:

Sử dụng các lệnh sau để tạo global config:

```bash
git config --global user.name "<Github username>"
git config --global user.email "<Github email>"
```

## Sử dụng SSH với Github:

1. Chạy lệnh sau để generate một SSH key mới:

```bash
ssh-keygen -t ed25519 -C "<Github email>"
```

Chọn nơi lưu trữ key SSH: Mặc định (default) bằng cách nhấn Enter. \
Sau đó nhập passphrase và xác nhận passphrase một lần nữa.

2. Chạy lần lượt các lệnh sau:

```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
xclip -selection clipboard < ~/.ssh/id_ed25519.pub
```

3. Đăng nhập Github trên trình duyệt. Chọn vào hình profile góc trên bên phải: **Settings > SSH and GPG keys > New SSH key**. Đặt title và copy nội dung file đã lưu trữ trên clipboard vào ô Key. Chọn "Add SSH key" để xác nhận

4. Chạy lệnh: `ssh -T git@github.com`. Thấy chữ *success* trong dòng output là thành công