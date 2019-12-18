Changelog for the Clash project
===============================

1.1.0
-----

-  New features (API):

   -  ``Clash.Class.Parity`` type class replaces Prelude ``odd`` and
      ``even`` functions due to assumptions that don’t hold for Clash
      specific numerical types, see
      `#970 <https://github.com/clash-lang/clash-compiler/pull/970>`__.
   -  ``NFDataX.ensureSpine``, see
      `#748 <https://github.com/clash-lang/clash-compiler/pull/803>`__
   -  ``makeTopEntity`` Template Haskell function for generating
      TopEntity annotations intended to cover the majority of use cases.
      Generation failures should either result in an explicit error, or
      a valid annotation of an empty ``PortProduct``. Any discrepancy
      between the *shape* of generated annotations and the *shape* of
      the Clash compiler is a bug. See
      `#795 <https://github.com/clash-lang/clash-compiler/pull/795>`__.
      Known limitations:

      -  Type application (excluding ``Signal``\ s and ``:::``) is best
         effort:
      -  Data types with type parameters will work if the generator can
         discover a single relevant constructor after attempting type
         application.
      -  Arbitrary explicit clock/reset/enables are supported, but only
         a single ``HiddenClockResetEnable`` constraint is supported.
      -  Data/type family support is best effort.

   -  Added ``Bundle ((f :*: g) a)`` instance
   -  Added ``NFDataX CUShort`` instance
   -  Clash’s internal type family solver now recognizes
      ``AppendSymbol`` and ``CmpSymbol``
   -  Added ``Clash.Magic.suffixNameFromNat``: can be used in cases
      where ``suffixName`` is too slow
   -  Added ``Clash.Class.AutoReg``. Improves the chances of synthesis
      tools inferring clock-gated registers, when used. See
      `#873 <https://github.com/clash-lang/clash-compiler/pull/873>`__.
   -  ``Clash.Magic.suffixNameP``, ``Clash.Magic.suffixNameFromNatP``:
      enable prefixing of name suffixes
   -  Added ``Clash.Magic.noDeDup``: can be used to instruct Clash to
      /not/ share a function between multiple branches
   -  A ``BitPack a`` constraint now implies a ``KnownNat (BitSize a)``
      constraint, so you won’t have to add it manually anymore. See
      `#942 <https://github.com/clash-lang/clash-compiler/pull/942>`__.

-  New internal features:

   -  `#918 <https://github.com/clash-lang/clash-compiler/pull/935>`__:
      Add X-Optimization to normalization passes
      (-fclash-aggressive-x-optimization)
   -  `#821 <https://github.com/clash-lang/clash-compiler/pull/821>`__:
      Add ``DebugTry``: print name of all tried transformations, even if
      they didn’t succeed
   -  `#856 <https://github.com/clash-lang/clash-compiler/pull/856>`__:
      Add ``-fclash-debug-transformations``: only print debug info for
      specific transformations
   -  `#911 <https://github.com/clash-lang/clash-compiler/pull/911>`__:
      Add ‘RenderVoid’ option to blackboxes

-  Fixes issues:

   -  `#974 <https://github.com/clash-lang/clash-compiler/issues/974>`__:
      Fix indirect shadowing in ``reduceNonRepPrim``
   -  `#964 <https://github.com/clash-lang/clash-compiler/issues/964>`__:
      SaturatingNum instance of ``Index`` now behaves correctly when the
      size of the index overflows an ``Int``.
   -  `#810 <https://github.com/clash-lang/clash-compiler/issues/810>`__:
      Verilog backend now correctly specifies type of ``BitVector 1``
   -  `#811 <https://github.com/clash-lang/clash-compiler/issues/811>`__:
      Improve module load behavior in clashi
   -  `#439 <https://github.com/clash-lang/clash-compiler/issues/439>`__:
      Template Haskell splices and TopEntity annotations can now be used
      in clashi
   -  `#662 <https://github.com/clash-lang/clash-compiler/issues/662>`__:
      Clash will now constant specialize partially constant constructs
   -  `#700 <https://github.com/clash-lang/clash-compiler/issues/700>`__:
      Check work content of expression in cast before warning users.
      Should eliminate a lot of (superfluous) warnings about
      “specializing on non work-free cast”s.
   -  `#837 <https://github.com/clash-lang/clash-compiler/issues/837>`__:
      Blackboxes will now report clearer error messages if they’re given
      unexpected arguments.
   -  `#869 <https://github.com/clash-lang/clash-compiler/issues/869>`__:
      PLL is no longer duplicated in Blinker.hs example
   -  `#749 <https://github.com/clash-lang/clash-compiler/issues/749>`__:
      Clash’s dependencies now all work with GHC 8.8, allowing
      ``clash-{prelude,lib,ghc}`` to be compiled from Hackage soon.
   -  `#871 <https://github.com/clash-lang/clash-compiler/issues/871>`__:
      RTree Bundle instance is now properly lazy
   -  `#895 <https://github.com/clash-lang/clash-compiler/issues/895>`__:
      VHDL type error when generating
      ``Maybe (Vec 2 (Signed 8), Index 1)``
   -  `#880 <https://github.com/clash-lang/clash-compiler/issues/880>`__:
      Custom bit representations can now be used on product types too
   -  `#976 <https://github.com/clash-lang/clash-compiler/issues/976>`__:
      Prevent shadowing in Clash’s core evaluator

