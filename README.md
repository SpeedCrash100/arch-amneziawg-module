# Arch linux package for building AmneziaWG kernel module


## Warning

This package downloads the kernel source for currently kernel you running. 
It means after you updated kernel, you need to rebuild the package after booted into new kernel.
It also means that if you have multiple kernels, it will build the package for only currently active one.


## ToDo:
 - [ ] Get kernel sources for installed kernels instead running one
 - [ ] DKMS support if possible(Mostly likely is not or not viable)

