# ICML-Rebuttal

### [Scalability with respect to Dimension and Constraints]

We first present the results of exact sampling, computing closed-form loss, and gradient estimator with respect to varying dimensions. The number of constraints is half of the dimension (n). All results are averaged for 100 runs and conducted on a Nvidia A800 80GB GPU. All numbers are measured in seconds. We highlight that even though increasing dimension slows down the algorithm, the additional computational cost can be mitigated by choosing a larger batch size. For example, the additional time taken to run with batch_size=16 and batch_size=32 is almost negligible for n=32, 64, and 128. In the challenging n=2048 case, using batch_size=32 only takes 1.5 times more time to run compared to batch_size=16. Larger batch size can significantly reduce computation time per sample thanks to the parallelization of our method.

| Batch Size | n=32   | n=64   | n=128  | n=256  | n=512  | n=1024 | n=2048 |
|------------|--------|--------|--------|--------|--------|--------|--------|
| 16         | 0.00249| 0.00348| 0.00467| 0.00760| 0.00760| 0.04843| 0.20515|
| 32         | 0.00250| 0.00348| 0.00473| 0.00769| 0.01770| 0.06266| 0.31654|
| 64         | 0.00252| 0.00348| 0.00479| 0.00806| 0.02159| 0.09138| 0.46224|
| 128        | 0.00253| 0.00352| 0.00483| 0.00916| 0.02921| 0.13943| 0.78970|
| 256        | 0.00255| 0.00366| 0.00498| 0.01052| 0.04500| 0.23699| 1.24126|