-  Fixes without issue reports:

   -  Fix bug in ``rnfX`` defined for ``Down``
      (`baef30e <https://github.com/clash-lang/clash-compiler/commit/baef30eae03dc02ba847ffbb8fae7f365c5287c2>`__)
   -  Render numbers inside gensym
      (`bc76f0f <https://github.com/clash-lang/clash-compiler/commit/bc76f0f1934fd6e6ed9c33bcf950dae21e2f7903>`__)
   -  Report blackbox name when encountering an error in ‘setSym’
      (`#858 <https://github.com/clash-lang/clash-compiler/pull/858>`__)
   -  Fix blackbox issues causing Clash to generate invalid HDL
      (`#865 <https://github.com/clash-lang/clash-compiler/pull/865>`__)
   -  Treat types with a zero-width custom bit representation like other
      zero-width constructs
      (`#874 <https://github.com/clash-lang/clash-compiler/pull/874>`__)
   -  TH code for auto deriving bit representations now produces nicer
      error messages
      (`7190793 <https://github.com/clash-lang/clash-compiler/commit/7190793928545f85157f9b8d4b8ec2edb2cd8a26>`__)
   -  Adds ‘–enable-shared-executables’ for nix builds; this should make
      Clash run *much* faster
      (`#894 <https://github.com/clash-lang/clash-compiler/pull/894>`__)
   -  Custom bit representations can now mark fields as zero-width
      without crashing the compiler
      (`#898 <https://github.com/clash-lang/clash-compiler/pull/898>`__)
   -  Throw an error if there’s data left to parse after successfully
      parsing a valid JSON construct
      (`#904 <https://github.com/clash-lang/clash-compiler/pull/904>`__)
   -  ``Data.gfoldl`` is now manually implemented, in turn fixing issues
      with ``gshow``
      (`#933 <https://github.com/clash-lang/clash-compiler/pull/933>`__)
   -  Fix a number of issues with blackbox implementations
      (`#934 <https://github.com/clash-lang/clash-compiler/pull/934>`__)

-  Deprecations & removals:

   -  Removed support for GHC 8.2
      (`#842 <https://github.com/clash-lang/clash-compiler/pull/842>`__)
   -  Removed support for older cabal versions, only Cabal >=2.2
      supported
      (`#851 <https://github.com/clash-lang/clash-compiler/pull/851>`__)
   -  Reset and Enable constructors are now only exported from
      Clash.Signal.Internal

1.0.0 *September 3rd 2019*
--------------------------

