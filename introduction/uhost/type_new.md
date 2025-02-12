{{indexmenu_n>2}}

# 机型与CPU平台

*此文档适合于2019年5月后新上线的新版主机创建页，重新定义了大部分机型的概念，这些新概念被聚合为主机机型概念2.0。若您仍然使用旧版本的主机创建页，机型概念请参照主机概念1.0的文档[机型与规格](/compute/uhost/introduction/uhost/type)；若您希望了解2.0概念与1.0概念相比发生了哪些变化，请参照[FAQ](/compute/uhost/faq#主机机型概念10和20发生了哪些变化)。*

## 机型

UCloud云主机根据应用场景将主机区分为：**快杰型O、通用型N、高主频型C、GPU型G**总计4种机型。

|             | 特点                   | 适用场景             |
| ----------- | -------------------- | ---------------- |
| 快杰型 O (公测中) | 计算、存储、网络性能卓越的最新一代云主机 | 数据库，MMO游戏，人工智能等  |
| 通用型 N       | 配置自由灵活，选择丰富          | 企业级应用，内存服务，数据分析等 |
| 高主频型 C      | 采用3.2GHz主频的CPU，计算性能强 | 高频交易，数据处理，图形渲染等  |
| GPU型 G      | 搭载K80，P40或V100 GPU   | 人工智能，科学计算，图形渲染等  |

价格详情请参见：[主机价格](https://docs.ucloud.cn/compute/uhost/price)

### 快杰型 O（公测中）

1）简介：计算、存储与网络性能卓越的最新一代云主机。适合全面需求场景。

2）CPU平台支持：Skylake/Cascadelake

3）CPU内存组合（支持配比1:1-1:8）：

| CPU | 内存                 |
| --- | ------------------ |
| 4核  | 4G，8G，16G，32G      |
| 8核  | 8G，16G，32G，64G     |
| 16核 | 16G，32G，64G，128G   |
| 32核 | 32G，64G，128G, 256G |
| 64核 | 64G，128G，256G      |

4）磁盘类型支持：支持RSSD云盘、SSD云盘

具体选择范围：

| 系统盘              | 数据盘                |
| ---------------- | ------------------ |
| SSD云盘 (20-500GB) | RSSD云盘（20-32000GB） |

5）特性支持：网络增强2.0和热升级

6）限制：快杰型云主机仅支持高内核版本镜像。若希望使用现有镜像创建快杰型云主机，请联系技术支持。

### 通用型 N

1）简介：提供最灵活自由的CPU、内存、磁盘组合。适合计算、存储、网络等均衡的场景。

2）CPU平台支持：IvyBridge/Haswell/Broadwell/Skylake

3）CPU内存组合（支持配比1:1-1:8）：

| CPU | 内存                         |
| --- | -------------------------- |
| 1核  | 1G，2G，4G，8G                |
| 2核  | 2G，4G，6G，8G，12G，16G        |
| 4核  | 4G，6G，8G，12G，16G，32G       |
| 8核  | 8G，12G，16G，24G，32G，48G，64G |
| 16核 | 16G，24G，32G，48G，64G，128G   |
| 24核 | 24G，32G，64G，96G，192G       |
| 32核 | 32G，64G，96G，128G           |

4）磁盘类型支持：支持云盘、普通本地盘、SSD本地盘

具体选择范围：

| 系统盘              | 数据盘                              |
| ---------------- | -------------------------------- |
| SSD云盘 (20-500GB) | SSD云盘（20-4000GB），普通云盘（20-8000GB） |
| 普通本地盘（20-100GB）  | 普通本地盘（20-2000GB）                 |
| SSD本地盘（20-100GB） | SSD本地盘（20-1000GB）                |

5）特性支持：网络增强1.0/网络增强2.0（仅Skylake及以上支持）和热升级

### 高主频型 C

1）描述：CPU主频≥3.0GHz的机型，适合计算类业务，如高频交易、渲染、人工智能等。

2）CPU平台支持：Skylake

3）CPU内存组合（支持配比1:1-1:8）：

| CPU | 内存               |
| --- | ---------------- |
| 1核  | 1G，2G，4G，8G      |
| 2核  | 2G，4G，8G，16G     |
| 4核  | 4G，8G，16G，32G    |
| 8核  | 8G，16G，32G，64G   |
| 16核 | 16G，32G，64G，128G |
| 32核 | 32G，64G，128G     |

4）磁盘类型支持：支持云盘、SSD本地盘

具体选择范围：

| 系统盘              | 数据盘                              |
| ---------------- | -------------------------------- |
| SSD云盘 (20-500GB) | SSD云盘（20-4000GB），普通云盘（20-8000GB） |
| SSD本地盘（20-100GB） | SSD本地盘（20-1000GB）                |

5）特性支持：网络增强1.0和热升级

### GPU型 G

附带GPU卡的机型，适合需要GPU进行计算的业务，如高性能运算、渲染、人工智能等。目前支持K80, P40, V100
3种GPU卡。三种卡附属的配置略有不同。

#### GPU性能对比

| 参数       | Tesla V100 | Tesla P40 | Tesla K80  |
| -------- | ---------- | --------- | ---------- |
| CUDA核心数  | 5120       | 3840      | 2496       |
| 单精度浮点性能  | 14 TFOPS   | 12 TFLOPS | 8.7 TFLOPS |
| INT8性能   | N/A        | 47 TOPS   | N/A        |
| Tensor性能 | 112 TFLOPS | N/A       | N/A        |
| 显存容量     | 16GB       | 24GB      | 12GB       |
| 架构       | Volta      | Pascal    | Kepler     |

#### V100 / P40 GPU

1）CPU平台支持：Broadwell

2）GPU-CPU-内存组合支持：

| GPU | CPU | 内存       |
| --- | --- | -------- |
| 1颗  | 4核  | 8G，16G   |
|     | 8核  | 16G，32G  |
| 2颗  | 8核  | 16G，32G  |
|     | 16核 | 32G，64G  |
| 4颗  | 16核 | 32G，64G  |
|     | 32核 | 64G，128G |

3）磁盘类型支持：SSD本地盘和云盘

| 系统盘              | 数据盘                              |
| ---------------- | -------------------------------- |
| SSD云盘 (20-500GB) | SSD云盘（20-4000GB），普通云盘（20-8000GB） |
| SSD本地盘（20-100GB） | SSD本地盘（20-1000GB）                |

4）特性支持：网络增强1.0

#### K80 GPU

1）CPU平台支持：Haswell

2）GPU-CPU-内存组合支持：

| GPU   | CPU | 内存      |
| ----- | --- | ------- |
| 1颗/2颗 | 4核  | 8G，16G  |
|       | 8核  | 16G，32G |
|       | 16核 | 32G，64G |

3）磁盘类型支持：SSD本地盘

| 系统盘              | 数据盘               |
| ---------------- | ----------------- |
| SSD本地盘（20-100GB） | SSD本地盘（20-1000GB） |

4）特性支持：网络增强1.0

## CPU平台

CPU平台属性是指云主机所在宿主机的CPU微架构版本，包含以下选项：Intel IvyBridge (V2), Intel Haswell
(V3)，Intel Broadwell (V4)，Intel Skylake (V5)，Intel
Cascadelake（V6）。每代CPU平台的主要差异为硬件架构不同、指令集不同。**不同CPU平台的云主机价格相同。**

创建时可选定最低的CPU平台，或让后台完全自动分配。例如，用户创建时选择了CPU平台≥Intel Haswell
(V3)，后台调度系统可能将主机调度到Haswell、Broadwell或是Skylake平台的宿主机上。

CPU平台选择最佳实践：

1）CPU平台是主机创建的高级选项，普通的Web网站/APP/数据库/devops以及其他并非重计算业务（CPU平均使用率在30%以下），以及对指令集无要求，建议选择CPU平台为自动分配。

2）对指令集有要求的业务（如软件明确要求AVX指令集），建议您参照以下表格进行选择：

| CPU平台       | AVX | AVX-2 | AVX-512 |
| ----------- | --- | ----- | ------- |
| IvyBridge   |     |       |         |
| Haswell     | √   |       |         |
| Broadwell   | √   | √     |         |
| Skylake     | √   | √     | √       |
| Cascadelake | √   | √     | √       |

3）对计算性能有明确要求的业务，推荐选择当前可用区的最新一代。

## 后续阅读

[主机价格](https://docs.ucloud.cn/compute/uhost/price)

[主机磁盘简介](/compute/uhost/introduction/disk)

[特性简介：网络增强、热升级与数据方舟](/compute/uhost/introduction/uhost/feature)
