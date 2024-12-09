# L4T(BSP) Build Env

## Reference

https://catalog.ngc.nvidia.com/orgs/nvidia/containers/jetpack-linux-aarch64-crosscompile-x86

## Sample build kernel

For build L4T 35.4.1(Jetpack 5.1.2)

1. Pull build env image for Jetpack 5.1.2

    ```sh
    sudo docker pull nvcr.io/nvidia/jetpack-linux-aarch64-crosscompile-x86:5.1.2
    ```

2. Run the container

    ```sh
    docker run -it --privileged --net=host -v /dev/bus/usb:/dev/bus/usb -v ./workspace:/workspace nvcr.io/nvidia/jetpack-linux-aarch64-crosscompile-x86:5.1.2
    ```

3. Extract the targetfs and toolchain

    ```sh
    cd /l4t
    cat targetfs.tbz2.* > targetfs.tbz2
    tar -I lbzip2 -xf targetfs.tbz2
    mkdir toolchain
    tar -C toolchain -xf toolchain.tar.gz
    ```

4. Build L4T public sources(build kernel)

    ```sh
    cd /workspace
    wget https://developer.nvidia.com/downloads/embedded/l4t/r35_release_v4.1/sources/public_sources.tbz2
    tar -xjf public_sources.tbz2
    cd Linux_for_Tegra/source/public
    tar -xjf kernel_src.tbz2
    mkdir kernel_out
    CROSS_COMPILE_AARCH64=/l4t/toolchain/bin/aarch64-buildroot-linux-gnu- CROSS_COMPILE_AARCH64_PATH=/l4t/toolchain NV_TARGET_BOARD=t186ref ./nvbuild.sh -o ${PWD}/kernel_out
    ```

