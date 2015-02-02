Docker image supporting Haskell GPU programming:

* accelerate-cuda-0.15.0.0 and
* accelerate-fft-0.15.0.0.

The current library versions are based on LTS Haskell 1.4 with GHC 7.8.4 and CUDA 6.5.

Available from the public Docker registry as 'mchakravarty/haskell-cuda:lts1.4-cuda6.5'.

NB: This image requires a host OS with NVIDIA's CUDA driver (version 6.5) to access any CUDA device.
