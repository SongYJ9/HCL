## High Confidence Learning（HCL）
中山大学 计算机学院 syj

这里是中山大学 2022 模式识别研究生课程大作业，题目为“对噪声标签鲁棒的视觉识别”

我们在 [Augmentation Strategies for Learning with Noisy Labels (CVPR 2021)](https://github.com/KentoNishi/Augmentation-for-LNL) 的模型 DM-AugDesc-WS 上做优化，并实现了更好的性能

<details open>
    <summary>Summary Metrics</summary>
    <h3>CIFAR-10</h3>
    <table>
        <thead>
            <tr>
                <th rowspan="2">Model</th>
                <th rowspan="2">Metric</th>
                <th colspan="3">Noise Type/Ratio</th>
            </tr>
            <tr>
                <th>20% sym</th>
                <th>50% sym</th>
                <th>80% sym</th>
            </tr>
            <tbody>
                <tr>
                    <td>SOTA</td>
                    <td>Highest</td>
                    <td>96.54%</td>
                    <td>95.64%</td>
                    <td>93.77%</td>
                </tr>
                <tr>
                    <td><strong>Ours</strong></td>
                    <td>Highest</td>
                    <td><strong>96.82%</strong></td>
                    <td><strong>96.03%</strong></td>
                    <td><strong>94.28%</strong></td>
                </tr>
            </tbody>
        </thead>
    </table>
    <h3>CIFAR-100</h3>
    <table>
        <thead>
            <tr>
                <th rowspan="2">Model</th>
                <th rowspan="2">Metric</th>
                <th colspan="3">Noise Type/Ratio</th>
            </tr>
            <tr>
                <th>20% sym</th>
                <th>50% sym</th>
                <th>80% sym</th>
            </tr>
            <tbody>
                <tr>
                    <td>SOTA</td>
                    <td>Highest</td>
                    <td>79.89%</td>
                    <td>77.64%</td>
                    <td>66.36%</td>
                </tr>
                <tr>
                    <td><strong>Ours</strong></td>
                    <td>Highest</td>
                    <td><strong>80.08%</strong></td>
                    <td><strong>78.01%</strong></td>
                    <td><strong>68.94%</strong></td>
                </tr>
            </tbody>
        </thead>
    </table>
</details>

### 训练

如果你想跑通我们的实验代码，你可以这么做：

1. 准备好 CIFAR-10 和 CIFAR-100 数据集，并将其文件夹 `cifar-10-batches-py` 和 `cifar-100-python` 放在与 `train_cifar_ce.py` 和 `train_cifar_mix.py` 同目录下

   ```
   root
   |
   |-- cifar-10-batches-py
   |   |
   |   |-- data_batch_1
   |   |-- ...
   |
   |-- cifar-100-python
   |   |
   |   |-- train
   |   |-- ...
   |
   |-- train_cifar_ce.py
   |-- train_cifar_mix.py
   |-- ...
   ```

   CIFAR-10 和 CIFAR-100 数据集请自行去 [CIFAR-10 and CIFAR-100 datasets (toronto.edu)](http://www.cs.toronto.edu/~kriz/cifar.html) 下载，解压后将文件夹放在上述对应位置即可

2. 运行对应的代码：

   ```python
   # HCL-Mix方法 cifar-10 20%噪声 
   python train_cifar_mix.py --preset c10.20sym.AugDesc-WS --machine localPC_mix
   # HCL-CE方法 cifar-100 80%噪声 
   python train_cifar_ce.py --preset c100.80sym.AugDesc-WS --machine localPC_ce
   # 其他情况依葫芦画瓢修改对应部分即可
   ```

   如果有 import error 按报错说明安装对应包即可

3. 结果：可在程序结束运行后找到对应的 metrics.log 文件，例如运行 `train_cifar_mix.py --preset c10.20sym.AugDesc-WS --machine localPC_mix ` 后，log 文件在 `localPC_mix_checkpoints/c10/20sym/AugDesc-WS/saved/metrics.log` 这里。

   当然也可以运行程序前用 `script log.txt` 自行记录命令行输出结果

### 我们的运行结果

我们已将我们的最好运行结果的 log 文件按情况标记好名字放在 log 文件夹内，有兴趣的可自行浏览
