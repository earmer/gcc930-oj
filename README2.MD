# GCC 9.3.0 Version for OI Purpose

This repository provides a modified version
of Gnu Compiler Collection (GCC) 9.3.0 for OI
and OJ.

We modified these files below:
- gcc/c-family/c-attribs.c: Disable attributes optimize.
- gcc/c-family/c-pragmas.c: Disable pragma optimize.

## How to use

### Compile

**Warning: I just compiled on Ubuntu AMD 64 machine, may not work for other platforms.**

Clone the project to the local machine. Switch the terminal to the root folder of the project. Excute the following commands:

```bash
./contrib/download_prerequisites
# Create a build directory
# Compile the project for C/C++
mkdir build && cd build && \
    ../configure --enable-languages=c,c++ --disable-multilib && \
    make -j$(nproc)
```

If you want to install it in the system, execute the following command:

```bash
# If in Dockerfile or root user, remove sudo
sudo make install
sudo update-alternatives --install /usr/bin/gcc gcc /usr/local/bin/gcc 100 && \
sudo update-alternatives --install /usr/bin/g++ g++ /usr/local/bin/g++ 100
```

### Use

You can validate the installation by creating `test.cpp`:

```cpp
#pragma GCC optimize("O3")
#include <iostream>

int main()
{
    return 0;
}
```

And run the command:

```bash
g++ test.cpp -o test
## The command above should not throw any error
export ONLINE_JUDGE=1
g++ test.cpp -o test
## The command above should throw an error like "%<#pragma GCC optimize%> is not allowed in online judge mode"
```