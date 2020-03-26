How to get llvm bytecode(.bc) of kernel module with clang?
---

1. Build Linux kernel with gllvm
    - Follow the Build Linux kernel with gllvm at the [instruction page](kernel-build-with-clang.md)

2. This step uses an example
    - Let us have ``hello.c`` file under the directory named ``hello``
    ```c
    #include <linux/init.h>
    #include <linux/module.h>
    #include <linux/kernel.h>

    static int hello_init(void) {
        printk("Hello, world\n");
        return 0;
    }

    static void hello_exit(void) {
        printk("Goodbye, world\n");
    }

    module_init(hello_init);
    module_exit(hello_exit);

    MODULE_LICENSE("Dual BSD/GPL");
    ```
    - Create one Makefile under ``hello`` directory
    ```Makefile
    obj-m   := hello.o
    KDIR    := /path/of/linux/directory/built/with/gllvm
    PWD     := $(shell pwd)

    default:
      $(MAKE) CC=gclang -C $(KDIR) M=$(PWD) modules

    ```
      - KDIR is the path of linux directory built using gllvm
      
    
3. Run ``make`` under ``hello`` directory
