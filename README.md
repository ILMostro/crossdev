# Gentoo Overlay for Crossdev Packages

See [Gentoo Wiki: AArch64](https://wiki.gentoo.org/wiki/Raspberry_Pi_3_64_bit_Install) for updated information 
about working with cross-platform development for the ARM architecture on a Gentoo system.

See [Gentoo Wiki: Custom_Repos - Crossdev](https://wiki.gentoo.org/wiki/Custom_repository#Crossdev) for updated information about working with overlays for `sys-devel/crossdev`.


The `crossdev` tool is used to facilitate the configuration and environment setup on a Gentoo system for 
cross-platform development.  It can be used, for example, to generate the necessary toolchain 
for compiling code on an x86*-based system that's meant to run on an arm-based system.  The following 
example illustrates such a procedure, where the existing packaging designs of the Gentoo production system 
are utilized to build the toolset needed to create software for the 64-bit `arm` architecture of the raspberry pi 3.

```
crossdev -t aarch64-unknown-linux-gnu
```

That provides the `gcc` cross-compiler, along with other low-level tools like `binutils`.
Environment variables or variable assignments can be easily utilized then to select 
the correct compiler or toolset for the architecture.

For example, as illustrated in the above-referenced Wiki page for Raspi3 on AArch64:

```
ARCH=arm64 CROSS_COMPILE=aarch64-unknown-linux-gnu- make
```


----

#### Default Overlay Targets for crossdev

The `sys-devel/crossdev` package will place the ebuilds/categories it generates into one of the 
following places (overlays) in the order that they are listed.

| Order Number | Short Name       | Description                    |
|-------|------------|--------------------------------|
| 1     | commandline    | The name of an overlay specified on the command-line with the `--ov-output` (`-oO`) option 
| 2     | cross-${CTARGET}   | The name of an overlay in the form of 'cross-${CTARGET}'  |
| 3     | crossdev   | The `crossdev` overlay, if one is created or exists  |
| 4     | Priority   | Finally, it falls back on the overlay with the lowest priority value in `/etc/portage/repos.conf/`  |
| 5     | Alphabetical   | If the priority value of the overlay(s) is the same, it defaults to using the first 
							overlay alphabetically.	|

