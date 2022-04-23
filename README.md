# Longformer_paddle



## 论文源代码跑通

* 论文代码地址 `https://github.com/allenai/longformer`

* 所跑通的数据集 `triviaQA`

* 训练描述

  ```bash
  # 根据作者描述，base model在triviaQA数据集上进行实验，4个epochs在4张GPU上面运行了一天
  # 我在我的3060显卡上使用batchsize=1 跑通了代码
  # 一个epoch是139105个条目， 平均每秒处理1.18个条目
  # 跑完一个epoch大概需要 34 个小时
  # 由打印出的loss数据可以看到，在训练过程中loss是由明显的下降趋势的（见下图）
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

* `loss `  随时间变化曲线

