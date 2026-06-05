# 🔧 Minecraft Java 优化参数 / JVM Optimization Flags for Minecraft

## 📋 参数说明（Parameter Description）
本项目提供经过验证的《我的世界》Java 版 JVM 启动参数，包含**客户端**与**服务端**，覆盖 Java 8、11、17 三个主流运行环境。  
合理使用这些参数可以有效：
- 降低垃圾回收（GC）造成的卡顿
- 提升帧生成时间稳定性
- 优化内存使用效率
- 适配新旧硬件与不同游戏版本

## 🖥️ 客户端优化参数（Client Optimization Flags）

### ☕ Java 8 客户端参数
```bash
-server -Xms4G -Xmx4G -XX:+UseG1GC -XX:+UnlockExperimentalVMOptions -XX:+UseStringDeduplication -XX:+ExplicitGCInvokesConcurrent -XX:MaxGCPauseMillis=50 -XX:+ParallelRefProcEnabled -XX:+AlwaysPreTouch -XX:G1HeapWastePercent=5 -XX:G1MixedGCCountTarget=4 -XX:InitiatingHeapOccupancyPercent=15 -XX:MaxTenuringThreshold=1 -XX:ParallelGCThreads=8 -XX:ConcGCThreads=2 -XX:ReservedCodeCacheSize=240m -XX:MaxInlineLevel=15 -XX:FreqInlineSize=325 -XX:MaxInlineSize=35 -XX:InlineSmallCode=2000 -XX:MinInliningThreshold=250 -XX:MaxRecursiveInlineLevel=1 -XX:-DontCompileHugeMethods -XX:-OmitStackTraceInFastThrow -XX:AutoBoxCacheMax=256 -XX:+UseBiasedLocking -XX:+PerfDisableSharedMem -Dsun.rmi.dgc.server.gcInterval=3600000 -Dfml.ignorePatchDiscrepancies=true -Dfml.ignoreInvalidMinecraftCertificates=true -Dfml.readTimeout=90
```

### ☕ Java 11 客户端参数
```bash
-server -Xms4G -Xmx4G -XX:+UseG1GC -XX:+UnlockExperimentalVMOptions -XX:+UseStringDeduplication -XX:+DisableExplicitGC -XX:MaxGCPauseMillis=50 -XX:+ParallelRefProcEnabled -XX:+AlwaysPreTouch -XX:+UseLargePages -XX:+UseLargePagesInMetaspace -XX:G1HeapWastePercent=5 -XX:G1MixedGCCountTarget=4 -XX:InitiatingHeapOccupancyPercent=15 -XX:MaxTenuringThreshold=1 -XX:SurvivorRatio=32 -XX:ParallelGCThreads=8 -XX:ConcGCThreads=2 -XX:ReservedCodeCacheSize=240m -XX:MaxInlineLevel=15 -XX:FreqInlineSize=325 -XX:MaxInlineSize=35 -XX:InlineSmallCode=2000 -XX:MinInliningThreshold=250 -XX:MaxRecursiveInlineLevel=1 -XX:-DontCompileHugeMethods -XX:-OmitStackTraceInFastThrow -XX:AutoBoxCacheMax=256 -XX:-UseBiasedLocking -XX:+PerfDisableSharedMem -Dsun.rmi.dgc.server.gcInterval=3600000 -Dfml.ignorePatchDiscrepancies=true -Dfml.ignoreInvalidMinecraftCertificates=true -Dfml.readTimeout=90
```

### ☕ Java 17 客户端参数
```bash
-server -Xms4G -Xmx4G -XX:+UseG1GC -XX:+UseStringDeduplication -XX:+DisableExplicitGC -XX:MaxGCPauseMillis=100 -XX:+ParallelRefProcEnabled -XX:+AlwaysPreTouch -XX:+UseLargePages -XX:G1HeapWastePercent=5 -XX:G1MixedGCCountTarget=4 -XX:InitiatingHeapOccupancyPercent=15 -XX:MaxTenuringThreshold=1 -XX:ParallelGCThreads=8 -XX:ConcGCThreads=2 -XX:ReservedCodeCacheSize=240m -XX:MaxInlineLevel=15 -XX:FreqInlineSize=325 -XX:MaxInlineSize=35 -XX:InlineSmallCode=2000 -XX:MinInliningThreshold=250 -XX:MaxRecursiveInlineLevel=1 -XX:-DontCompileHugeMethods -XX:-OmitStackTraceInFastThrow -XX:AutoBoxCacheMax=256 -XX:+PerfDisableSharedMem -Dfml.ignorePatchDiscrepancies=true -Dfml.ignoreInvalidMinecraftCertificates=true -Dfml.readTimeout=90
```

