# OpenWrt for CMCC PZ-L8

通过 GitHub Actions 自动构建的 OpenWrt 固件，专为 CMCC PZ-L8（IPQ5018）设备优化。

## 特性

| 特性 | 说明 |
|------|------|
| PR #21495 | ath11k smallbuffers - 256MB 内存优化 |
| PR #21496 | PZ-L8 双 CPU 链接 - 2Gbps 支持 |
| 精简组件 | 移除 DNS/DHCP/Firewall（纯 AP 模式） |
| Mesh 网络 | wpad-mesh-mbedtls 支持 |
| 漫游管理 | Usteer 无线漫游 |
| Web 界面 | LuCI 中文界面 |

## 构建固件

### 手动触发构建

1. 访问 [Actions](https://github.com/orlog-data/openwrt-pz-l8/actions)
2. 选择 **Build OpenWrt for CMCC PZ-L8**
3. 点击 **Run workflow**
4. 等待构建完成（约 2-4 小时）

### 下载固件

- **Releases**: https://github.com/orlog-data/openwrt-pz-l8/releases
- **Artifacts**: Actions 运行页面的 Artifacts 区域

## 固件文件

| 文件 | 用途 |
|------|------|
| `*squashfs-sysupgrade.bin` | 系统升级/刷写 |
| `*initramfs-uImage.itb` | 救援模式启动 |

## 目录结构

```
.
├── .github/workflows/build.yml   # GitHub Actions 构建配置
├── config-pz-l8                  # OpenWrt 配置文件
├── package/kernel/mac80211/patches/ath11k/
│   └── 951-*.patch               # ath11k smallbuffers 补丁
└── target/linux/qualcommax/patches-6.12/
    ├── 0752-*.patch              # DSA PHY-to-PHY 支持
    ├── 0754-*.patch              # 多 CPU 端口选择
    └── 0755-*.patch              # preferred_default_local_port
```

## 自定义配置

修改 `config-pz-l8` 文件后提交推送，然后手动触发构建即可。

## 许可证

MIT License
