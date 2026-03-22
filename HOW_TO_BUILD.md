# OpenWrt PZ-L8 自动构建状态

## 仓库地址

https://github.com/orlog-data/openwrt-pz-l8

## 触发构建

### 方法一：手动触发（推荐）

1. 访问仓库的 **Actions** 页面
2. 选择 **Build OpenWrt for CMCC PZ-L8** 工作流
3. 点击 **Run workflow** 按钮
4. 选择参数：
   - `upload_release`: 选择 `true`（默认）
5. 点击绿色按钮开始构建

### 方法二：通过 API 触发

```bash
curl -X POST \
  -H "Authorization: token YOUR_GITHUB_TOKEN" \
  -H "Accept: application/vnd.github.v3+json" \
  https://api.github.com/repos/orlog-data/openwrt-pz-l8/actions/workflows/build.yml/dispatches \
  -d '{"ref":"main","inputs":{"upload_release":"true"}}'
```

## 构建时间

- GitHub Actions 使用 2核7G 的 Ubuntu 22.04 环境
- 完整构建约需 **2-4 小时**

## 固件下载

构建完成后，固件将发布到：
- **Releases**: https://github.com/orlog-data/openwrt-pz-l8/releases
- **Artifacts**: Actions 运行页面的 Artifacts 区域

## 固件文件

| 文件 | 用途 |
|------|------|
| `openwrt-qualcommax-ipq50xx-cmcc_pz-l8-squashfs-sysupgrade.bin` | 系统升级/刷写 |
| `openwrt-qualcommax-ipq50xx-cmcc_pz-l8-initramfs-uImage.itb` | 救援模式启动 |

## 包含特性

- **PR #21495**: ath11k smallbuffers - 256MB 内存优化
- **PR #21496**: PZ-L8 双 CPU 链接 - 2Gbps 支持
- 移除 DNS/DHCP/Firewall（纯 AP 模式）
- 添加 Mesh 网络和 Usteer 漫游
- LuCI 中文界面

## 本地修改说明

如果需要修改配置：

1. 修改 `config-pz-l8` 文件
2. 提交并推送到 main 分支
3. 重新触发 workflow

```bash
git add config-pz-l8
git commit -m "Update config"
git push
```
