# 2.3 CUDA Streams and Events

For this module, we need to add **sm_90**, the NVIDIA “Streaming Multiprocessor” (SM) compute capability 9.0, to support the Hopper generation.

To compile the streams and events code, we need to modify the [Makefile](https://github.com/openhackathons-org/nways_multi_gpu/blob/bc2a5887505bba17672882b3ec7a62c04ecf0d24/labs/CFD/English/C/source_code/cuda/Makefile).

Use the [Makefile_cuda](https://github.com/jpnavarro-nv/cuda_training_nways/blob/main/Makefile_cuda) as a reference.
