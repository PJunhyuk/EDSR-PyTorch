#### Server-Info
Ubuntu 16.04.3 LTS  
amd64 (64bit)

#### Install

```
$ nvidia-docker run -it --shm-size 8G --name jgravity_EDSR_1 pytorch/pytorch:0.4_cuda9_cudnn7 /bin/bash
```

> https://github.com/pytorch/pytorch/issues/2244

```
$ nvidia-docker restart jgravity_EDSR_1
$ nvidia-docker attach jgravity_EDSR_1
```

```
# git clone https://github.com/PJunhyuk/EDSR-PyTorch
```

```
# pip install --upgrade pip
# pip install matplotlib
# pip install imageio
# pip install tqdm
# pip install scikit-image
```

#### Test sample image

```
# python main.py --data_test Demo --scale 4 --pre_train download --test_only --save_results --cpu
```

```
$ docker cp jgravity_EDSR_1:/workspace/EDSR-PyTorch/test/0853x4.png ./
$ docker cp jgravity_EDSR_1:/workspace/EDSR-PyTorch/experiment/test/results-Demo/0853x4_x4_SR.png ./
```

#### Test own images

```
# apt-get update
# apt-get install wget

test# wget https://jgravity2.cafe24.com/dataset/1.jpg
test# wget https://jgravity2.cafe24.com/dataset/2.jpg

# python main.py --data_test Demo --scale 4 --pre_train download --test_only --save_results --cpu
```

#### Standard benchmarks

```
/dataset# wget https://cv.snu.ac.kr/research/EDSR/benchmark.tar
/dataset# wget https://cv.snu.ac.kr/research/EDSR/DIV2K.tar
/dataset# tar xvf DIV2K.tar
/dataset# tar xvf benchmark.tar

# python main.py --data_test Set5+Set14+B100+Urban100+DIV2K --data_range 801-900 --scale 4 --n_resblocks 32 --n_feats 256 --res_scale 0.1 --pre_train download --test_only --self_ensemble --cpu
```

#### Results

> Total (with Saving...)

- 0853x4.png (510x339, 268KB) -> 0853x4_x4_SR.png (2040x1356, 2.42MB) : 76.80s
- 1.jpg (1440x1440, 582KB) -> 1_x4_SR.png (5760x5760, 22.0MB) : 661.56s
- 2.jpg -> 2_x4_SR.png : 786.65s
- 1_small.jpg (360x360, 26.7KB) -> 1_small_x4_SR.png (1440x1440, 1.29MB) : 25.75s
- 2_small.jpg (360x360, 53.5KB) -> 2_small_x4_SR.png (1440x1440, 2.40MB) : 29.96s
