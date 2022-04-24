# Longformer_paddle



## 论文源代码跑通

* 论文代码地址 `https://github.com/allenai/longformer`

* 所跑通的数据集 `triviaQA`

* 训练描述

  ```bash
  # 根据作者描述，base model在triviaQA数据集上进行实验，4个epochs在4张GPU上面运行了一天
  # 使用论文中的方法生成了训练集和验证集
  # 我在显卡上使用batchsize=4 跑通了代码
  # 一个epoch是139105个条目， 平均每秒处理1.6个条目
  # 跑完一个epoch + 验证 大概需要 24 个小时
  # 由loss数据可以看到，在训练过程中loss是由明显的下降趋势的
  # 经过一个epoch， loss值降至0.1至0.2之间
  # 由验证集的F1值可以看到，是0.694 -> 0.709, 是逐步上升向验收标准靠拢的
  # base model 在 trivaQa数据集上的表现符合论文中所描述的
  # 所使用的脚本如下
  python -m scripts.triviaqa  \
      --train_dataset datas/squad-wikipedia-train-4096.json  \
      --dev_dataset datas/squad-wikipedia-dev-4096.json  \
      --gpus 1  --batch_size 1  --num_workers 0 \
      --lr 0.00003 --warmup 1000 --epochs 4  --max_seq_len 4096 --doc_stride -1  \
      --save_prefix output_dir  \
      --model_path longformer-base-4096  \
      --seed 4321
  ```


* 论文代码跑通的输出结果见 ` paper_pyTorch_base_trivaQa.txt`

