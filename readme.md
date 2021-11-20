GHC patch: <https://gitlab.haskell.org/ghc/ghc/-/merge_requests/7037>


RTS loader/linker:

```
$ cabal repl example

Build profile: -w ghc-9.3.20211120 -O1
In order, the following will be built (use -v for more details):
 - pqexample-0.0.0 (lib) (configuration changed)
 - example-0.0.0 (lib) (configuration changed)
Configuring library for pqexample-0.0.0..
Preprocessing library for pqexample-0.0.0..
Building library for pqexample-0.0.0..
Configuring library for example-0.0.0..
Preprocessing library for example-0.0.0..
GHCi, version 9.3.20211120: https://www.haskell.org/ghc/  :? for help
ghc: internal error: ASSERTION FAILED: file rts/CheckUnload.c, line 345

Stack trace:
                 0x4e1c707    set_initial_registers (rts/Libdw.c:294.5)
            0x7f3661fe4820    dwfl_thread_getframes (/nix/store/35v0m2ih9q4x3crhxiyr3pxc8ckn73gi-elfutils-0.180/lib/libdw-0.180.so)
            0x7f3661fe434b    get_one_thread_cb (/nix/store/35v0m2ih9q4x3crhxiyr3pxc8ckn73gi-elfutils-0.180/lib/libdw-0.180.so)
            0x7f3661fe4682    dwfl_getthreads (/nix/store/35v0m2ih9q4x3crhxiyr3pxc8ckn73gi-elfutils-0.180/lib/libdw-0.180.so)
            0x7f3661fe4bcf    dwfl_getthread_frames (/nix/store/35v0m2ih9q4x3crhxiyr3pxc8ckn73gi-elfutils-0.180/lib/libdw-0.180.so)
                 0x4e1c5f1    libdwGetBacktrace (rts/Libdw.c:263.15)
                 0x4dc57ae    rtsFatalInternalErrorFn (rts/RtsMessages.c:169.22)
                 0x4dc5397    barf (rts/RtsMessages.c:49.3)
                 0x4dc53fa    errorBelch (rts/RtsMessages.c:68.1)
                 0x4e18d33    findSectionIdx (rts/CheckUnload.c:347.8)
                 0x4e18e70    findOC (rts/CheckUnload.c:373.18)
                 0x4e1908a    markObjectCode (rts/CheckUnload.c:430.22)
                 0x4ded90d    markCAFs (rts/sm/GCAux.c:165.12)
                 0x4de96ae    GarbageCollect (rts/sm/GC.c:511.6)
                 0x4dcd6b7    scheduleDoGC (rts/Schedule.c:1884.5)
                 0x4dcb76d    schedule (rts/Schedule.c:579.7)
                 0x4dce92c    scheduleWaitThread (rts/Schedule.c:2652.11)
                 0x4dc0e7d    rts_evalLazyIO (rts/RtsAPI.c:567.1)
                 0x4dc5243    hs_main (rts/RtsMain.c:73.18)
                 0x145a3cd    (null) (/home/adam/src/ghc/ghc/_build/stage1/bin/ghc)
            0x7f3662061c7d    __libc_start_main (/nix/store/9df65igwjmf2wbw0gbrrgair6piqjgmi-glibc-2.31/lib/libc-2.31.so)
                 0x135317a    _start (../sysdeps/x86_64/start.S:122.0)

    (GHC version 9.3.20211120 for x86_64_unknown_linux)
    Please report this as a GHC bug:  https://www.haskell.org/ghc/reportabug
cabal: repl failed for example-0.0.0. The build process terminated with exit
code -6
```

System loader/linker:

```
$ cabal repl example --ghc-options=-fprefer-dynamic-loader

Warning: Unknown/unsupported 'ghc' version detected (Cabal 3.2.0.0 supports
'ghc' version < 8.12): /home/adam/src/ghc/ghc/_build/stage1/bin/ghc is version
9.3.20211120
Resolving dependencies...
Build profile: -w ghc-9.3.20211120 -O1
In order, the following will be built (use -v for more details):
 - pqexample-0.0.0 (lib) (configuration changed)
 - example-0.0.0 (lib) (configuration changed)
Configuring library for pqexample-0.0.0..
Preprocessing library for pqexample-0.0.0..
Building library for pqexample-0.0.0..
Configuring library for example-0.0.0..
Preprocessing library for example-0.0.0..
GHCi, version 9.3.20211120: https://www.haskell.org/ghc/  :? for help
Loaded GHCi configuration from /home/adam/.ghci
[1 of 2] Compiling A                ( src/A.hs, interpreted ) [Flags changed]
[2 of 2] Compiling B                ( src/B.hs, interpreted ) [Flags changed]
Ok, two modules loaded.
Leaving GHCi.
```
