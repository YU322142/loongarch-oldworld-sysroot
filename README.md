# LoongArch old-world ABI1.0 development sysroot

中文说明见 [README.zh-CN.md](README.zh-CN.md).

This repository publishes a LoongArch old-world ABI1.0 development sysroot as a GitHub release asset. It is intended for online cross-builds of native libraries used by ClassIsland on Loongnix 20 old-world ABI1.0.

The archive is a build sysroot, not a runnable root filesystem. It contains old-world LoongArch headers and libraries needed by desktop native builds, including fontconfig, FreeType, X11, OpenGL, Vulkan, libc and related development files.

## Current release

```text
Tag: oldworld-dev-sysroot-20260607
Asset: loongarch64-oldworld-dev-sysroot-20260607.tar.xz
SHA256: 5D442178DB80F8C1BC599B5C0E5963071BBBB33270DE05747959ADC65E7BC086
```

Download URL:

```text
https://github.com/YU322142/loongarch-oldworld-sysroot/releases/download/oldworld-dev-sysroot-20260607/loongarch64-oldworld-dev-sysroot-20260607.tar.xz
```

## Usage

```bash
curl -fL -o loongarch64-oldworld-dev-sysroot-20260607.tar.xz \
  https://github.com/YU322142/loongarch-oldworld-sysroot/releases/download/oldworld-dev-sysroot-20260607/loongarch64-oldworld-dev-sysroot-20260607.tar.xz

echo "5D442178DB80F8C1BC599B5C0E5963071BBBB33270DE05747959ADC65E7BC086  loongarch64-oldworld-dev-sysroot-20260607.tar.xz" | sha256sum -c -

mkdir -p sysroot
tar -xf loongarch64-oldworld-dev-sysroot-20260607.tar.xz -C sysroot
```

Then pass `--sysroot=$PWD/sysroot` to the LoongArch old-world cross compiler, and add the matching include and library search paths required by your build system.

## Verification target

- Architecture: `linux-loongarch64`
- ABI: LoongArch old-world ABI1.0, LP64-compatible
- Runtime baseline: glibc 2.28 or older consumers
- Desktop build coverage: fontconfig, FreeType, X11, OpenGL and Vulkan development files

Downstream builds should still verify their final `.so` files with `readelf` and reject symbols newer than the intended GLIBC ceiling.

## Licensing

The files committed directly to this repository, including README and metadata files, are licensed under the MIT License in [LICENSE](LICENSE).

The sysroot archive published as a release asset is an aggregate of third-party software packages. This repository does not relicense those files. Each file inside the extracted sysroot remains governed by its original upstream or distribution package license, and license notices are typically available under paths such as `usr/share/doc` inside the archive.