> ⚠️ **注意**：`-Xms` 与 `-Xmx` 请根据你的实际物理内存调整，推荐分配 **4G~8G**，但不要超过系统总内存的 80%。  
> `ParallelGCThreads` 与 `ConcGCThreads` 应设置为 CPU 核心数（逻辑核心）的 **1~2 倍**和 **约 1/4**，请根据你的硬件修改。

---

## 🖧 服务端优化参数（Server Optimization Flags）

服务端参数更侧重**吞吐量**、**稳定GC**与**玩家连接数**，基于 Aikar's Flags 进行优化适配。

### ☕ Java 8 服务端参数
```bash
-server -Xms4G -Xmx4G -XX:+UseG1GC -XX:+UnlockExperimentalVMOptions -XX:+UseStringDeduplication -XX:+ExplicitGCInvokesConcurrent -XX:MaxGCPauseMillis=200 -XX:+ParallelRefProcEnabled -XX:+AlwaysPreTouch -XX:G1NewSizePercent=30 -XX:G1MaxNewSizePercent=40 -XX:G1HeapWastePercent=5 -XX:G1MixedGCCountTarget=4 -XX:InitiatingHeapOccupancyPercent=15 -XX:G1MixedGCLiveThresholdPercent=90 -XX:G1RSetUpdatingPauseTimePercent=5 -XX:SurvivorRatio=32 -XX:MaxTenuringThreshold=1 -XX:ParallelGCThreads=8 -XX:ConcGCThreads=2 -XX:ReservedCodeCacheSize=240m -XX:-DontCompileHugeMethods -XX:+PerfDisableSharedMem -Dfml.ignorePatchDiscrepancies=true -Dfml.ignoreInvalidMinecraftCertificates=true -Dfml.readTimeout=90 -Dcom.mojang.eula.agree=true
```

### ☕ Java 11 服务端参数
```bash
-server -Xms4G -Xmx4G -XX:+UseG1GC -XX:+UnlockExperimentalVMOptions -XX:+UseStringDeduplication -XX:+DisableExplicitGC -XX:MaxGCPauseMillis=200 -XX:+ParallelRefProcEnabled -XX:+AlwaysPreTouch -XX:+UseLargePages -XX:+UseLargePagesInMetaspace -XX:G1NewSizePercent=30 -XX:G1MaxNewSizePercent=40 -XX:G1HeapWastePercent=5 -XX:G1MixedGCCountTarget=4 -XX:InitiatingHeapOccupancyPercent=15 -XX:G1MixedGCLiveThresholdPercent=90 -XX:G1RSetUpdatingPauseTimePercent=5 -XX:SurvivorRatio=32 -XX:MaxTenuringThreshold=1 -XX:ParallelGCThreads=8 -XX:ConcGCThreads=2 -XX:ReservedCodeCacheSize=240m -XX:-DontCompileHugeMethods -XX:+PerfDisableSharedMem -Dfml.ignorePatchDiscrepancies=true -Dfml.ignoreInvalidMinecraftCertificates=true -Dfml.readTimeout=90 -Dcom.mojang.eula.agree=true
```

### ☕ Java 17 服务端参数
```bash
-server -Xms4G -Xmx4G -XX:+UseG1GC -XX:+UseStringDeduplication -XX:+DisableExplicitGC -XX:MaxGCPauseMillis=200 -XX:+ParallelRefProcEnabled -XX:+AlwaysPreTouch -XX:+UseLargePages -XX:G1NewSizePercent=30 -XX:G1MaxNewSizePercent=40 -XX:G1HeapWastePercent=5 -XX:G1MixedGCCountTarget=4 -XX:InitiatingHeapOccupancyPercent=15 -XX:G1MixedGCLiveThresholdPercent=90 -XX:G1RSetUpdatingPauseTimePercent=5 -XX:SurvivorRatio=32 -XX:MaxTenuringThreshold=1 -XX:ParallelGCThreads=8 -XX:ConcGCThreads=2 -XX:ReservedCodeCacheSize=240m -XX:-DontCompileHugeMethods -XX:+PerfDisableSharedMem -Dfml.ignorePatchDiscrepancies=true -Dfml.ignoreInvalidMinecraftCertificates=true -Dfml.readTimeout=90 -Dcom.mojang.eula.agree=true
```

