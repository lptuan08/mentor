# Setup Visual Studio Code

## Cài đặt VS Code trên Ubuntu/Debian:

1. Download deb package của VS Code từ [trang chủ](https://code.visualstudio.com/download)
2. Trỏ đến thư mục Downloads bằng lệnh: ```cd ~/Downloads```
3. Thực thi lệnh: 
```bash
    sudo dpkg -i <file-name>.deb
```
(Nếu câu lệnh trên fail, chạy ```sudo apt install -f``` và chạy lại lệnh trên một lần nữa)

4. Kiểm tra VS Code bằng cách chạy: ```code .```

## Cài đặt các Extensions cần thiết

Một số Extensions cần thiết cho môi trường lập trình NodeJS/ReactJS trên VS Code:

- Node.js Extension Pack (Wade Anderson)
- Auto Rename Tag (Jun Han)
- Bracket Pair Colorizer (CoenraadS)
- Color Highlight (Sergii Naumov)
- Material Icon Theme (Phillip Kief)
- Atom One Dark (hoặc bất kỳ color theme nào khác)

## Cấu hình cá nhân hoá VS Code:

VS Code lưu trữ settings như là một file JSON. Có thể mở nó bằng: **File > Preferences > Settings** và click vào icon Open Settings góc trên bên phải

Một số settings cơ bản cho VS Code:

```json
{
  "editor.fontFamily": "Fantasque Sans Mono", // thay đổi font bạn muốn dùng
  "editor.fontSize": 16, // kích cỡ font
  "editor.fontWeight": "400", // 400 - regular, 500 - medium, > 600 - semibold trở lên
  "editor.lineHeight": 24,
  "editor.fontLigatures": true,
  "editor.formatOnSave": true,
  "editor.minimap.enabled": false,
  "editor.suggestSelection": "first",
  "editor.tabSize": 2,
  "emmet.includeLanguages": {
    "javascript": "javascriptreact"
  },
  "files.associations": {
    "*.html": "html"
  },
  "files.exclude": {
    "**/.git": true,
    "**/.svn": true,
    "**/.hg": true,
    "**/CVS": true,
    "**/.DS_Store": true,
    "**/__pycache__": true
  },
  "[html]": {
    "editor.formatOnSave": true
  },
  "javascript.updateImportsOnFileMove.enabled": "always",
  "terminal.integrated.fontSize": 16,
  "typescript.updateImportsOnFileMove.enabled": "always",
  "workbench.startupEditor": "none",
  "workbench.iconTheme": "material-icon-theme", // icon theme
  "workbench.colorTheme": "Ever Night", // color theme
  "scm.inputFontSize": 14,
  "workbench.tree.indent": 14
}
```

Ngoài ra bạn có thể tham khảo thêm một số settings khác của VS Code trên Github của mình: [settings.json](https://github.com/wuallanx/configuration/blob/master/editors/vscode/settings.json)