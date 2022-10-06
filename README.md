# video-grounding-benchmark

| model  | lib      | dataset                                 | note | time/epoch |
| ------ | -------- | --------------------------------------- | ---- | ---------- |
| VSLNet | tf1.x    | all                                     |      |            |
| LPNet  | tf1.x    | all                                     |      |            |
| ABLR   | tf1.x    | anet<br />tacos                         |      |            |
| 2D-TAN | torch    | all                                     |      |            |
| MAN    | -        | -                                       |      |            |
| TALL   | tf0.x    | tacos<br />charades(no feature offered) |      |            |
| SCDM   | tf1.x    | all                                     |      |            |
| RMW-RL | torch0.4 | charades                                |      |            |
| QSPN   | caffe    | charades                                |      |            |

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
