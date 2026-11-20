# Xnavi Beacon

《塞尔达传说 旷野之息》定位信标模组 —— 为 [Xnavi](https://github.com/ZoruaFox/BOTWmap)
实时定位导航提供**游戏内直报**的坐标。

以往 Xnavi 只能扫描模拟器内存猜测玩家位置，进神庙、传送、站桩等场景容易误判。
本模组以 exlaunch subsdk 形式注入游戏，每 200ms 读取玩家世界坐标写入一块内存信标，
由宿主直接读取：坐标与状态由游戏给出，无需任何推断。

## 组成

| 路径 | 说明 |
|---|---|
| `plugin/` | 插件源码（`main.cpp`）与构建配置，产出 `subsdk9` |
| `beacon.h` | 信标协议定义（64 字节布局、状态枚举、CRC 约定），宿主与插件共用 |
| `docs/协议-v1.md` | 协议与通道说明 |
| `docs/安装与兼容.md` | 安装步骤、兼容性矩阵、故障排查 |
| `NOTICE` | 第三方组件署名与许可证划分 |

宿主侧的读取层（魔数扫描发现、序号判活、三级回退）在 Xnavi 仓库的 `xnavi/` 目录，
与本仓库的 `beacon.h` 协议保持一致。

## 环境要求

- Eden 模拟器
- 《塞尔达传说 旷野之息》1.6.0（TitleID `01007EF00011E000`）
- 构建需要 devkitA64 + libnx + switch-tools（devkitPro 工具链）与 exlaunch 框架

## 构建与安装

见 [plugin/README.md](plugin/README.md)。

## 许可

GPL-2.0（见 `LICENSE`）。协议定义（`beacon.h`）随宿主 MIT 授权。

## 致谢

- [exlaunch](https://github.com/shadowninja108/exlaunch) —— Switch 应用注入框架（GPL-2.0）
- [botw-save-state](https://github.com/Pistonight/botw-save-state) —— 内存偏移资料（GPL-3.0）
