# Basic Usage

The `ipmctl` utility has many options. A complete list of commands can be shown by executing `ipmctl` with no arguments, `ipmctl help`, or reading the `ipmctl(1)` man page. Running `ipmctl`requires root privileges. `ipmctl` can also be used from UEFI. Namespaces are created using `ipmctl` at UEFI level or the [ndctl utility](https://github.com/sscargal/pmem-docs-ipmctl-user-guide/tree/f25a04768fa69975fc7b10ea1818b460255f1b79/getting-started-guide/what-is-ndctl.md).

Usage:

```text
ipmctl COMMAND [OPTIONS] [TARGETS] [PROPERTIES]
```

Items in square brackets `[..]` are optional. Options, targets, and property values are separated by a pipe `|` meaning "or", and the default value is italicized. Items in parenthesis `(..)` indicate a user supplied value.

`ipmctl` commands include:

* help
* load
* set
* delete
* show
* create
* dump
* start

More information can be shown for each command using the `-verbose` flag, which is helpful for debugging.

A video recorded by Lenovo shows [How to use ipmctl commands to monitor Intel® Optane™ DC Persistent Memory Module health status on Microsoft Windows](https://www.youtube.com/watch?v=pzSsdcfL-vg). It provides an introduction for using ipmctl. The commands are the same on Linux.



