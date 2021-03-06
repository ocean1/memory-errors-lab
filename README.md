Memory Error Primer
===================

Source code and virtual machine that I use for teaching purposes.

Getting Started
---------------

*Step 1:* Clone this repository

    $ git clone https://github.com/ocean1/memory-errors-lab.git

*Step 2:* Install [VirtualBox](https://www.virtualbox.org/) according to your host
operating system's recommended procedure.

*Step 3:* Install Vagrant ([instructions
here](http://www.vagrantup.com/downloads)).

*Step 4:* Start the virtual machine:

    $ cd memory-errors-lab/linux64
    $ cd linux64
    $ vagrant plugin install vagrant-vbguest
    $ vagrant up

If you want to skip the vbguest plugin installation, you'll have to setup
the vbox guest additions yourself after a "vagrant up", you'll then need to halt and start again the machine:

    $ vagrant halt
    $ vagrant up

*Step 5:* Start hacking:

    $ vagrant ssh

    Linux debianstable32bit 3.2.0-4-686-pae #1 SMP Debian 3.2.54-2 i686

    The programs included with the Debian GNU/Linux system are free software;
    the exact distribution terms for each program are described in the
    individual files in /usr/share/doc/*/copyright.

    Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
    permitted by applicable law.
    Last login: Tue Apr 22 03:11:28 2014 from 10.0.2.2

    vagrant@debianstable32bit:~$

GCC Options
-----------

When compiling, the following options are recommended:

    -fno-stack-protector           # disables stack-smashing protection
    -z execstack                   # enables executable stack
    -mpreferred-stack-boundary=2   # aligns memory allocation to 2^2 bytes
    -m32                           # compile as 32-bitx86 elf file

Since the `-mpreferred-stack-boundary=2` option affects how the machine
allocates memory on the stack, it also affects the displacement calculation
when preparing format string exploits. Therefore, disabling this option is
recommended when practicing with format string bugs.
