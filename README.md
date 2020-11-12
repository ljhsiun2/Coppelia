# Coppelia
## Description
This is the repository for the Coppelia tool described in our [MICRO '18](https://cs.unc.edu/~rzhang/files/MICRO2018.pdf) paper.

## Publication
* Rui Zhang, Calvin Deutschbein, Peng Huang, and Cynthia Sturton. 
End-to-End Automated Exploit Generation for Validating the Security of Processor Designs. 
In Proceedings of *the 51st IEEE/ACM International Symposium on Microarchitecture*, MICRO '18.

## Download
```
git clone https://github.com/rzhang2285/Coppelia
cd Coppelia
git submodule update --init --recursive
```

## Installation
### Klee
Please refer to website: [https://klee.github.io/build-llvm9/](https://klee.github.io/build-llvm9/) about 
how to build KLEE.

### Verilator
```
git clone http://git.veripool.org/git/verilator
git checkout verilator_3_900
cd verilator
autoconf
./configure
make
sudo make install
```
For additional information, please refer to website: [http://www.veripool.org/projects/verilator/wiki/Installing](http://www.veripool.org/projects/verilator/wiki/Installing).

Update the Makefile with your own `KLEE_ROOT` and `KLEE_INCLUDE`:

```
vim verilator/verilated.mk
KLEE_ROOT = (use your own klee_root)
KLEE_INCLUDE = (use your own klee_include)
```

Update Verilator's Makefile with Klee and WLLVM:

```
mv /usr/local/share/verilator/include/verilated.mk /usr/local/share/verilator/include/verilated.mk.bak
cp verilator/verilated.mk /usr/local/share/verilator/include
```

## Usage
### Directory Structure

```
.
+-- cores/              # Verilog source
|   +-- or1200/
|   include/            # Basic global defines and contraints using klee_assume
|   one_cycle/          # Testbench for described single-cycle methodology
|   script/              
|   +-- multi.py        # wrapper invoking necessary klee API and file parsing
|   +-- multi/          
|       +-- dissassembler
|       +-- *.py        # python files for generating testbenches (e.g. reset) 
|   +-- tb_cpu.cpp
|   +-- tb_reset.cpp
```

Invoking multi.py to run Coppelia off of the source RTL under $COPPELIA_ROOT/cores
