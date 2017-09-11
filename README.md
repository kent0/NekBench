## NekBench - Scripts for benchmarking Nek5000
### Introduction

This repository contains scripts for benchmarking [Nek5000](https://nek5000.mcs.anl.gov/), a fast and scalable open-source
spectral element solver for CFD in different platforms from normal linux desktop and laptop
machines to super computers at ALCF, NERSC, etc. This is written using bash scripting language
and should run without any problem on any Unix-like operating system which supports bash.

### Setting up the repository

You can clone the git repository directly using `git`:
```bash
git clone https://github.com/thilinarmtb/NekBench.git
```
or you can download the repository as a zip archive by clicking the `clone or download` button
in this page.

### Running benchmarks

Main script used in benchmarking is the ``go.sh`` which can be found on the source root of the
repository. If you run ``./go.sh --help`` or ``go.sh -h``, it will print out a basic help message
describing all the parameters that can be passed into the ``go.sh`` script.

```
go.sh [options]

options:
   -h|--help                   Print this usage information and exit
   -x|--lx1 \"<list>\"         Specify a list of lx1 values for the run
                                 (Mandatory, e.g., \"3 4 5 6\")
   -y|--ly1 \"<list>\"         Specify a list of ly1 values for the run
                                 (Optional, Default: lx1 list)
   -z|--lz1 \"<list>\"         Specify a list of lz1 values for the run
                                 (Optional, Default: lx1 list)
   -e|--lelt \"<list>\"        Specify a list of lelt values for the run
                                 (Mandatory, e.g., \"128 256\")
   -n|--np \"<list>\"          Specify a list of MPI ranks for the run
                                 (Mandatory, e.g., \"2 4 8\")
   -m|--machine \"machine\"    Specify a machine for the run
                                 (Mandatory, e.g., theta, cetus, ..)
   -t|--test \"<list>\"        Specify a list of tests to be run
                                 (Mandatory, e.g., scaling, pingpong,..)
   -c|--case \"case_name\"     Specify a case to be used in benchmarking
                                 (Use the full path of the case, e.g.,
                                   /home/nek_user/cases/box)
```

Below is an example usage of the ``go.sh`` script.

```sh
./go.sh -x "6 7" -e "100 200" -n "4 8" -m "linux" -t "scaling" -c "/home/foo/NekTests/eddy_uv"
```
Once this command is executed, it will create a benchmark run for a scaling study under a
folder named ``runs``. The directory structure will look like follows:

```
.
├── build.sh

├── go.sh
.
.
├── README.md
├── runs
│   └── eddy_uv
│       └── scaling
│           ├── lelt_100
│           │   ├── lx_6
│           │   │   └── eddy_uv
│           │   └── lx_7
│           │       └── eddy_uv
│           └── lelt_200
│               ├── lx_6
│               │   └── eddy_uv
│               └── lx_7
│                   └── eddy_uv
└── scaling.sh
```

### Important notes

### Developer documentation

### Caveats
* Constants in Caps, variables in lowercase
* Case direcotry name and the case name should be the same
* lxd should have an integer expression, otherwise sed fails
