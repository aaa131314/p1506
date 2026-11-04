# 天籁 P150-06 车机 OTA 升级包

日产天籁（Teana）车机系统 OTA 整包，版本号 **P150-06**，内部版本标识 `HSCE_HSAE_MCU_P010_10`。

固件体积 1.59 GiB，超过 GitHub 单文件 100 MB 的硬限制，因此**以 Release 资产形式分发**，不在仓库文件树内。

## 下载

| 文件 | 大小 | SHA256 |
|---|---|---|
| `P150-06.zip` | 1,706,359,374 B（1.59 GiB） | `51655fe63c9453589783eee7a09f8ad59c49ef3db5c8cf32d152f9cb39e0cdcd` |

Release 页：<https://github.com/AAA131314/p1506/releases/tag/P150-06>

## 校验

Windows：

```powershell
Get-FileHash .\P150-06.zip -Algorithm SHA256
```

Linux / macOS：

```bash
shasum -a 256 P150-06.zip
```

摘要必须与上表完全一致，不一致的包不要上车。

## 包结构

```
P150-06.zip                        1,706,359,374 B
├── update.zip                     1,710,600,245 B   ← 主升级镜像（stored，未压缩）
│   ├── update.zip                 1,412,149,555 B   ← 系统分区镜像
│   ├── iflytek.zip                  288,456,528 B   ← 讯飞语音资源
│   ├── res_48M.img.tar.gz             5,681,062 B   ← 48M 分区资源
│   ├── res_24M.img.tar.gz             4,234,451 B   ← 24M 分区资源
│   ├── mcu.bin                          494,080 B   ← MCU 固件
│   ├── config                                64 B    ← 升级配置（二进制）
│   ├── md5                                   32 B    ← 10FEBBDC785850369E5649605BF0856E
│   └── version.txt                           21 B    ← HSCE_HSAE_MCU_P010_10
└── Autoboot_Utility                       8 B        ← 自动引导标记文件
```

整包内层为 stored 方式打包（不压缩），解出后占用约 1.59 GiB 额外磁盘。

## 升级步骤

1. U 盘格式化为 **FAT32**，簇大小默认，容量 ≥ 4 GB。
2. 将 `P150-06.zip` 解压，把 `update.zip` 与 `Autoboot_Utility` 放到 U 盘**根目录**（不要套文件夹）。
3. 车辆处于 P 挡、驻车制动拉起、发动机或电源保持供电（升级中途断电会导致主机变砖）。
4. 插入 U 盘，车机进入设置 → 系统 → 系统升级，按提示执行。
5. 升级过程 15–30 分钟，屏幕可能黑屏重启多次，**不要拔 U 盘、不要断电**。
6. 完成后车机自动重启，确认版本号显示 `P150-06` 再拔出 U 盘。

## 注意

- 该包仅对应 P150 平台车机，刷入其他平台会变砖。
- 升级前建议记录当前版本号，便于回退排查。
- 本仓库仅做镜像归档，固件版权归原厂所有；下载后请自行承担刷机风险。
