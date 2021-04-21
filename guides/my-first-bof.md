---
description: A very old guide I found one of my HDD's
---

# My First BoF

## Creating your first buffer overflow

In a 32 bit Kali installation open a terminal and type the following command and set the value to 0

```text
sudo nano /proc/sys/kernel/randomize_va_space
```

This will turn off ASLR  on the system \(this is a protection against buffer overflows\)

Next type

```text
nano overflow.c
```

And copy the following vulnerable code into the text box.

```text
#include <stdio.h>
main() {
            char *name;
            char *dangerous_system_command;
            name = (char *) malloc(10);
            dangerous_system_command = (char *) malloc(128);
            printf("Address of name is %d\n", name);
            printf("Address of command is %d\n", dangerous_system_command);
            sprintf(dangerous_system_command, "echo %s", "hello world!");
            printf("whats your name?");
            gets(name);
            system(dangerous_system_command);
}
```

This code is written in C and essentially it creates 2 variables name and dangerous\_system\_command it then allocates a memory buffer for each variable. The next 2 print statements print out the address in memory. The program will then ask for your name, it uses the vulnerable command “gets” \(which does not sanitise input\). If the input is of correct size the program will print out “hello world” lets do this now.

type:

```text
./overflow
```

to run the program and look at the memory addresses. you should be able to count the difference between them.

![](../.gitbook/assets/image%20%281%29.png)

In my example the difference is 28250160 - 28250128 = 32. This means that any input of 32 characters or less the program will accept as a valid input, however anything over this then the program will not know how to handle it. lets try this now with some inputs.![](file:///C:/Users/gordo/AppData/Local/Packages/oice_16_974fa576_32c1d314_21ce/AC/Temp/msohtmlclip1/01/clip_image004.gif)

![](../.gitbook/assets/image%20%282%29.png)

As you can see, with a valid input we get the expected output “hello world!”![](file:///C:/Users/gordo/AppData/Local/Packages/oice_16_974fa576_32c1d314_21ce/AC/Temp/msohtmlclip1/01/clip_image006.gif)

If we enter a string that is greater than 32 characters we see that we get an error message that looks like the shell command “r” can not be found. The letter “r” is the 33rd character of the input.

![](../.gitbook/assets/image%20%283%29.png)

So if we know the program has a 32 length buffer and that if we overflow the name variable of 32 bytes we end up in a command variable, why not forge a command at the end of our buffer overflow. To do this we would need a string of 32bit length and a command at the end of it. like so:

```text
12345678901234567890123456789012cat /etc/passwd
```

The command cat /etc/password is the command we are trying to inject which will read the linux file system password file.![](file:///C:/Users/gordo/AppData/Local/Packages/oice_16_974fa576_32c1d314_21ce/AC/Temp/msohtmlclip1/01/clip_image008.gif)

![](../.gitbook/assets/image%20%284%29.png)

