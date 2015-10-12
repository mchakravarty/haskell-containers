# Haskell Ubuntu container image with GHC 7.10.2, cabal-install 1.22.6, Alex 3.1.4, Happy 1.19.5 & c2hs 0.25.2
# (tracking LTS Haskell 3.8)

FROM ubuntu:14.04

MAINTAINER Manuel M T Chakravarty <chak@justtesting.org>

# Grab required Ubuntu packages
RUN apt-get update && apt-get install -y make curl xz-utils libgmp-dev libz-dev libtinfo-dev

WORKDIR /usr/src

# Grab the appropriate GHC binary distribution and install it
RUN    curl -SL http://downloads.haskell.org/~ghc/7.10.2/ghc-7.10.2-x86_64-unknown-linux-deb7.tar.xz \
       | tar -xJ \
    && (cd ghc-7.10.2 && ./configure && make install) \
    && rm -rf ghc-7.10.2 /usr/local/share/doc \
    && ghc --version
    
# Grab the cabal-install source distribution and install it (no suitable binary available at this time)
RUN    curl -SL https://www.haskell.org/cabal/release/cabal-install-1.22.6.0/cabal-install-1.22.6.0.tar.gz \
       | tar -xz \
    && (cd cabal-install-1.22.6.0 && env EXTRA_CONFIGURE_OPTS="" ./bootstrap.sh) \
    && mv /root/.cabal/bin/cabal /usr/local/bin \
    && rm -rf cabal-install-1.22.6.0 \
    && cabal --version

# Install Alex, Happy & c2hs (and remove all packages installed while doing that)
RUN    cabal update \
    && cabal install --verbose=0 --global --disable-documentation alex-3.1.4 happy-1.19.5 \
    && cabal install --verbose=0 --global --disable-documentation c2hs-0.25.2 \
    && rm -rf /root/.ghc /root/.cabal \
    && (for pkg in language-c QuickCheck tf-random random syb mtl text dlist \
                   primitive; \
        do ghc-pkg unregister $pkg; done) \
    && rm -rf /usr/local/lib/x86_64-linux-ghc-7.10.2 \
    && alex --version \
    && happy --version \
    && c2hs --version \
    && ghc-pkg list

CMD ["ghci"]
