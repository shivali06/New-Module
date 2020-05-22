# New-Module
OS Creating new module 

## Created a hello world module

1. First I have created a demo directory in which my helloworld module will reside.
``` mkdir demo; //this will create a directory name demo. ```
  - ```Cd demo ``` will insert me into the demo directory.
```
#include <linux/module.h>       /* Needed by all modules */
#include <linux/kernel.h>       /* Needed for KERN_INFO */
#include <linux/init.h>         /* Needed for the macros */

static int __init hello_start(void)
{
printk(KERN_INFO "SC_hello module loading...\n"); //it will print
printk(KERN_INFO "Hello world\n"); //
return 0;
}

static void __exit hello_end(void)//exit function
{
	     printk(KERN_INFO " SC_hello module unloading ");//print statement
}

module_init(hello_start); //call the hello start
module_exit(hello_end); //exit the module
```
  - Now we will make a Makefile. This is to tell the compiler that the source files of our new module are in present in the directory.
```
obj-m = sc_hello.o
KVERSION = $(shell uname -r)
all:
        make -C /lib/modules/$(KVERSION)/build M=$(PWD) modules 
clean:
        make -C /lib/modules/$(KVERSION)/build M=$(PWD) clean
```
  - specifies the path for modules and to clean as well.
  - Now ran the command make. make purpose of the make utility is to determine automatically which pieces of a large program need to be recompiled, and issue the commands to recompile them. you can use make with any programming language whose compiler can be run with a shell command.
  
2. Compiled the module, installed it and uninstalled it

  - ```insmod sc_hello.ko ``` it is used to insert the modules in the operating system. And sc_hello.ko we are specifying the module.
  - ``` lsmod | grep modulename ```
  - it will list the running modules.
  - ``` rmmod sc_hello ``` this will remove the module, And uninstall it.
