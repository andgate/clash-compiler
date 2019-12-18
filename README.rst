Clash - A functional hardware description language
==================================================

|Hackage| |Hackage Dependencies| |Docs| |Pipeline status|

.. |Hackage| image:: https://img.shields.io/hackage/v/clash-ghc.svg
   :target: https://hackage.haskell.org/package/clash-ghc
   :alt: Hackage Release Version

.. |Hackage Dependencies| image:: https://img.shields.io/hackage-deps/v/clash-ghc.svg?style=flat
   :target: https://packdeps.haskellers.com/feed?needle=exact%3Aclash-ghc
   :alt: Hackage Dependency Freshness

.. |Pipeline status| image:: https://gitlab.com/clash-lang/clash-compiler/badges/master/pipeline.svg
   :target: https://gitlab.com/clash-lang/clash-compiler/commits/master
   :alt: CI Pipeline Status

.. |Docs| image:: https://readthedocs.org/projects/clash-lang/badge/?version=latest
   :target: https://clash-lang.readthedocs.io/en/latest/?badge=latest
   :alt: Documentation Status

Clash is a functional hardware description language that borrows both
its syntax and semantics from the functional programming language
Haskell. The Clash compiler transforms these high-level descriptions to
low-level synthesizable VHDL, Verilog, or SystemVerilog.

Features of Clash:

-  Strongly typed, but with a very high degree of type inference,
   enabling both safe and fast prototyping using concise descriptions.

-  Interactive REPL: load your designs in an interpreter and easily test
   all your component without needing to setup a test bench.

-  Higher-order functions, with type inference, result in designs that
   are fully parametric by default.

-  Synchronous sequential circuit design based on streams of values,
   called ``Signal``\ s, lead to natural descriptions of feedback loops.

-  Support for multiple clock domains, with type safe clock domain
   crossing.

Community
=========

**Mailing list**: for updates and questions join the mailing list
clash-language+subscribe@googlegroups.com or read the
`forum <https://groups.google.com/d/forum/clash-language>`__

**Slack**: Invite yourself at
`fpchat-invite.herokuapp.com <https://fpchat-invite.herokuapp.com/>`__.
To join #clash, click on “Channels” and search for “clash”.

**IRC**:
`freenode#clash-lang <https://webchat.freenode.net/#clash-lang>`__

.. install_start

Installing Clash
================

Installing via Snap
-------------------

Clash is released as a binary package on snapcraft. Snap is supported on
all major Linux distributions. Visit `Clash’s snapcraft
page <https://snapcraft.io/clash>`__, scroll down, and choose your
distribution for installation instructions. To install the latest stable
version, use:

.. code:: bash

   snap install clash

To install the latest development version of Clash, run:

.. code:: bash

   snap install clash --edge

This version is updated every 24 hours.

Installing via Source (Linux / MacOS)
-------------------------------------

Install the `latest nix <https://nixos.org/nix/download.html>`__ and
run:

.. code:: bash

   curl -s -L https://github.com/clash-lang/clash-compiler/archive/1.0.tar.gz | tar xz
   nix-shell clash-compiler-1.0/shell.nix

See the `releases
page <https://github.com/clash-lang/clash-compiler/releases>`__ for all
available versions of the compiler.

Installing via Source (Windows)
-------------------------------

1. Install `GHC
   Platform <https://www.haskell.org/platform/windows.html>`__. Make
   sure to install Stack along with it.
2. Download the source code of `Clash
   1.0 <https://github.com/clash-lang/clash-compiler/archive/1.0.tar.gz>`__
3. Unpack the archive
4. Use cd to navigate to the unpacked directory
5. Run ``stack build clash-ghc``. **This will take a while.**

See the `releases
page <https://github.com/clash-lang/clash-compiler/releases>`__ for all
available versions of the compiler.

Installing via Source (HEAD)
----------------------------

Clone Clash from github using ``git`` and enter the cloned directory:

.. code:: bash

   git clone https://github.com/clash-lang/clash-compiler.git
   cd clash-compiler

Use one of the build tools below to get Clash up and running.

Cabal
~~~~~

Install Cabal >= 2.4 and GHC >= 8.4. Even though GHC 8.6 is supported,
we currently recommend running 8.4 as the former contains some known
bugs concerning documentation generation. If you’re using Ubuntu, add
`HVR’s PPA <https://launchpad.net/~hvr/+archive/ubuntu/ghc>`__ and
install them using APT:

.. code:: bash

   sudo add-apt-repository -u ppa:hvr/ghc
   sudo apt install ghc-8.4.4 cabal-install-2.4

Add ``/opt/ghc/bin`` `to your
PATH <https://askubuntu.com/questions/60218/how-to-add-a-directory-to-the-path>`__.
Finally, run Clash using ``cabal``:

.. code:: bash

   cabal new-run --write-ghc-environment-files=always -- clash

Stack
~~~~~

You can use
`Stack <https://docs.haskellstack.org/en/stable/install_and_upgrade/>`__
to build and run Clash too:

.. code:: bash

   stack run -- clash

Nix
~~~

Or `use Nix <https://nixos.org/nix/download.html>`__ to get a shell with
the ``clash`` and ``clashi`` binaries on your PATH:

.. code:: bash

   nix-shell

.. install_end

