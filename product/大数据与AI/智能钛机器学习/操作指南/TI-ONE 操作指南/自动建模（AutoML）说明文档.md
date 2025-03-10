#### 半自动建模

1.登录**智能钛机器学习平台**，拖拽所选组件置于画布中。

2.单击组件，点击画布右侧参数配置区上方工具栏的**自动调参按钮**，启动算法自动调参模式。

   ![https://main.qcloudimg.com/raw/3badee9d2cbf007d6ddccefb876993ff.png](https://main.qcloudimg.com/raw/3badee9d2cbf007d6ddccefb876993ff.png)

3.配置算法参数，其中的**调参算法**目前TI支持`贝叶斯调参`、`网格调参`和`随机调参`三种调参方式：

   ![](https://main.qcloudimg.com/raw/c22264553b8317514e6af07fb8bba921.png)

   贝叶斯调参：给定优化的目标函数，通过不断地添加样本点来更新目标函数的后验分布。

   网格调参：在所有候选的参数选择中，通过循环遍历尝试每一种可能性，表现最好的参数就是最终的结果。

   随机调参：从指定的分布中采样固定数量的参数设置，为每类超参数定义一个边缘分布，并在这些参数上采样进行搜索。

   配置完所有的算法参数后，点击工具栏的运行按钮，启动任务运行。

4.对于运行效果良好的迭代，可将其**作为节点导出**至当前画布，点击**参数**，为**节点命名**并点击**节点导出**即可。

   ![https://main.qcloudimg.com/raw/468b39c81a31fbadb2f780bd5c41de32.jpg](https://main.qcloudimg.com/raw/468b39c81a31fbadb2f780bd5c41de32.jpg)

   导出后的节点默认直接与数据源进行连接，节点参数将默认填充迭代的具体值。

   ![https://main.qcloudimg.com/raw/cf3db5b9f321bac507f55fd77d4aded3.png](https://main.qcloudimg.com/raw/cf3db5b9f321bac507f55fd77d4aded3.png)

#### 全自动建模

在不通过人为来设定参数的情况，通过某些学习机制，让系统智能地去调节这些超参数，让整个机器学习流程做到全自动化。

1.登录**智能钛机器学习平台**，建立一个**全自动调参**的任务。

  此步骤中需要先设置好数据源，将左侧**自动建模（全自动AutoML）节点**拖入至画布产生连接，便可启动一个AutoML的任务。

   ![https://main.qcloudimg.com/raw/746e597fae946ce61ff3b7b6b1209f14.png](https://main.qcloudimg.com/raw/746e597fae946ce61ff3b7b6b1209f14.png)

2.AutoML节点的参数栏中，只需指定输入路径，进行简单的参数设置（迭代次数/迭代时间等）和资源参数设置，便可完成建模流程

#### 查看自动建模参数详情

用户可进行半自动与全自动建模参数的查看，方法如下：

1.单击组件，通过右键算法节点中的**自动调参详情**入口进行查看

   ![https://main.qcloudimg.com/raw/00af33b6c0056da60726c1137d6bfa91.jpg](https://main.qcloudimg.com/raw/00af33b6c0056da60726c1137d6bfa91.jpg)

2.自动调参详情页面：

   上方展示的是算法的基本运行信息，如训练/验证数据量、开始运行时间、目标列和特征列等；

   下方分两个模块，**模型指标**和**参数详情**。用户可以选择不同的评估指标来查看，**模型指标**模块主要以曲线呈现每一迭代的AUC效果

   ![https://main.qcloudimg.com/raw/899ad41aed98ba1326ce681b1d494295.jpg](https://main.qcloudimg.com/raw/899ad41aed98ba1326ce681b1d494295.jpg)

   **参数详情**模块展示的是每一轮迭代的信息、AUC值、运行状态及对应迭代的参数，点击参数展示被调的参数这一轮的具体值。

   ![https://main.qcloudimg.com/raw/a25f77b5ef3cabd0947aea8374f35e2b.jpg](https://main.qcloudimg.com/raw/a25f77b5ef3cabd0947aea8374f35e2b.jpg)

   ![https://main.qcloudimg.com/raw/e11c7e9753b23a2591c14861ec3eabf1.jpg](https://main.qcloudimg.com/raw/e11c7e9753b23a2591c14861ec3eabf1.jpg)

