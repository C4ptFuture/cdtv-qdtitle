# Quick and Dirty CDTV Title Generator

This repo contains a shell (POSIX) script that will take a directory on your filesystem and do all the magic that is needed to create a bootable CDTV title ISO out of it.

_Note: This repo does not contain any Commodore or Amiga intellectual property._

![](pics/CDTV%20Quick%20and%20Dirty%20Title%20Generator.jpg)


## Usage
`cdtv-qdtitle` can create CDTV compatible (i.e., bootable) ISO images for you that you can use in WinUAE (and other emulators) or burn to CD so you can use it on real hardware like CD1000, A570 and A690.

You simply stage all the files you want to have on the ISO image in a directory and just point `cdtv-qdtitle` to it.

Usage:

```sh
cdtv-qdtitle  <directory> [iso-filename] [volume-id]
```

E.g.:

```sh
cdtv-qdtitle  my_awesome_cdtv_title [CDTVtitle.iso] [AWESOME]
```

The example above will take all the files in the directory called `my_awesome_cdtv_title` and create a bootable CDTV title ISO image of it, named `CDTVtitle.iso`. The disc will appear on your system with the volume name _AWESOME_, when you mount it.

The first argument is required, the second and third are optional.


## Requirements
The `cdtv-qdtitle` script should work fine on any POSIX system with bash (Linux, MacOS, other UNIX systems).

You also need to have the following tools installed and in your path:

- mkisofs
- curl


## Limitations
This software is NOT a full replacement for the original Commodore software _ISOCD_. It currently does not do any of the I/O speed optimizations that _ISOCD_ can do. It also does not support any CDFS filesystem options besides the bare minimum `TM` option to support the trademark file requirement. If you need any of those features, please use _ISOCD_.

What this software _does_ do however is it allows you to automate the build process of your CDTV title and make it part of your build pipeline, so you can iterate quickly, instead of having to click buttons in a UI for every single damn build. Once you're satisfied with your CDTV title and you need speed optimizations or extra CDFS boot options, you can always author the final release build of your CDTV title in _ISOCD_. But if you're only using your CDTV ISO in emulators (i.e. not on real hardware), the speed optimizations are typically not really any major concern.

Another limitation currently is that this software generates ISOs with upper case only characters for filenames. This is mostly a cosmetic issue, because CDFS is case insensitive. This will probably get fixed in a future version.
 

## FAQ

### Why is this called Quick and Dirty CDTV Title Generator?
Because that's what it is! It was thrown together one morning to satisfy a use case we had on the CDTV Land Discord: Being able to build bootable CDTV ISOs _and_ being able to distribute the actual code itself as part of a project without any copyright issues. This `cdtv-qdtitle` repo does not host any Commodore or Amiga IP, and is freely distributable under the GPLv3 license.

### Will it ever support additional CDFS boot options or optimizations?
Seek optimizations, probably not. The script wouldn't be so quick and dirty anymore ;-) But I can see the benefit of adding support for several CDFS boot options like setting the directory and file cache sizes, because being able to tweak those settings can sometimes make memory hungry applications work on stock CDTV systems with just 1 MB of memory, that would not run on such systems otherwise.

### I'm on Windows. How do I use this?
If you're looking for a way to author CDTV titles and you don't care about being able to run it as part of a script or automation/pipelines, then I would recommend getting hold of _ISOCD_ and running that in WinUAE. There is also a Windows application called [ISOCD-Win](https://github.com/fuseoppl/isocd-win), which is a replacement that runs on Windows and also has a GUI. 

There _are_ ways of running bash scripts on Windows (google for _WSL_ or _Git-bash_), but that's beyond the scope of this document and is not "officially" supported.
