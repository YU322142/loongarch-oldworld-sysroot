# LoongArch 旧世界 ABI1.0 构建资产

English documentation: [README.md](README.md).

本仓库通过 GitHub Release 发布 LoongArch 旧世界 ABI1.0 构建资产，用于 ClassIsland 等项目在 GitHub Actions 中交叉编译旧世界原生库。

sysroot 压缩包是“构建用 sysroot”，不是可直接启动的根文件系统。它包含旧世界 LoongArch 开发头文件和库，包括 fontconfig、FreeType、X11、OpenGL、Vulkan、libc 以及相关开发文件。

工具链压缩包是与该 sysroot 匹配的 Linux x64 交叉编译工具链。将工具链和 sysroot 一起固定，可以避免误用较新的公开 cross-tools sysroot 或 GCC include-fixed 头文件。

## 当前发布

```text
Tag: oldworld-dev-sysroot-20260607
Asset: loongarch64-oldworld-dev-sysroot-20260607.tar.xz
SHA256: 5D442178DB80F8C1BC599B5C0E5963071BBBB33270DE05747959ADC65E7BC086

Asset: linux-x64-cross-tools-loongarch64-oldworld-gcc14-20260607.tar.xz
SHA256: 78335E5FCE4FDD6505B23734C539304547753FA1887CC199F5EA0C7554ED0185
```

下载地址：

```text
https://github.com/YU322142/loongarch-oldworld-sysroot/releases/download/oldworld-dev-sysroot-20260607/loongarch64-oldworld-dev-sysroot-20260607.tar.xz
https://github.com/YU322142/loongarch-oldworld-sysroot/releases/download/oldworld-dev-sysroot-20260607/linux-x64-cross-tools-loongarch64-oldworld-gcc14-20260607.tar.xz
```

## 使用方式

```bash
curl -fL -o loongarch64-oldworld-dev-sysroot-20260607.tar.xz \
  https://github.com/YU322142/loongarch-oldworld-sysroot/releases/download/oldworld-dev-sysroot-20260607/loongarch64-oldworld-dev-sysroot-20260607.tar.xz
curl -fL -o linux-x64-cross-tools-loongarch64-oldworld-gcc14-20260607.tar.xz \
  https://github.com/YU322142/loongarch-oldworld-sysroot/releases/download/oldworld-dev-sysroot-20260607/linux-x64-cross-tools-loongarch64-oldworld-gcc14-20260607.tar.xz

echo "5D442178DB80F8C1BC599B5C0E5963071BBBB33270DE05747959ADC65E7BC086  loongarch64-oldworld-dev-sysroot-20260607.tar.xz" | sha256sum -c -
echo "78335E5FCE4FDD6505B23734C539304547753FA1887CC199F5EA0C7554ED0185  linux-x64-cross-tools-loongarch64-oldworld-gcc14-20260607.tar.xz" | sha256sum -c -

mkdir -p sysroot
tar -xf loongarch64-oldworld-dev-sysroot-20260607.tar.xz -C sysroot
tar -xf linux-x64-cross-tools-loongarch64-oldworld-gcc14-20260607.tar.xz
```

随后使用 `loongarch64-unknown-linux-gnu/bin/loongarch64-unknown-linux-gnu-gcc` 或 `g++`，并在交叉编译时传入 `--sysroot=$PWD/sysroot`，再按构建系统需要补充 include/lib 搜索路径。

## 验证目标

- 架构：`linux-loongarch64`
- ABI：LoongArch 旧世界 ABI1.0，LP64 兼容
- 运行库基线：面向 glibc 2.28 或更旧消费者
- 桌面构建覆盖：fontconfig、FreeType、X11、OpenGL、Vulkan 开发文件

下游项目仍应对最终生成的 `.so` 使用 `readelf` 做 ABI 检查，并拒绝超过目标 GLIBC 上限的符号版本。

## 许可证

本仓库直接提交的 README、元数据等文件使用 [LICENSE](LICENSE) 中的 MIT License。

Release 中发布的 sysroot 和工具链压缩包是第三方软件包的聚合物。本仓库不会也不能重新授权这些文件；解压后压缩包内的每个文件仍遵循其上游项目或发行版软件包原本的许可证。相关许可证说明通常位于压缩包内的 `usr/share/doc` 等目录。