-  10x - 50x faster compile times
-  New features:

   -  API changes: check the migration guide at the end of
      ``Clash.Tutorial``
   -  All memory elements now have an (implicit) enable line; “Gated”
      clocks have been removed as the clock wasn’t actually gated, but
      implemented as an enable line.
   -  Circuit domains are now configurable in:

      -  (old) The clock period

      -  (new) Clock edge on which memory elements latch their inputs
         (rising edge or falling edge)

      -  (new) Whether the reset port of a memory element is level
         sensitive (asynchronous reset) or edge sensitive (synchronous
         reset)

      -  (new) Whether the reset port of a memory element is active-high
         or active-low (negated reset)

      -  (new) Whether memory element power on in a configurable/defined
         state (common on FPGAs) or in an undefined state (ASICs)

      -  See the `blog
         post <https://clash-lang.org/blog/0005-synthesis-domain/>`__ on
         this new feature

   -  Data types can now be given custom bit-representations:
      http://hackage.haskell.org/package/clash-prelude/docs/Clash-Annotations-BitRepresentation.html
   -  Annotate expressions with attributes that persist in the generated
      HDL, e.g. synthesis directives:
      http://hackage.haskell.org/package/clash-prelude/docs/Clash-Annotations-SynthesisAttributes.html
   -  Control (System)Verilog module instance, and VHDL entity
      instantiation names in generated code:
      http://hackage.haskell.org/package/clash-prelude/docs/Clash-Magic.html
   -  Much improved infrastructure for handling of unknown values:
      defined spine, but unknown leafs:
      http://hackage.haskell.org/package/clash-prelude/docs/Clash-XException.html#t:NFDataX
   -  Experimental: Multiple hidden clocks. Can be enabled by compiling
      ``clash-prelude`` with ``-fmultiple-hidden``
   -  Experimental: Limited GADT support (pattern matching on vectors,
      or custom GADTs as longs as their usage can be statically removed;
      no support of recursive GADTs)
   -  Experimental: Use regular Haskell functions to generate HDL black
      boxes for primitives (in an addition to existing string templates
      for HDL black boxes) See for example:
      http://hackage.haskell.org/package/clash-lib/docs/Clash-Primitives-Intel-ClockGen.html

