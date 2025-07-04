# D4Cos
Note:Still under development...

 D4Cos is an UNIX-like kernel written in C, which uses Limine as its default bootloader and boot protocol.

# Building and Running

This guide provides instructions on how to build and run Polaris OS. 

## 1. Prerequisites

*   **Linux Environment:** A Linux environment is required. Windows users can utilize WSL2 without issues.

## 2. Installation of Dependencies

Install the following packages:

*   `make`
*   `xorriso`
*   `bsdtar`

## 3. Building Polaris OS

### 3.1. Clone the Repository

Clone the Polaris OS repository, ensuring to include submodules:

```bash
git clone --recurse-submodules [repository_url]
```

### 3.2. Prepare Userspace

*   **Download Jinx Script:** Navigate to the repository's root and run `make jinx` to download the jinx script, which is used for building  userspace.

    ```bash
    make jinx
    ```

*   **Build Base Userspace:** To build a base system, run `make userspace-base` from the repository's root.

    ```bash
    make userspace-base
    ```

*   **Build Full Userspace:** To build all ported packages, run `make userspace-full` from the repository's root.

    ```bash
    make userspace-full
    ```

### 3.3. Generate ISO Image

Run `make` from the repository's root to generate the ISO image:

```bash
make
```

## 4. Running Polaris OS

It is highly recommended to use QEMU for ease of use. Below is an example command to run Polaris:

```bash
qemu-system-x86_64 -M q35 -m 8192M -cdrom [ISO path] -serial stdio -boot d -smp 4
```

**Note on Memory Allocation:**

Since the entire root filesystem (rootfs) resides in the ramdisk, a minimum of 8 gigabytes of memory is needed for the entire userspace. If you do not have the required memory free, you can use `userspace-base` instead of `userspace-full`.

We intend to move the rootfs to disk in future updates, but for now, you need to allocate a minimum of 8 

