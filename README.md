# MSF-Haskell

## Introduction
This directory contains the Haskell Metasploit binding and library as
well as [a whitepaper](whitepaper/main.pdf) describing the purpose and use of the library.

In brief, the [Metasploit Framework (MSF)](http://www.metasploit.com)
is a widely deployed open
source penetration testing platform. Much of the functionality of the
framework is provided by a remote procedure call (RPC) interface via
the standard HTTP protocol. This is known as the [Metasploit Remote API](https://community.rapid7.com/docs/DOC-1516).

Open source bindings to this API already exist in other programming
languages. This package is a Haskell implementation of this API so
that developers can write Haskell clients that communicate with the
Metasploit server.

In addition to a low-level implementation of the API, we provide
higher level abstractions to improve the safety of Haskell
clients. These abstractions help penetration testers writing Haskell
code to avoid certain errors. For instance, there is compile-time
support to detect if the developer attempted to launch an exploit
against a host that they meant to only port scan. The included
[whitepaper](whitepaper/main.pdf) covers the capabilities of these safety features in more
detail.

This binding was compatible with the MSF API as of early 2013, but has
not been tested on more recent releases.

# Contact
* Isaac Potoczny-Jones <ijones@galois.com> [@SyntaxPolice](https://twitter.com/syntaxpolice)
* Trevor Elliott <trevor@galois.com>

# Directory Contents

In this section, we describe the most important files and directories
contained in this package:

## Documentation

- **whitepaper** - This directory contains [a PDF](whitepaper/main.pdf) and the latex source files
  for the high-level whitepaper describing the system. This whitepaper
  outlines the purpose of the library and explains the types of
  programming errors that can be avoided when using the library. To read
  the whitepaper, view whitepaper/main.pdf in Adobe Acrobat or another
  PDF viewer.

## Code

- **msfHaskell.cabal** - The Haskell Cabal is the standard build system for
  Haskell, similar to tools like Ant for Java. This file is the set of
  build instructions for this package.

- **src** - This directory contains the library source files.

- **src/RPC** - The RPC directory is a low-level implementation of the
  Metasploit Remote API.

- **src/MSF** - The MSF directory is a higher-level implementation of the
  Metasploit Remote API. This builds upon the code in the RPC
  directory. It includes more advanced features like event handling,
  port scanning, and improved type safety.

- **examples** - a directory containing a single example program, which we
  may extend in the future with more examples.

- **examples/ExampleExploit.hs** - This program demonstrates many of the
  features of the API, and uses both the MSF and RPC code. In
  particular, the example instructs Metasploit to perform an nmap
  operation, launch an exploit, and download assets like the /etc/passwd
  files from the target. The exploit in this
  [example](http://www.metasploit.com/modules/exploit/multi/samba/usermap_script) uses an old,
  patched, and publicly known vulnerability ([CVE-2007-2447](http://cvedetails.com/cve/2007-2447/)) that
  is included in the standard open source Metasploit framework.

# Building

The library and examples build using the standard Haskell compilation
system called Cabal. The system requires GHC, Cabal, and some
packages. GHC and Cabal should be installed using your operating
system's package manager (e.g. RPM). The package dependencies will be
automatically downloaded and installed by the Cabal build system. To
build, run "cabal update" and "cabal install" from the top level
directory.