> 🧠 **服务端说明**：`G1NewSizePercent` 与 `G1MaxNewSizePercent` 用于扩大年轻代，减少对象晋升老年代频率，适合 Minecraft 服务端大量临时对象的特性。  
> 添加了 `-Dcom.mojang.eula.agree=true` 以自动同意 EULA，方便开服。

---

## ✅ 推荐参数模板（Recommended Template）
| 环境 | Java 版本 | 内存建议 | 参数特色 |
|------|-----------|----------|----------|
| 客户端 | Java 17 | 4G~8G | 降低暂停时间，使用大页内存，禁用偏向锁 |
| 服务端 | Java 17 | 4G~12G | 提高吞吐量，更大年轻代，稳定 GC |

---

## ⚙️ 参数兼容性提醒（Compatibility Notes）
| 参数（Parameter） | 需要 Java 版本 | 说明 |
|-------------------|----------------|------|
| `-XX:+UseLargePages` / `-XX:+UseLargePagesInMetaspace` | 11+ | 需要在操作系统层面启用大页（Linux `Transparent HugePages` 或 Windows `Lock Pages in Memory`），否则可能被忽略或导致启动失败 |
| `-XX:+UseBiasedLocking` | Java 8 | Java 15 起已废弃，Java 11 中可选关闭 |
| `-XX:+DisableExplicitGC` | 11+ | 替代 Java 8 的 `ExplicitGCInvokesConcurrent` |
| `-XX:+UseStringDeduplication` | 8u20+ | 需要 G1GC 生效 |

---

## 🔧 如何使用（How to Use）

### 官方启动器 / 第三方客户端
在启动器的 **“JVM 参数”** 或 **“Java 虚拟机参数”** 栏中粘贴对应参数，并确保：
- 删除原有的 `-Xmx` 等冲突设置。
- 将 `-Xms` 与 `-Xmx` 修改为适合你电脑的数值。

### 服务端（Server）
将参数添加至启动脚本，例如：
```bash
java @jvm_args.txt -jar server.jar nogui
```
或直接写在命令中（注意引号）。

### 验证参数是否生效
使用 `-Xlog:gc*` 或按 `F3` 在游戏中查看内存分配与 GC 行为。

---

## ⚠️ 重要提醒（Important Reminders）
1. **内存分配**：`-Xms` 与 `-Xmx` 必须相等，避免堆大小动态调整带来的性能抖动。
2. **线程数调整**：`ParallelGCThreads` 和 `ConcGCThreads` 请根据你的 CPU 修改（通常线程数 = 逻辑处理器数）。
3. **大页内存**：Windows 用户需在组策略中授予用户“锁定内存页”权限；Linux 用户建议开启 `Transparent HugePages`。
4. **参数冲突**：请勿混用不同 Java 版本的专属参数，否则可能导致 JVM 拒绝启动。
5. **备份原有参数**：修改前请保存你的原始参数，以便恢复。

---

## 📚 参考文献与工具
- [Aikar's Flags (Minecraft Server)](https://aikar.co/mcflags.html) — 服务端 GC 优化经典方案
- [Oracle G1GC Tuning](https://docs.oracle.com/javase/9/gctuning/garbage-first-garbage-collector-tuning.htm) — G1 调优官方指南
- [Fabric Wiki – JVM Arguments](https://fabricmc.net/wiki/player:tutorials:jvm_args) — Minecraft 社区推荐参数
- [Flags.sh](https://flags.sh) — 交互式 JVM 参数生成器

---

## 👥 贡献与反馈（Contribution & Feedback）
本项目由社区共同维护，欢迎提交 Issue 或 Pull Request 改进参数、适配新版本 Java 或更新说明。  
如果你有更优的参数组合，请附带测试数据（FPS 曲线、GC 日志等）一同提交。

## ⭐ 支持项目
如果这些参数对你的游戏体验有帮助，请**给项目一个 Star**！你的支持是持续更新的动力 🚀
