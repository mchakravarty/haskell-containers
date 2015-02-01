# Haskell Ubuntu container with GHC 7.8.4, cabal-install 1.22, Alex 3.1.4, Happy 1.19.5 & c2hs 0.22.1

FROM ubuntu:14.04

MAINTAINER Manuel M T Chakravarty <chak@justtesting.org>

# Grab required Ubuntu packages
RUN apt-get update && apt-get install -y make curl xz-utils libgmp-dev libz-dev

RUN mkdir -p /usr/src
WORKDIR /usr/src

# Grab the appropriate GHC binary distribution and install it
RUN    curl -SL https://www.haskell.org/ghc/dist/7.8.4/ghc-7.8.4-x86_64-unknown-linux-deb7.tar.xz \
       | tar -xJ \
    && (cd ghc-7.8.4 && ./configure && make install) \
    && rm -rf ghc-7.8.4 \
    && ghc --version
    
# Grab the cabal-install source distribution and install it (no suitable binary available at this time)
RUN    curl -SL https://www.haskell.org/cabal/release/cabal-install-1.22.0.0/cabal-install-1.22.0.0.tar.gz \
       | tar -xz \
    && (cd cabal-install-1.22.0.0 && env EXTRA_CONFIGURE_OPTS="" ./bootstrap.sh) \
    && mv /root/.cabal/bin/cabal /usr/local/bin \
    && rm -rf cabal-install-1.22.0.0 \
    && cabal --version

# Install Alex, Happy & c2hs (and remove all packages installed while doing that)
RUN    cabal update \
    && cabal install --verbose=0 --global alex-3.1.4 happy-1.19.5 \
    && cabal install --verbose=0 --global c2hs-0.22.1 \
    && rm -rf /root/.ghc /root/.cabal \
    && (for pkg in language-c-0.4.7 QuickCheck-2.7.6 tf-random-0.5 random-1.1 syb-0.4.4 dlist-0.7.1 primitive-0.5.4.0; \
        do ghc-pkg unregister $pkg; done) \
    && rm -rf /usr/local/lib/x86_64-linux-ghc-7.8.4 \
    && alex --version \
    && happy --version \
    && c2hs --version \
    && ghc-pkg list

CMD ["ghci"]
