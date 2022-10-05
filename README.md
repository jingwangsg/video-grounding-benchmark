# video-grounding-benchmark

| model  | lib      | note                                                               | time/epoch |
| ------ | -------- | ------------------------------------------------------------------ | ---------- |
| VSLNet | tf1.x    | to zh                                                              |            |
| LPNet  | tf1.x    | to zh                                                              |            |
| ABLR   | tf1.x    |                                                                    |            |
| 2D-TAN | torch    |                                                                    |            |
| MAN    | -        | -                                                                  | -          |
| TALL   | tf0.x    | charades没有提供特征，需要自己抽特征<br />(用py3 tf1.x尝试跑通ing) |            |
| SCDM   | tf1.x    |                                                                    |            |
| RMW-RL | torch0.4 |                                                                    |            |
| QSPN   | caffe    |                                                                    |            |

All benchmarks run on TACoS Dataset

# Working Log

# VSLNet

**Pre-trained Glove**

The pre-trained GloVe embedding is available at [here](https://nlp.stanford.edu/projects/glove/), please download
`glove.840B.300d.zip`, unzip and put it under `data/` folder.

**TACoS**

TACoS dataset is from [[jiyanggao/TALL]](https://github.com/jiyanggao/TALL), while the videos of TACoS is from MPII
Cooking Composite Activities dataset, which can be download [here](https://www.mpi-inf.mpg.de/departments/computer-vision-and-machine-learning/research/human-activity-recognition/mpii-cooking-composite-activities/).
Note that we also use the processed TACoS dataset in [[microsoft/2D-TAN]](https://github.com/microsoft/2D-TAN).

Extract visual features for TACoS:

```shell
python3 extract_tacos.py --load_model <path to>/rgb_imagenet.pt  \
      --video_dir <path to video dir>  \
      --dataset_dir <path to charades-sta dataset dir>  \
      --images_dir <path to images dir>  \  # if images not exist, decompose video into images
      --save_dir <path to save extracted visual features>  \
      --strides 16 --remove_images  # whether remove extracted images to release space
```

(Optional) Convert the pre-trained C3D visual features from [[jiyanggao/TALL]](https://github.com/jiyanggao/TALL)
([Interval64_128_256_512_overlap0.8_c3d_fc6.tar](https://drive.google.com/file/d/1zQp0aYGFCm8PqqHOh4UtXfy2U3pJMBeu/view),
[Interval128_256_overlap0.8_c3d_fc6.tar](https://drive.google.com/file/d/1zC-UrspRf42Qiu5prQw4fQrbgLQfJN-P/view)):

```shell
python3 extract_tacos_org.py --data_path <path to tacos annotation dataset>  \
      --feature_path <path to downloaded C3D features>  \
      --save_dir <path to save extracted visual features>  \
      --sample_rate 64  # sliding windows
```

# Experiment Result

| model  | framework  | time/per epoch (batch size=16) |
| ------ | ---------- | ------------------------------ |
| VSLNet | tensorflow |                                |
| LPNet  | tensorflow |                                |
| 2D-TAN | pytorch    |                                |
| TALL   | tensorflow |                                |
|        |            |                                |
