How to build Linux kernel with clang?
---

1. Download Linux kernel from git
    - ``git clone git://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git``
    - ``cd linux-stable``
    - ``git reset --hard v5.2`` (please update the version as you want such as v4.14. You can find the list of tags with ``git ls-remote --tags origin``)

2. Installation of Clang/LLVM
    - Please download binaries from https://releases.llvm.org/download.html
    - And, add the biniary folder in PATH
    - Please check if clang is properly installed with ``clang --version``

3. Build with clang
    - ``cd linux-stable``
    - Create default config ``make defconfig``. AMDGPU is not supported, so please disable it (if you use defconfig under x86 machine, it is automatically disabled) 
    - ``make CC=clang HOSTCC=clang -j 5``
    - Tested versions
      - Linux kernel-5.3 + clang/llvm-9.0 (Ubuntu 18.04)
      - Linux kernel-4.14 + clang/llvm-3.8 (Ubuntu 18.04)
    
Build Linux kernel with gllvm
---
- The reason for building Linux kernel with [gllvm](https://github.com/SRI-CSL/gllvm) is to retrieve llvm byte code (.bc)

1. Installation of gllvm
    - Please follow the instruction at [gllvm](https://github.com/SRI-CSL/gllvm)

2. After installation of gllvm, follow the above step 2.

3. Build with gllvm
    - ``cd linux-stable``
    - Create default config ``make defconfig``. AMDGPU is not supported, so please disable it (if you use defconfig under x86 machine, it is automatically disabled) 
    - ``make CC=gclang HOSTCC=gclang -j 5``
    - Tested versions
      - Linux kernel-5.3 + clang/llvm-9.0 (Ubuntu 18.04)
      - Linux kernel-4.14 + clang/llvm-3.8 (Ubuntu 18.04)
4. With each object file (.o), run ``get-bc example.o`` to get .bc file, and use ``llvm-dis example.bc`` to get readable byte code (.ll)

References
---
- https://github.com/microsoft/checkedc-clang/wiki/Building-the-Linux-kernel
- https://github.com/ramosian-glider/clang-kernel-build
- https://www.phoronix.com/scan.php?page=article&item=clang-linux-53&num=1
- https://docs.google.com/presentation/d/1vJrsJ7fRSi6uidJWVSI2bg8aR19gXeshLgD0tcXfMqg/edit#slide=id.g47b3de7edd_1_6
