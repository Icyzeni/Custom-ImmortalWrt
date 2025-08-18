# ImmortalWrt x86/64 ImageBuilder 快速构建

基于 ImmortalWrt 24.10 ImageBuilder 的 x86/64 固件快速构建项目。

## ✨ 特性

- 🚀 **快速构建**：使用 ImageBuilder，构建时间仅需 5-10 分钟
- 🎯 **专为 x86/64 优化**：基于 ImmortalWrt 24.10 稳定版
- 📦 **自定义软件源**：已集成 https://op.dllkids.xyz/packages/x86_64/
- 🔧 **模块化配置**：易于定制和维护
- ⚡ **自动化发布**：构建完成自动发布到 GitHub Releases

## 🚀 快速开始

1. **Fork 本仓库**到您的 GitHub 账户
2. **启用 Actions**：Settings → Actions → General → Allow all actions
3. **触发构建**：Actions → Build ImmortalWrt x86/64 with ImageBuilder → Run workflow

## 📁 项目结构

```
Custom-ImmortalWrt/
├── .github/workflows/build-immortalwrt.yml  # GitHub Actions 工作流
├── config/
│   ├── packages.conf                        # 软件包配置文件
│   └── repositories.conf                    # 自定义软件源配置
├── files/                                   # 自定义文件目录（可选）
└── README.md                               # 说明文档
```

## ⚙️ 自定义配置

### 软件包配置 (config/packages.conf)

编辑 `config/packages.conf` 文件来定制您的固件：

```bash
# 安装软件包（直接写包名）
luci-app-passwall
luci-app-ssr-plus
luci-app-ddns

# 移除软件包（以 - 开头）
-wpad-basic
-ppp
-ppp-mod-pppoe

# 注释行（以 # 开头）
# 这是注释，不会被处理
```

### 软件源配置 (config/repositories.conf)

编辑 `config/repositories.conf` 文件来配置自定义软件源：

```bash
# 自定义软件源配置
# 格式：src/gz <name> <url>

# 自定义软件源 - op.dllkids.xyz
src/gz custom_packages https://op.dllkids.xyz/packages/x86_64/packages
src/gz custom_luci https://op.dllkids.xyz/packages/x86_64/luci

# 第三方软件源（根据需要启用）
# src/gz kenzok8_packages https://op.supes.top/packages/x86_64
```

### 自定义文件

在 `files/` 目录中放置自定义文件，这些文件会被复制到固件的根文件系统中：

```
files/
├── etc/
│   ├── config/
│   │   ├── network      # 网络配置
│   │   ├── wireless     # 无线配置
│   │   └── system       # 系统配置
│   └── banner           # 登录横幅
└── root/
    └── .bashrc          # root 用户配置
```

## 🔧 构建配置

### 构建触发方式

- **手动触发**：Actions 页面点击 "Run workflow"
- **定时构建**：每周五上午 8 点自动构建
- **Watch 触发**：Star 本仓库触发构建
- **API 触发**：通过 repository_dispatch 事件

### 固件规格

- **目标平台**：x86/64 (generic)
- **根文件系统大小**：512MB
- **默认软件源**：ImmortalWrt 官方 + 自定义源
- **构建时间**：约 5-10 分钟

## 📦 内置软件源

项目已配置以下软件源：

1. **ImmortalWrt 官方源**（默认）
2. **自定义源**：https://op.dllkids.xyz/packages/x86_64/
3. **第三方源**：https://op.supes.top/packages/x86_64

## 🎯 常用插件配置

### 科学上网
```bash
luci-app-passwall
luci-app-ssr-plus
luci-app-openclash
```

### 网络工具
```bash
luci-app-ddns
luci-app-upnp
luci-app-nlbwmon
luci-app-sqm
```

### 存储和下载
```bash
luci-app-samba4
luci-app-aria2
luci-app-transmission
luci-app-qbittorrent
```

### 系统工具
```bash
luci-app-ttyd
luci-app-webadmin
luci-app-adguardhome
luci-app-statistics
```

## 🔍 故障排除

### 构建失败
1. 检查 Actions 日志中的错误信息
2. 确认软件包名称正确
3. 检查软件源是否可用

### 软件包不存在
1. 在 ImageBuilder 中运行 `make info` 查看可用软件包
2. 检查软件包是否在配置的软件源中
3. 尝试使用不同的软件包名称

### 固件过大
1. 移除不必要的软件包
2. 增加 ROOTFS_PARTSIZE 参数
3. 使用精简版软件包

## 📝 更新日志

- **v1.0.0**：基于 ImageBuilder 的快速构建方案
- 支持自定义软件包配置
- 集成多个软件源
- 自动发布到 GitHub Releases

## 🤝 贡献

欢迎提交 Issue 和 Pull Request 来改进这个项目！

## 📄 许可证

本项目基于 MIT 许可证开源。

## 🙏 致谢

- [ImmortalWrt](https://github.com/immortalwrt/immortalwrt) 项目团队
- [OpenWrt](https://openwrt.org/) 社区
- 所有贡献者和用户