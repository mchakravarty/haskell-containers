# Docker image with Haskell libraries for parallel programming based on LTS Haskell

FROM mchakravarty/ghc-7.8.4:latest

MAINTAINER Manuel M T Chakravarty <chak@justtesting.org>

# For packages in LTS, we give no version number, as that is fixed by LTS.
ENV PKGS accelerate accelerate-io-0.15.0.0 \
         vect-floating-accelerate-0.1.0.4 linear-accelerate-0.2 \
         monad-par monad-par-extras \
         parallel \
         repa repa-algorithms repa-io

RUN    cabal update \
    && curl -LS http://www.stackage.org/snapshot/lts-1.4/cabal.config?global=true >>/root/.cabal/config \
    && cabal install $PKGS
