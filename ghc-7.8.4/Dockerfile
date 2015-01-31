# Haskell Ubuntu container with GHC 7.8.4, cabal-install 1.22, Alex 3.1.4, Happy 1.19.5 & c2hs 0.22.1

FROM ubuntu:14.04

MAINTAINER Manuel M T Chakravarty <chak@justtesting.org>

# Grab required Ubuntu packages
RUN apt-get update && apt-get install -y make wget xz-utils libgmp-dev libz-dev

RUN mkdir -p /build
WORKDIR /build

# Grab the appropriate GHC binary distribution and install it
ENV ghc_tarball ghc-7.8.4-x86_64-unknown-linux-deb7.tar.xz
ADD https://www.haskell.org/ghc/dist/7.8.4/$ghc_tarball /build/
RUN tar xf $ghc_tarball
RUN (cd ghc-7.8.4 && ./configure && make install)
RUN rm -rf ghc-7.8.4 $ghc_tarball
RUN ghc --version

# Grab the cabal-install source distribution and install it (no suitable binary available at this time)
ENV cabal_tarball cabal-install-1.22.0.0.tar.gz
ADD https://www.haskell.org/cabal/release/cabal-install-1.22.0.0/$cabal_tarball /build/
RUN tar xf $cabal_tarball
RUN (cd cabal-install-1.22.0.0 && env EXTRA_CONFIGURE_OPTS="" ./bootstrap.sh)
RUN mv /root/.cabal/bin/cabal /usr/local/bin
RUN rm -rf cabal-install-1.22.0.0 $cabal_tarball
RUN cabal --version

# Install Alex, Happy & c2hs
RUN cabal update
RUN cabal install --global alex-3.1.4
RUN alex --version
#
RUN cabal install --global happy-1.19.5
RUN happy --version
#
RUN cabal install --global c2hs-0.22.1
RUN c2hs --version

# Clean up extra packages...
# ... local package db
RUN rm -rf /root/.ghc /root/.cabal

# ... global package db
RUN ghc-pkg unregister language-c-0.4.7
RUN ghc-pkg unregister QuickCheck-2.7.6
RUN ghc-pkg unregister tf-random-0.5
RUN ghc-pkg unregister mtl-2.2.1
RUN ghc-pkg unregister transformers-0.4.2.0
RUN ghc-pkg unregister random-1.1
RUN ghc-pkg unregister syb-0.4.4
RUN ghc-pkg unregister dlist-0.7.1
RUN ghc-pkg unregister primitive-0.5.4.0
RUN rm -rf /usr/local/lib/x86_64-linux-ghc-7.8.4
RUN ghc-pkg list
