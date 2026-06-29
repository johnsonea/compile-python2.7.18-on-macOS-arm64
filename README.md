# compile-python2.7.18-on-macOS-arm64
Instructions to compile python 2.7.18 on macOS 15 Sequoia as an arm64 binary.

The python2_install_on_apple_silicon.zsh code downloads, compiles as an arm64 binary (native Apple Silicon), and installs Python 2.7.18.  (Note that it does not change the PATH to automatically add the newly compiled python2 to the path.)

The installer available from python.org -- https://www.python.org/ftp/python/2.7.18/python-2.7.18-macosx10.9.pkg -- which is linked from https://www.python.org/downloads/release/python-2718/ -- is x86_64, i.e., compiled for an Intel chip.  It will currently run fine under Rosetta 2, but it has been announced that Rosetta 2 will be removed for general applications starting in macOS 28 (to be released in late 2027).
