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

### Pseudo Code:
```
# n is dimension
For n in ls_n:
    num_constraints = n // 2
    Total_time = 0
    For i in range(repeat_num):
        Randomly generate unconstrained parameter and constraints
        Conduct exact sampling
        Compute closed-form loss
        Compute gradient estimator
        Total_time += time
    Total_time /= repeat_num
    print(Total_time)
```

We next investigate the impact of the number of constraints (num_k). We conduct experiments on the challenging n=2048 setting. Similar to the findings in scaling the number of dimensions, using larger batch sizes significantly reduces computation time per sample. Additionally, we also found that increasing the number of constraints does not significantly increase the computational time. For example, under batch_size = 64, increasing the number of constraints from 256 to 512 only increases computational time by 32%.

| Batch Size | num_k=32 | num_k=64 | num_k=128 | num_k=256 | num_k=512 | num_k=1024 |
|------------|----------|----------|-----------|-----------|-----------|------------|
| 16         | 0.05109  | 0.05343  | 0.05894   | 0.07336   | 0.10885   | 0.20515    |
| 32         | 0.09899  | 0.10259  | 0.11060   | 0.13211   | 0.18119   | 0.31654    |
| 64         | 0.19531  | 0.20241  | 0.21666   | 0.24871   | 0.32935   | 0.46224    |
| 128        | 0.29093  | 0.30316  | 0.32456   | 0.38556   | 0.52796   | 0.78970    |
| 256        | 0.47706  | 0.48106  | 0.50057   | 0.52001   | 0.84375   | 1.24126    |

### Pseudo Code:
```
# num_k is number of constraints
For num_k in ls_k:
    Total_time = 0
    For i in range(repeat_num):
        Randomly generate unconstrained parameter and constraints
        Conduct exact sampling
        Compute closed-form loss
        Compute gradient estimator
        Total_time += time
    Total_time /= repeat_num
    print(Total_time)
```

### [Comparison with Baseline CL in DDPM]
| **DDPM + CL** | **FID**  | **IS**          |
|---------------|----------|-----------------|
| **CIFAR**     | 4.234    | 8.535(0.157)    |
| **CelebA**    | 12.067   | 2.345(0.039)    |
| **Lsun Church** | 6.695  | 2.319(0.028)    |
| **Lsun Cat**    | 13.472 | 4.642(0.081)    |


### [Comparison with Baseline Constrained Reparameterization]

| VAE + Constrained Reparam             | LL           | ELBO          | RL           | Violation |
| -                                     | -            | -             | -            | -         |
| VAE + Constrained Reparam             | -22.33(0.48) | -23.83(0.49)  | 14.54(0.58)  | 0.0(0.0)   |
| Ladder VAE + Constrained Reparam      | -25.27(0.19) | -31.56(0.48)  | 25.20(0.62)  | 0.0(0.0)   |
| Graph VAE + Constrained Reparam       | -22.96(0.80) | -23.55(0.86)  | 16.08(1.38)  | 0.0(0.0)   |

| **DDPM + Constrained Reparametrization** | **FID**  | **IS**            |
|-|-|-|
| CIFAR                                    | 3.881   | 9.2126(0.122)     |
| CelebA                                   | 10.961  | 2.043(0.028)      |
| Lsun Church                              | 4.895   | 2.377(0.032)      |
| Lsun Cat                                 | 12.696  | 4.7071(0.062)     |

| **Charge Neural Prediction**             | **MAD**         | **NLL**           |
|-|-|-|
| Constrained Reparametrization           | 0.0256(0.0007)  | 334.03(2398)      |
| Constrained Reparametrization Ensemble  | 0.0242(0.0006)  | 4883.46(1695)     |

| **Chemical Process Units and Subsystems** | **CSTR**    | **Plant**     | **Distillation** |
|-|-|-|-|
| Constrained Reparametrization            | 7.13(3.22) | 0.14(0.07)    | 2.22(0.94)       |

| **Stock Investment**           | **Value**         |
|-|-|
| Constrained Reparametrization  | 1.8162(0.2966)    |



### [Updated Paper]
<iframe src="updated_paper.pdf" width="100%" height="600"></iframe>








