# jelly_sentry

STM32H723VGT6 / Cortex-M7 BSP 工程，包含 Core、HAL/CMSIS、USB CDC、CMSIS-DSP 和 User_File 中的驱动、算法及任务代码。

## 在 VS Code 中编译

1. 用“文件 → 打开文件夹”打开整个 `jelly_sentry` 文件夹。
2. 安装推荐的 STM32Cube 和 CMake Tools 扩展。
3. 在 STM32Cube Bundle Manager 中安装下列版本（本机已安装）：
   - CMake `4.4.0+st.1`
   - Ninja `1.13.2+st.1`
   - GNU Tools for STM32 `14.3.1+st.2`
   - ST Arm clangd `21.1.0+st.2`（代码索引）
4. 执行 `CMake: Select Configure Preset`，选择 `Debug` 或 `Release`。
5. 执行 `CMake: Configure`，再执行 `CMake: Build`。

预设使用 Windows 默认 STM32Cube bundle 目录 `%LOCALAPPDATA%/stm32cube/bundles`，显式选择 Ninja 并加入 ARM GCC 路径。编译无需 NMake 或 Visual Studio C++ 工具包。若工具版本或 bundle 安装位置不同，可通过本地 `CMakeUserPresets.json` 继承并覆盖配置。

命令行也可以使用已安装的 CMake（PowerShell）：

```powershell
$stm32Cmake = "$env:LOCALAPPDATA\stm32cube\bundles\cmake\4.4.0+st.1\bin\cmake.exe"
& $stm32Cmake --preset Debug
& $stm32Cmake --build --preset Debug --parallel
```

将 `Debug` 替换为 `Release` 可构建发布版本。输出位于 `build/Debug/` 或 `build/Release/`，包括 `jelly_sentry.elf`、`jelly_sentry.hex`、`jelly_sentry.bin`、链接映射和 `compile_commands.json`。

## CubeMX

硬件配置保留在 `dm02_test.ioc` 中。修改硬件配置后重新生成代码，应保留 User Code 区域及 `CMakeLists.txt` 中的自定义目录和 CMSIS-DSP 链接项。CubeMX 可能重新生成工程名；固件目标名在 `CMakeLists.txt` 的 `project(...)` 中设置。

## 已验证

- GNU ARM GCC 14.3.1、Ninja 1.13.2、CMake 4.4.0。
- Debug 和 Release 均完成全部 94 个编译及链接步骤，生成 ELF、HEX 和 BIN。
- 编译验证不代表已完成实机烧录或外设测试。

保留源码和第三方库中的版权及许可证声明。