# embed: A tiny embeddable Forth interpreter

| Project   | Embed Forth VM and eForth Image |
| --------- | ------------------------------- |
| Author    | Richard James Howe              |
| Copyright | 2017-2018 Richard James Howe    |
| License   | MIT                             |
| Email     | howe.r.j.89@gmail.com           |

Available at <https://github.com/howerj/embed>

This project contains a tiny virtual machine (VM) optimized to execute 
[Forth][]. It is powerful and well developed enough to be self hosted, 
the VM and Forth interpreter image can be used to recreate a new image from
source (which is in [meta.fth][]). [meta.fth][] contains a more complete
description of the Forth interpreter, the virtual machine (which is only ~200
Lines of C code) and how a Forth "meta-compiler" works.

The virtual machine is available as a library, as well, so it can be
**embedded** into another project, hence the project name. The virtual machine
([embed.c][] and [embed.h][]), the eForth image ([eforth.blk][]), 
and the metacompiler ([meta.fth][]) are all licensed under the [MIT License][].

Feel free to [email me][] about any problems, or [open up an issue on GitHub][].

## Program Operation

To build the project you will need a [C compiler][], and [make][]. The
system should build under [Linux][] and [Windows][] (MinGW). After installing
[make][] and a [C99][] compiler, simply type "make" to build the
Forth virtual machine. An image containing a working Forth
implementation is contained within [eforth.blk][].

Linux:

	./embed eforth.blk

Windows:

	embed.exe eforth.blk

To exit the virtual machine cleanly either type **bye** and then hit
return, or press *CTRL+D* (on Linux) / *CTRL+Z* (on Windows) and then return.

The source code for [eforth.blk][] is provided in [meta.fth][], which contains
an explanation on how a Forth cross compiler works (know as a *metacompiler* in
Forth terminology) as well as a specification for the virtual machine and a
little about [Forth][] itself.

If you do not have a copy of [make][], but do have a [C99][] compiler, the
following command should build the project:

	cc -std=c99 -DUSE_EMBED_MAIN embed.c -o embed

Generating a new image is easy as well:

	./embed eforth.blk new.blk meta.fth

We can then use the new image to generate a further image:

	./embed new.blk new2.blk meta.fth

Ad infinitum, the two newly generated images should be byte for byte equal
([eforth.blk][] may differ as the latest image might not be checked in).

Unit tests can be ran typing:

	make tests                           # Using make
	./embed eforth.blk unit.blk unit.fth # manual invocation

## Project Organization

* [embed.c][]: The Embed Virtual Machine
* [embed.h][]: The Embed Virtual Machine library interface
* [eforth.blk][]: A Forth interpreter image
* [meta.fth][]: A meta compiler and a Forth interpreter
* [unit.fth][]: Unit tests for the eForth image

[MIT License]: LICENSE
[embed.c]: embed.c
[embed.h]: embed.h
[eforth.blk]: eforth.blk
[unit.fth]: unit.fth
[meta.fth]: meta.fth
[C compiler]: https://gcc.gnu.org/
[make]: https://www.gnu.org/software/make/
[Windows]: https://en.wikipedia.org/wiki/Microsoft_Windows
[Linux]: https://en.wikipedia.org/wiki/Linux
[C99]: https://en.wikipedia.org/wiki/C99
[forth]: https://en.wikipedia.org/wiki/Forth_(programming_language)
[open up an issue on GitHub]: https://github.com/howerj/embed/issues
[email me]: mailto:howe.r.j.89@gmail.com
