# compile-python2.7.18-on-macOS-arm64
Instructions to compile python 2.7.18 on macOS 15 Sequoia as an arm64 binary.

The python2_install_on_apple_silicon.zsh code downloads, compiles as an arm64 binary (native Apple Silicon), and installs Python 2.7.18.  (Note that it does not change the PATH to automatically add the newly compiled python2 to the path.)

The installer available from python.org -- https://www.python.org/ftp/python/2.7.18/python-2.7.18-macosx10.9.pkg -- which is linked from https://www.python.org/downloads/release/python-2718/ -- is x86_64, i.e., compiled for an Intel chip.  It will currently run fine under Rosetta 2, but it has been announced that Rosetta 2 will be removed for general applications starting in macOS 28 (to be released in late 2027).

Note that, before installing python2 from source, you must have zlib and OpenSSL 1.1.1 installed as follows:

1. zlib installed like:

       URL=https://zlib.net/current/zlib.tar.gz
       curl -L -o - $URL | tar zxf -
       pushd zlib-*
       ./configure && make && make check && sudo make install
       popd

2. OpenSSL 1.1.1 installed (where it will not contaminate other builds) like:
    
       export OPENSSL111=/usr/local/obsolete/openssl111
       URL=https://github.com/openssl/openssl/releases/download/OpenSSL_1_1_1w/openssl-1.1.1w.tar.gz
       [ -d $OPENSSL111 ] || sudo mkdir -p $OPENSSL111
       curl -L -o - $URL | tar zxf -
       pushd openssl-1.1.1w
       ./config --prefix=$OPENSSL111 --openssldir=$OPENSSL111 shared zlib
       make && make test && sudo make install
       for f in libcrypto.1.1.dylib libssl.1.1.dylib; do
           sudo install_name_tool -id $OPENSSL111/lib/$f $OPENSSL111/lib/$f
       done
       sudo install_name_tool -change $OPENSSL111/libcrypto.1.1.dylib $OPENSSL111/lib/libcrypto.1.1.dylib $OPENSSL111/lib/libssl.1.1.dylib
       popd

