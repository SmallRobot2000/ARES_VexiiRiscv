# VexiiRiscv for ARES
To build in root directory run:
```
git submodule sync --recursive
git submodule update --init --recursive

sbt "Test/runMain vexiiriscv.soc.litex.SocGen \
  --xlen=32 \
  --reset-vector=2147483648 \
  --with-supervisor \
  --with-user \
  --with-rvm \
  --with-rva \
  --with-rvf \
  --with-rvc \
  --with-rvZcbm \
  --with-fetch-l1 \
  --with-lsu-l1 \
  --fetch-l1-sets=64 \
  --fetch-l1-ways=2 \
  --fetch-l1-refill-count=2 \
  --fetch-l1-mem-data-width-min=32 \
  --lsu-l1-sets=64 \
  --lsu-l1-ways=2 \
  --lsu-l1-refill-count=2 \
  --lsu-l1-writeback-count=2 \
  --lsu-l1-mem-data-width-min=32 \
  --memory-region=2147483648,536870912,rwxc,m \
  --memory-region=268435456,268435456,rw,p \
  --with-rdtime \
  --with-sstc \
  --pmp-size=4 \
  --with-axilite-xlen \
  --netlist-directory=generated \
  --netlist-name=VexiiSoc"

```
The end product will be in generated/VexiiSoc.v

# VexiiRiscv

VexiiRiscv (Vex2Risc5) is the successor of VexRiscv. Work in progress, here are its currently implemented features :

- RV32/64 I[M][A][F][D][C][S][U][B]
- Up to 5.24 coremark/MHz 2.50 dhystone/MHz
- In-order execution
- early [late-alu]
- single/dual issue (can be asymmetric)
- BTB, GShare, RAS branch prediction
- cacheless fetch/load/store
- Optional I$, D$
- Optional SV32/SV39 MMU
- Can run linux / buildroot / Debian
- Pipeline visualisation in simulation via Konata
- Lock step simulation via RVLS and Spike
- AXI4, Wishbone, Tilelink memory busses (RVA is not available in some configs, see the RTD doc SoC main page)
- ... and many other things

Here is a demonstration of a quad core VexiiRiscv running debian on FPGA : https://youtu.be/dR_jqS13D2c?t=112

Overall the goal is to have a design which can stretch (through configuration) from Cortex M0 up to a Cortex A53 and potentially beyond.

Here is the online documentation : 

- https://spinalhdl.github.io/VexiiRiscv-RTD/master/VexiiRiscv/Introduction/#
- https://spinalhdl.github.io/VexiiRiscv-RTD/master/VexiiRiscv/HowToUse/index.html

Here is the VexiiRiscv's scala doc (auto-generated from the source code) :

- https://spinalhdl.github.io/VexiiRiscv/doc/vexiiriscv/index.html

A roadmap is available here : 

- https://github.com/SpinalHDL/VexiiRiscv/issues/1

# TL;DR Getting started

The quickest way for getting started is to pull the Docker image with all the dependencies installed

Please refer to the self contained tutorial for a comprehensive step by step instruction manual with
screenshots: https://spinalhdl.github.io/VexiiRiscv-RTD/master/VexiiRiscv/Tutorial/index.html

After running the generation you'll find a file named "VexiiRiscv.v" in the root
of the repository folder, which you can drag into your Quartus or whatever.

We decided to not start covering FPGA boards because there's just too many, so it's up to you
to define your pin configuration for your specific FPGA board

If you want to know what else you can do with sbt, please refer to the complete documentation.

# Rebuild the Docker container

In case you wanna rebuild leviathan's Docker container you can run

    docker build . -f docker/Dockerfile -t vexiiriscv --progress=plain