-  Fixes issues:

   -  `#316 <https://github.com/clash-lang/clash-compiler/issues/316>`__
   -  `#319 <https://github.com/clash-lang/clash-compiler/issues/319>`__
   -  `#323 <https://github.com/clash-lang/clash-compiler/issues/323>`__
   -  `#324 <https://github.com/clash-lang/clash-compiler/issues/324>`__
   -  `#329 <https://github.com/clash-lang/clash-compiler/issues/329>`__
   -  `#331 <https://github.com/clash-lang/clash-compiler/issues/331>`__
   -  `#332 <https://github.com/clash-lang/clash-compiler/issues/332>`__
   -  `#335 <https://github.com/clash-lang/clash-compiler/issues/335>`__
   -  `#348 <https://github.com/clash-lang/clash-compiler/issues/348>`__
   -  `#349 <https://github.com/clash-lang/clash-compiler/issues/349>`__
   -  `#350 <https://github.com/clash-lang/clash-compiler/issues/350>`__
   -  `#351 <https://github.com/clash-lang/clash-compiler/issues/351>`__
   -  `#352 <https://github.com/clash-lang/clash-compiler/issues/352>`__
   -  `#353 <https://github.com/clash-lang/clash-compiler/issues/353>`__
   -  `#358 <https://github.com/clash-lang/clash-compiler/issues/358>`__
   -  `#359 <https://github.com/clash-lang/clash-compiler/issues/359>`__
   -  `#363 <https://github.com/clash-lang/clash-compiler/issues/363>`__
   -  `#364 <https://github.com/clash-lang/clash-compiler/issues/364>`__
   -  `#365 <https://github.com/clash-lang/clash-compiler/issues/365>`__
   -  `#371 <https://github.com/clash-lang/clash-compiler/issues/371>`__
   -  `#372 <https://github.com/clash-lang/clash-compiler/issues/372>`__
   -  `#373 <https://github.com/clash-lang/clash-compiler/issues/373>`__
   -  `#378 <https://github.com/clash-lang/clash-compiler/issues/378>`__
   -  `#380 <https://github.com/clash-lang/clash-compiler/issues/380>`__
   -  `#381 <https://github.com/clash-lang/clash-compiler/issues/381>`__
   -  `#382 <https://github.com/clash-lang/clash-compiler/issues/382>`__
   -  `#383 <https://github.com/clash-lang/clash-compiler/issues/383>`__
   -  `#387 <https://github.com/clash-lang/clash-compiler/issues/387>`__
   -  `#393 <https://github.com/clash-lang/clash-compiler/issues/393>`__
   -  `#396 <https://github.com/clash-lang/clash-compiler/issues/396>`__
   -  `#398 <https://github.com/clash-lang/clash-compiler/issues/398>`__
   -  `#399 <https://github.com/clash-lang/clash-compiler/issues/399>`__
   -  `#401 <https://github.com/clash-lang/clash-compiler/issues/401>`__
   -  `#403 <https://github.com/clash-lang/clash-compiler/issues/403>`__
   -  `#407 <https://github.com/clash-lang/clash-compiler/issues/407>`__
   -  `#412 <https://github.com/clash-lang/clash-compiler/issues/412>`__
   -  `#413 <https://github.com/clash-lang/clash-compiler/issues/413>`__
   -  `#420 <https://github.com/clash-lang/clash-compiler/issues/420>`__
   -  `#422 <https://github.com/clash-lang/clash-compiler/issues/422>`__
   -  `#423 <https://github.com/clash-lang/clash-compiler/issues/423>`__
   -  `#424 <https://github.com/clash-lang/clash-compiler/issues/424>`__
   -  `#438 <https://github.com/clash-lang/clash-compiler/issues/438>`__
   -  `#450 <https://github.com/clash-lang/clash-compiler/issues/450>`__
   -  `#452 <https://github.com/clash-lang/clash-compiler/issues/452>`__
   -  `#455 <https://github.com/clash-lang/clash-compiler/issues/455>`__
   -  `#460 <https://github.com/clash-lang/clash-compiler/issues/460>`__
   -  `#461 <https://github.com/clash-lang/clash-compiler/issues/461>`__
   -  `#463 <https://github.com/clash-lang/clash-compiler/issues/463>`__
   -  `#468 <https://github.com/clash-lang/clash-compiler/issues/468>`__
   -  `#475 <https://github.com/clash-lang/clash-compiler/issues/475>`__
   -  `#476 <https://github.com/clash-lang/clash-compiler/issues/476>`__
   -  `#500 <https://github.com/clash-lang/clash-compiler/issues/500>`__
   -  `#507 <https://github.com/clash-lang/clash-compiler/issues/507>`__
   -  `#512 <https://github.com/clash-lang/clash-compiler/issues/512>`__
   -  `#516 <https://github.com/clash-lang/clash-compiler/issues/516>`__
   -  `#517 <https://github.com/clash-lang/clash-compiler/issues/517>`__
   -  `#526 <https://github.com/clash-lang/clash-compiler/issues/526>`__
   -  `#556 <https://github.com/clash-lang/clash-compiler/issues/556>`__
   -  `#560 <https://github.com/clash-lang/clash-compiler/issues/560>`__
   -  `#566 <https://github.com/clash-lang/clash-compiler/issues/566>`__
   -  `#567 <https://github.com/clash-lang/clash-compiler/issues/567>`__
   -  `#569 <https://github.com/clash-lang/clash-compiler/issues/569>`__
   -  `#573 <https://github.com/clash-lang/clash-compiler/issues/573>`__
   -  `#575 <https://github.com/clash-lang/clash-compiler/issues/575>`__
   -  `#581 <https://github.com/clash-lang/clash-compiler/issues/581>`__
   -  `#582 <https://github.com/clash-lang/clash-compiler/issues/582>`__
   -  `#586 <https://github.com/clash-lang/clash-compiler/issues/586>`__
   -  `#588 <https://github.com/clash-lang/clash-compiler/issues/588>`__
   -  `#591 <https://github.com/clash-lang/clash-compiler/issues/591>`__
   -  `#596 <https://github.com/clash-lang/clash-compiler/issues/596>`__
   -  `#601 <https://github.com/clash-lang/clash-compiler/issues/601>`__
   -  `#607 <https://github.com/clash-lang/clash-compiler/issues/607>`__
   -  `#629 <https://github.com/clash-lang/clash-compiler/issues/629>`__
   -  `#637 <https://github.com/clash-lang/clash-compiler/issues/637>`__
   -  `#644 <https://github.com/clash-lang/clash-compiler/issues/644>`__
   -  `#647 <https://github.com/clash-lang/clash-compiler/issues/647>`__
   -  `#661 <https://github.com/clash-lang/clash-compiler/issues/661>`__
   -  `#668 <https://github.com/clash-lang/clash-compiler/issues/668>`__
   -  `#677 <https://github.com/clash-lang/clash-compiler/issues/677>`__
   -  `#678 <https://github.com/clash-lang/clash-compiler/issues/678>`__
   -  `#682 <https://github.com/clash-lang/clash-compiler/issues/682>`__
   -  `#691 <https://github.com/clash-lang/clash-compiler/issues/691>`__
   -  `#703 <https://github.com/clash-lang/clash-compiler/issues/703>`__
   -  `#713 <https://github.com/clash-lang/clash-compiler/issues/713>`__
   -  `#715 <https://github.com/clash-lang/clash-compiler/issues/715>`__
   -  `#727 <https://github.com/clash-lang/clash-compiler/issues/727>`__
   -  `#730 <https://github.com/clash-lang/clash-compiler/issues/730>`__
   -  `#736 <https://github.com/clash-lang/clash-compiler/issues/736>`__
   -  `#738 <https://github.com/clash-lang/clash-compiler/issues/738>`__

