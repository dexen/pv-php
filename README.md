# pv - monitor the progress of data through a pipeline

## Description

Monitor progress of transfer of large archives, DB backup/restore, etc.

A pure PHP implementation of the `pv` CLI tool. Useful in case of shared web hostings when you have SSH access, but cannot install packages.

Quoting original `pv`'s manual:
>pv  shows  the  progress of data through a pipeline by giving information such as time elapsed,
>percentage completed (with progress bar),
>current throughput rate, total data transferred, and ETA.

>To use it, insert it in a pipeline between two processes, with the appropriate options.  Its standard input will be passed
>through to its standard output and progress will be shown on standard error.

>pv  will  copy  each  supplied FILE in turn to standard output (- means standard input), or if no FILEs are specified just
>standard input is copied. This is the same behaviour as cat(1).

## Usage

A subset of options of original `pv` is supported. The aim is to eventually become fully compatible.

`-s SIZE` / `--size SIZE` - assume SIZE bytes to be transferred, for purposes of ETA and completion percentage calculation. Supports 'K' / 'M' / 'G' / 'T' suffix to specify larger units (IEC standard - multiplies of 1024).

`-i INTERVAL` / `--interval INTERVAL` - udate display at about INTERVAL seconds. Decimal values are supported. Default: 0.2 seconds.

## Environment

Environment variables influencing the script

`$TERM` - terminal type, influences method of line erase. Supported: `xterm` / `linux` - use `CR`; `dumb`/any other: use multiple ASCII `BS`.

`$COLUMNS` - width of terminal in colums influences output width. Used in case `tput cols` does not return usable information. Fallback value: 80.

## Examples

Restore MySQL backup from a dump file, monitor progress.

```bash
pv < mysql-backup-20201122.sql | mysql -u USER -p MY_DATABASE
```
