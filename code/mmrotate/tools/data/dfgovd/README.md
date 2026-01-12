# Preparing DFGOVD Dataset

<!-- [DATASET] -->

The data structure is as follows:

```none
mmrotate
├── mmrotate
├── tools
├── configs
├── data
│   ├── DFGOVD
│   │   ├── train
│   │   ├── val
│   │   ├── test
```

## split dfgovd dataset

Please crop the original images into 1024×1024 patches with an overlap of 200 by run

```shell
python tools/data/dfgovd/split/img_split.py --base-json \
  tools/data/dfgovd/split/split_configs/ss_train.json
python tools/data/dfgovd/split/img_split.py --base-json \
  tools/data/dfgovd/split/split_configs/ss_val.json
python tools/data/dfgovd/split/img_split.py --base-json \
  tools/data/dfgovd/split/split_configs/ss_test.json
```


## change root path in base config

Please change `data_root` in `configs/_base_/datasets/dfgovd.py` to split dfgovd dataset.
