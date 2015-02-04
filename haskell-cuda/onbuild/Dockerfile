# Docker image with Haskell libraries for GPU programming — onbuild variant

FROM mchakravarty/haskell-cuda:lts1.4-cuda6.5

MAINTAINER Manuel M T Chakravarty <chak@justtesting.org>

ONBUILD ADD . /usr/src/app

WORKDIR /usr/src/app

ONBUILD RUN    tarfile=`echo -n *.tar.gz` \
            && (if [ -e "$tarfile" ]; then tar --transform=s,^.*/,, -xzf $tarfile; fi) \
            && cabal install --verbose=0 --only-dependencies \
            && cabal build  --verbose=0

CMD []
ENTRYPOINT ["/usr/local/bin/cabal", "run"]
