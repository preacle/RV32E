# 安装riscv-gnu-toolchain

## clone riscv-gnu-toolchain

```
$ git clone https://github.com/riscv/riscv-gnu-toolchain
$ cd riscv-gnu-toolchain
$ git submodule update --init --recursive
```
## 添加preacle的riscv-next分支
```
$ cd riscv-newlib/
$ git remote add preacle https://github.com/preacle/riscv-newlib
$ git pull preacle
$ git checkout preacle/RVE

$ cd ../riscv-gcc
$ git remote add preacle https://github.com/preacle/riscv-gcc
$ git pull preacle
$ git checkout preacle/RVE

$ cd ../riscv-binutils-gdb
$ git remote add preacle https://github.com/preacle/riscv-binutils-gdb
$ git pull preacle
$ git checkout preacle/RVE
```
## 安装RV32工具链
```
$ cd ..
$ export RISCV=/OPT/RISCV
$ ./configure --prefix=$RISCV --with-arch=rv32e --with-abi=ilp32 
$ make
```
## 安装RV64工具链
```
$ cd ..
$ export RISCV=/OPT/RISCV
$ ./configure --prefix=$RISCV --with-arch=rv64e --with-abi=lp64 
$ make
```

-----------------------------------------------------
# 安装spike

## 安装riscv-fesvr
```
$ git clone https://github.com/riscv/riscv-fesvr.git
$ cd riscv-fesvr
$ mkdir build
$ cd build
$ ../configure --prefix=$RISCV
$ make install
```
## 安装spike
```
$ git clone https://github.com/riscv/riscv-isa-sim.git
$ cd riscv-isa-sim
$ mkdir build
$ cd build
$ ../configure --prefix=$RISCV --with-fesvr=$RISCV
$ make
$ make install
```
## 安装spike pk 

preacle/riscv-pk包含已改动的分支RV32E
```
$ export PATH=$RISCV/bin:$PATH #可能需要的步骤

```

```
$ git clone https://github.com/preacle/riscv-pk.git
$ cd riscv-pk
$ git checkout origin/RV32E 
$ mkdir build
$ cd build
$ ../configure --prefix=$RISCV --host=riscv32-unknown-elf
$ make
$ make install
```

# RV32E使用方法
## 编译
```
$ riscv32-unknown-elf-g++ hello.cpp -o hello
```
## 运行
运行时候需要添加 --isa=RV32
```
$ spike --isa=RV32 pk hello
```
## 获取trace
```
$ spike --isa=RV32 -l pk hello 2> hello.log
```