# Patchfiles

## ◆ For fix L4T35.4.1 cpu bug

There is a bug in L4T35.4.1 that causes the CPU usage to be 100%.

Input following commands and apply patch before build kernel, you can avoid this bug.

```sh
cp patches/fix_L4T3541_cpu_bug.patch Linux_for_Tegra/source/public
cd Linux_for_Tegra/source/public
patch -u kernel/nvidia/drivers/media/platform/tegra/camera/vi/vi5_fops.c < patches/fix_L4T3541_cpu_bug.patch
```