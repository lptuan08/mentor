# Setup NVM

## NVM là gì

NVM (viết tắt của Node Version Management) là một tool quản lý các version Node khác nhau trên một máy host.
Người dùng có thể lựa chọn cài đặt các phiên bản NodeJS khác nhau và chuyển đổi qua lại giữa chúng.

## Cài đặt NVM trên Ubuntu/Debian:

1. Đến trang [github của NVM](https://github.com/nvm-sh/nvm#installing-and-updating) và copy dòng sau:

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v<nvm_version>/install.sh | bash
```

2. Sau khi cài đặt thành công, đóng cửa sổ Terminal hiện tại và mở lại một cửa sổ mới. Kiểm tra NVM đã chạy hay chưa bằng lệnh: `nvm --help`. Nếu chưa chạy được, thêm dòng sau vào cuối `~/.bash_profile` (hoặc `~/.profile`, `~/.zshrc`, `~/.bashrc`):

```bash
export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm
```

## Cài đặt NodeJS:

1. Sử dụng lệnh: `nvm ls-remote` kiểm tra các phiên bản NodeJS hiện tại.
2. Sử dụng lệnh: `nvm install <node_version>` để cài đặt chính xác phiên bản NodeJS mà bạn muốn. Hoặc `nvm install latest` để cài phiên bản mới nhất (Recommend sử dụng LTS version mới nhất - NodeJS 14).
3. Kiểm tra NodeJS đã cài đặt hay chưa: `node -v` và cả npm nữa: `npm -v`.
4. Update npm lên version mới nhất nếu muốn: `npm install -g npm`