### Benchmarks Included
- [PARSEC](http://parsec.cs.princeton.edu/)


### PARSEC
This repository incldues sources and patches for building 32-bit of PARSEC-3.0 benchmarks on a 64 bit system for micro-architectural simulations. Simulation inputs are not included in this repository and must be downloaded.

#### Simulation Inputs
Tar archive containing simulation inputs for PARSEC-3.0 is available [here](http://parsec.cs.princeton.edu/download/3.0/parsec-3.0-input-sim.tar.gz). This tar archive does not contain simulation inputs for facesim. Those can be extracted from PARSEC-2.1 simulation inputs archive available [here](http://parsec.cs.princeton.edu/download/2.1/parsec-2.1-sim.tar.gz).


#### Building 32-bit binaries on 64-bit systems
These instruction have been tested on 64-bit Debian Squeeze systems.

- Install debian packages
```
apt-get install make autoconf gcc-multilib g++-multilib
apt-get install pkg-config gettext
apt-get install ia32-libs-dev libx11-dev libxext-dev libxt-dev libxmu-dev libxi-dev
```

- Make a copy of `/bin/uname`
```
mv /bin/uname /bin/uname.orig
```

- Make a wrapper shell script to make uname return `i686` instaed of `x86_64`. Create a new file `/bin/uname` with the following contents:
```
!/bin/sh
/bin/uname.orig $* | sed 's/x86_64/i686/g'
```

- Add execute permissions to `/bin/uname`
```
chmod a+x uname
```

- Change the environment variable ```HOSTTYPE``` to ```i386```
```
export HOSTTYPE=i386
```

- Now PARSEC and SPLASH2X applications can be build using `parsecmgmt` tools
```
./bin/parsecmgmt -a build -p parsec
./bin/parsecmgmt -a build -p splash2x
```

Following applications cannot be build:
- splash2x.ocean_ncp
- splash2x.volrend

#### Docker Builds
A docker file is also provided in repository for building these benchmarks

