### CRNN

环境配置

```bash
#依赖库
pip install pyyaml，easydict，opencv-python，torch，torchvision
```

###  数据结构

#### Image

```bash
#/data/img
YT4781508601922_c.jpg
YT4780969904156_a.jpg
```

#### label

```bash
#/lib/dataset/txt/train.txt
#/lib/dataset/txt/test.txt
YT4781508601922_c.jpg 13718333065
YT4780969904156_a.jpg 18387504894
YT4783157963048_e.jpg 18712892065
YT4782906609375_d.jpg 15227376615
YT4783337132719_c.jpg 18643431985
YT4782654683779_a.jpg 13707288872
YT4778918252899_d.jpg 13913109992
YT4784300572415_e.jpg 16650113285
YT4780338010986_b.jpg 18220462612
```

#### build_label_txt

```
#generate_txt.py
data/label_test/    -->  /lib/dataset/txt/train.txt
data/label_train/   -->  /lib/dataset/txt/test.txt
```

### 修改模型参数

```bash
vim lib/config/OWN_config.yaml
datasets：
    ROOT: "data/img"
    JSON_FILE: {'train': 'lib/dataset/txt/train.txt', 'val': 'lib/dataset/txt/test.txt'}
    ALPHABETS: '0123456789'
MODEL:
  IMAGE_SIZE:
    OW: 160. # 除非输入数据全部是统一尺度的，否则就固定设置为160
    H: 32 #输入高度固定为32
    W: 160   # 模型的输入尺度160
其他参数为默认值。
```

### Train

```
python train.py --cfg lib/config/OWN_config.yaml
```

#### Tensorboard

```bash
 cd output/OWN/crnn/xxxx-xx-xx-xx-xx/
 tensorboard --logdir log/
```

### Test

```
python demo.py --image_path images/test.png --checkpoint output/checkpoints/mixed_second_finetune_acc_97P7.pth
```

