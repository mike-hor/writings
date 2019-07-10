# 由于墙的原因或是资源下载过慢 导致打包失败

将 7z 文件下载到 以下 cache 目录并解压
```bash
macOS: ~/Library/Caches/electron-builder
Linux: ~/.cache/electron-builder
windows: %LOCALAPPDATA%\electron-builder\cache
```
目录结构如下
```html
├── nsis-resources
│   └── nsis-3.0.1.13
│   └── nsis-resources-3.3.0
└── winCodeSign
    └── winCodeSign-1.9.0
```
