#### Wojciech's ptpd-builder

This is a quick and dirty set of scripts used for building ptpd on a variety of OSes. It is probably not fit for general distribution but hey, github backup! Very little error checking, inconsistent variable naming, magic values, you name it it's got it. No guarantee, no support, no pain, no gain.

Written some time in 2014 by Wojciech Owczarek for the PTPd project. Licence is BSD clause whatever (clause 3 in fact).

##### Assumptions:

* SSH keys in place: having parallel processes asking for password is, erm, suboptimal
* ssh config has the right username preset
* hostnames are resolvable, etc
* your target OSes can all run the configure script
* you are not a muppet

##### Dependencies:

* bash
* GNU parallel

##### Setting up - it's all in flat files:

* ./settings: included before the build - source directory definition and binary name
* ./configopts: ./configure parameters - can/should be a symlink so it's easy to switch between different configs
* ./buildhosts: list of hostnames to SSH to, one per line, no comment or whitespace removal, so know what you're doing; also a symlink
* ./buildscript: this is what is executed on each host - so any OS (uname) specific stuff should be case'd there

##### Movin' it, doin' it, y'know

* just run ./runbuilds and watch it burn. Most prep work has suppressed output, build scripts only print stderr to console, everything goes int buildlogs/$hostname
* after builds are done, binaries are fetched to binaries/$host/$binaryname.$host