0.99.3 *July 28th 2018*
-----------------------

-  Fixes bugs:

   -  Evaluator recognizes ``Bit`` literals
      `#329 <https://github.com/clash-lang/clash-compiler/issues/329>`__
   -  Use existential type-variables in context of GADT pattern match
   -  Do not create zero-bit temporary variables in generated HDL
   -  Use correct arguments in nested primitives
      `#323 <https://github.com/clash-lang/clash-compiler/issues/329>`__
   -  Zero-constructor data type needs 0 bits
      `#238 <https://github.com/clash-lang/clash-compiler/issues/238>`__
   -  Create empty component when result needs 0 bits
   -  Evaluator performs BigNat arithmetic

-  Features:

   -  Bundle and BitPack instances up to and including 62-tuples
   -  Handle undefined writes to RAM properly
   -  Handle undefined clock enables properly

0.99.1 *May 12th 2018*
----------------------

-  Allow ``~NAME[N]`` tag inside ``~GENSYM[X]``
-  Support HDL record selector generation
   `#313 <https://github.com/clash-lang/clash-compiler/pull/313>`__
-  ``InlinePrimitive`` support: specify HDL primitives inline with
   Haskell code
-  Support for ``ghc-typelits-natnormalise-0.6.1``
-  ``Lift`` instances for ``TopEntity`` and ``PortName``
-  ``InlinePrimitive`` support: specify HDL primitives inline with
   Haskell code

0.99 *March 31st 2018*
----------------------

-  New features:

   -  Major API overhaul: check the migration guide at the end of
      ``Clash.Tutorial``
   -  New features:

      -  Explicit clock and reset arguments
      -  Rename ``CLaSH`` to ``Clash``
      -  Implicit/``Hidden`` clock and reset arguments using a
         combination of ``reflection`` and ``ImplicitParams``.
      -  Large overhaul of ``TopEntity`` annotations
      -  PLL and other clock sources can now be instantiated using
         regular functions: ``Clash.Intel.ClockGen`` and
         ``Clash.Xilinx.ClockGen``.
      -  DDR registers:

         -  Generic/ASIC: ``Clash.Explicit.DDR``
         -  Intel: ``Clash.Intel.DDR``
         -  Xilinx: ``Clash.Intel.Xilinx``

   -  ``Bit`` is now a ``newtype`` instead of a ``type`` synonym and
      will be mapped to a HDL scalar instead of an array of one (e.g
      ``std_logic`` instead of ``std_logic_vector(0 downto 0)``)
   -  Hierarchies with multiple synthesisable boundaries by allowing
      more than one function in scope to have a ``Synthesize``
      annotation.

      -  Local caching of functions with a ``Synthesize`` annotation

   -  ``Bit`` type is mapped to a HDL scalar type (e.g. ``std_logic`` in
      VHDL)
   -  Improved name preservation
   -  Zero-bit values are filtered out of the generated HDL
   -  Improved compile-time computation

-  Many bug fixes

Older versions
--------------

Check out: \*
https://github.com/clash-lang/clash-compiler/blob/3649a2962415ea8ca2d6f7f5e673b4c14de26b4f/clash-prelude/CHANGELOG.md
\*
https://github.com/clash-lang/clash-compiler/blob/3649a2962415ea8ca2d6f7f5e673b4c14de26b4f/clash-lib/CHANGELOG.md
\*
https://github.com/clash-lang/clash-compiler/blob/3649a2962415ea8ca2d6f7f5e673b4c14de26b4f/clash-ghc/CHANGELOG.md
