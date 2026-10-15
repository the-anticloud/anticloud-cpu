# CPU

> Anticloud offline package — upstream: u-root/cpu @ `main`.

## What This Project Does

cpu command in Go, inspired by the Plan 9 cpu command

**Topics:** cpu, golang, plan9

## Upstream README

# cpu

[![CircleCI](https://circleci.com/gh/u-root/cpu.svg?style=svg)](https://circleci.com/gh/u-root/cpu)
[![Go Report Card](https://goreportcard.com/badge/github.com/u-root/cpu)](https://goreportcard.com/report/github.com/u-root/cpu)
[![CodeQL](https://github.com/u-root/cpu/workflows/CodeQL/badge.svg)](https://github.com/u-root/cpu/actions?query=workflow%3ACodeQL)
[![GoDoc](https://godoc.org/github.com/u-root/cpu?status.svg)](https://godoc.org/github.com/u-root/cpu)
[![License](https://img.shields.io/badge/License-BSD%203--Clause-blue.svg)](https://github.com/u-root/cpu/blob/master/LICENSE)

This repo is an implementation the Plan 9 cpu command, both client and server, for Linux.
More detail is available in the [CPU chapter of the LinuxBoot book](https://book.linuxboot.org/utilities/cpu.html).
Unlike the Plan 9 command, this version uses the ssh protocol for the underlying transport. It includes
features familiar to ssh users, such as support for the ssh config file.

## Overview
The cpu command
lets you log in from a local system to a remote system and see some or all of the files (how much is
up to you) from the local system.

This is wonderfully convenient for embedded systems programmers. Because some or all the files
can come from your local machine, including binaries, the only thing you need installed
on the remote machine is the cpu daemon itself.

### Motivation
Consider the case of running a
complex Python program on an embedded system.
We will need to either do a full install of some distro on that system, meaning we
need USB ports and local storage; or we will need to run the program over the
network.

Installing distros can turn into a mess. Some programs only work under specific distros.
In some cases, when two programs are needed in a pipeline, it can happen that they only work
under different distros!
Users are left juggling USB sticks and NVME cards, and this fails the first time there are
two programs which need two different distros.

Running over a network is usually done with ssh, but ssh can not supply the programs and files.
We would need to either set up a network file system, meaning
finding a sysadmin willing to set it up, and keep it working; or, trying to figure out which
files the program needs, and using rsync or scp to get them there. In some cases,
the target system might not have enough memory to hold those files!

Cpu looks like ssh, but with an important difference: it also provides a file transport
so that the files your program needs are available via a 9p mount. For example, if I have an
embedded system named camera, and I need to read the flash with the flashrom command, I simply type:

```
cpu camera flashrom -r rom.img
```

<img alt="IP camera robots" src="doc/img/ip-camera-robot.jpg" height="240px" />

Breaking this down: cpu is the cpu command; camera is the host name; flashrom is the command
to run; the options are to do a read (-r) into a file called rom.img.

Where does that file end up? In whatever

## License

Upstream terms preserved in `THIRD_PARTY_LICENSES/`. Overlay licensed under Anticommons 0.1.0.

## Verification

Recompute the SHA3-256 of `BENCH.json` and compare to this package’s register. Any drift = invalid package.
