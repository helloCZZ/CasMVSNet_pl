This folder contains the minimum necessary scripts for running DTU evaluation. You can download the full code [here](http://roboimagedata2.compute.dtu.dk/data/MVS/SampleSet.zip).

## Install

You need to have `Matlab`. It is a **must**, you cannot use workaround free software like `octave`, I tried but some libraries are not available (e.g. `KDTreeSearch`)

## Data download

1.  Download [Points](http://roboimagedata2.compute.dtu.dk/data/MVS/Points.zip) and [SampleSet](http://roboimagedata2.compute.dtu.dk/data/MVS/SampleSet.zip).
2.  Extract the files and arrange in the following structure:
```
├── DTU (can be anywhere)
│   ├── Points
│   └── ObsMask
```
Where the `ObsMask` folder is taken from `SampleSet/MVS Data`.

## Evaluation

1.  Change `dataPath`, `plyPath`, `resultsPath` [here](https://github.com/kwea123/CasMVSNet_pl/blob/784cec6635fa819bab0d716c15ba07972c260293/evaluations/dtu/BaseEvalMain_web.m#L8-L10). Be careful that you need to ensure `resultsPath` folder already exists because `Matlab` won't automatically create...
2.  Open `Matlab` and run `BaseEvalMain_web.m`. It will compute the metrics for each scan specified [here](https://github.com/kwea123/CasMVSNet_pl/blob/master/evaluations/dtu/BaseEvalMain_web.m#L23). This step will take **A VERY LONG TIME**: for the point cloud I provide, each of them takes **~20mins** to evaluate... the time depends on the point cloud size.
3.  Set `resultsPath` [here](https://github.com/kwea123/CasMVSNet_pl/blob/master/evaluations/dtu/ComputeStat_web.m#L10) the same as above, then run `ComputeStat_web.m`, it will compute the average metrics of all scans. The final numbers `mean acc` and `mean comp` are the final result, and `overall` is just the average of these two numbers. You can then compare these numbers with papers/other implementations.

## Result
Since it takes a long time to evaluate (5 hours using default settings...), I provide the numbers here for comparison with some open source methods:

|   | Acc. | Comp. | Overall | resolution |
| --- | --- | --- | --- | --- |
| [MVSNet](https://github.com/YoYo000/MVSNet) | 0.396 | 0.527 | 0.462 | 1600x1184 |
| [MVSNet_pytorch](https://github.com/xy-guo/MVSNet_pytorch) | 0.4492 | 0.3796 | 0.4144 | 1600x1184(?) |
| *[MVSNet_pytorch](https://github.com/xy-guo/MVSNet_pytorch) | 0.5229 | 0.4514 | 0.4871 | 1152x864 |
| *[R-MVSNet](https://github.com/YoYo000/MVSNet) | 0.383 | 0.452 | 0.4175 | 1600x1184 |
| *[CasMVSNet](https://github.com/alibaba/cascade-stereo/tree/master/CasMVSNet) | - | - | - | 1152x864 |
| *[PointMVSNet](https://github.com/callmeray/PointMVSNet) | - | - | - | 1280x960 |
| *This repo | 0.3653 | 0.3664 | 0.3658 | 1152x864 |

1. The number of views used is 5 for all methods.
2. *Methods' metrics are verified by me using their pretrained model, or the point cloud directly for R-MVSNet.
3. Generally, larger resolution leads to better result.
3. (?) means not sure, asking the author currently.