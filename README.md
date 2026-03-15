# ImmortalWrt 24.10 X86/64 编译配置

> **作者:** Russell Lee  
> **源码:** ImmortalWrt openwrt-24.10 分支  
> **目标平台:** X86/64

---

## 📦 已包含插件

### 主题
- ✅ luci-theme-argon (Argon 主题)
- ✅ luci-app-argon-config (Argon 主题设置)

### 科学上网
- ✅ luci-app-homeproxy (现代化代理工具)

### DNS 配置
- ✅ luci-app-smartdns (智能 DNS)
- ✅ luci-app-nextdns (NextDNS 服务)

### 下载工具
- ✅ luci-app-qbittorrent (BT 下载)
- ✅ luci-app-filebrowser (文件浏览器)

### 内网穿透
- ✅ luci-app-frpc (Frp 客户端)
- ✅ luci-app-frps (Frp 服务端)

### 网络工具
- ✅ luci-app-upnp (自动端口映射)
- ✅ luci-app-wol (网络唤醒)

### 系统工具
- ✅ luci-app-cpufreq (CPU 频率调节)
- ✅ luci-app-ttyd (Web 终端)
- ✅ luci-app-samba4 (SMB 文件共享)
- ✅ luci-app-diskman (磁盘管理)

### 安全/监控
- ✅ luci-app-banip (IP 黑名单)
- ✅ luci-app-nlbwmon (带宽监控)
- ✅ luci-app-statistics (系统统计)

---

## 🚀 使用方法

### 方式一：手动触发编译

1. 点击 **Actions** 标签页
2. 选择 **Build ImmortalWrt X86/64** 工作流
3. 点击 **Run workflow**
4. 选择是否上传到 Releases
5. 等待编译完成（约 30-40 分钟）

### 方式二：自动定时编译

默认每周日 2:00 UTC 自动编译并上传到 Releases

---

## 📥 下载固件

编译完成后，固件会：

1. **Artifacts:** 在 Actions 页面下载（保留 90 天）
2. **Releases:** 自动发布到 Releases 页面（保留最新 5 个版本）

---

## 💻 本地编译

```bash
# 克隆仓库
git clone https://github.com/你的用户名/immortalwrt-x86.git
cd immortalwrt-x86

# 克隆源码
git clone --depth 1 -b openwrt-24.10 https://github.com/immortalwrt/immortalwrt.git

# 复制配置
cp .config immortalwrt/
cp feeds.conf.default immortalwrt/

# 编译
cd immortalwrt
./scripts/feeds update -a
./scripts/feeds install -a
make defconfig
make -j$(nproc) V=s

# 固件位置
cd bin/targets/x86/64/
ls -la *.img.gz
```

---

## 🔧 自定义配置

### 添加插件

编辑 `.config` 文件，添加：
```bash
CONFIG_PACKAGE_luci-app-插件名=y
```

### 修改作者信息

编辑 `.config` 文件中的：
```bash
CONFIG_VERSION_MANUFACTURER="你的名字"
```

### 更改定时编译

编辑 `.github/workflows/build.yml` 中的：
```yaml
schedule:
  - cron: '0 2 * * 0'  # 修改为需要的 Cron 表达式
```

---

## ⚠️ 注意事项

1. **GitHub Actions 限制:**
   - 免费账户：每月 2000 分钟
   - 单次编译最长 6 小时
   - 磁盘空间：约 14GB

2. **固件大小:**
   - 默认配置约 100-200MB
   - 如需精简，编辑 `.config` 禁用不需要的包

3. **首次使用:**
   - 默认 IP: `192.168.1.1`
   - 默认密码：`password`
   - 首次登录需修改密码

---

## 📝 常见问题

### Q: 编译失败怎么办？
A: 查看 Actions 日志，通常是网络问题或依赖缺失

### Q: 如何添加 Docker 支持？
A: 在 `.config` 中添加：
```bash
CONFIG_PACKAGE_luci-app-docker=y
CONFIG_PACKAGE_docker-ce=y
```

### Q: 如何更改默认 IP？
A: 编译后在 LuCI 界面修改，或编辑 `package/base-files/files/etc/config/network`

---

## 📄 许可证

- ImmortalWrt: [GPL-2.0](https://github.com/immortalwrt/immortalwrt/blob/openwrt-24.10/LICENSE)
- 本配置：MIT License

---

## 🔗 相关链接

- [ImmortalWrt 官网](https://immortalwrt.org/)
- [ImmortalWrt GitHub](https://github.com/immortalwrt)
- [OpenWrt 文档](https://openwrt.org/)
- [GitHub Actions 文档](https://docs.github.com/en/actions)

---

**Happy Flashing! 🎉**
