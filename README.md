# Release repository for ultra96-zynqmp

Montavista Software, LLC. release of ultra96-zynqmp. 

How to use:
==========
```
git clone --recursive https://github.com/MontaVista-OpenSourceTechnology/opencgx-xilinx-2.6
cd opencgx-xilinx-2.6
source setup.sh
```
Optionally, you can pass setup.sh a directory name to use instead of the
default "project" as follows:

```
source setup.sh <project directory>
```
Note: If you are running setup.sh under another script, you should execute it
as a shell script:

```
bash setup.sh <project directory>
source <project directory>/setup.sh
```
The kernel sources by default will be checked out locally to the sources
directory. If you would rather have bitbake do the checkout run the following
command prior to sourcing setup.sh:

```
export LOCAL_SOURCES=0
```

After running the top level setup.sh, you are ready to build. When starting
another session, you can source the setup.sh script in the project directory
to get started. This script will automatically source the environment for
the build tools stored under buildtools, and sources the 
poky/oe-init-build-env script.

directory layout:
================
```
opencgx-xilinx-2.6/
       project - bitbake project for the ultra96-zynqmp project build
       buildtools - build tools to provide minimal build requirement for poky builds
       layers - layers for building ultra96-zynqmp project
       setup.sh - project setup script
       bin - various helper applications for setting up and maintaining the release directory
```

Note:
=====
```
To build images such as cgx-complete-image, core-image-minimal for 
zcu106-zynqmp, we need to build pmu-firmware first with zynqmp-pmu as MACHINE type.
Hence the build consists of following steps,

Step 1. Build pmu-firmware using 'bitbake pmu-firmware' command with below settings 
        in conf/local.conf

MACHINE="zynqmp-pmu"
DISTRO="xilinx-standalone"
GCCVERSION="7.%"
TMPDIR="${TOPDIR}/pmutmp"

Step 2. Remove above four lines added in conf/local.conf in Step 1.

Step 3. Build cgx-complete-image using 'bitbake cgx-complete-image' with below 
        setting in conf/local.conf

        MACHINE="zcu106-zynqmp"

```

Verfied machines: ultra96-zynqmp zedboard-zynq7 zcu106-zynqmp
