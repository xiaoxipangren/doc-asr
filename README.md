# Asr-tool docker镜像安装使用指南

## 系统要求

### Docker

推荐安装17.09.0-ce\(community edition\)或更高版本，具体安装步骤请参考[https://docs.docker.com/install/](https://docs.docker.com/install/ "官方文档")

# 安装

只需要将asr-tool的docker镜像pull到本地便完成安装：

```bash
sudo docker pull registry.cn-hangzhou.aliyuncs.com/nationalchip/asr:jieba
```

_提示：镜像较大，推荐使用阿里云的镜像加速服务，具体参考_[_http://blog.csdn.net/yp090416/article/details/75107938_](http://blog.csdn.net/yp090416/article/details/75107938)

# 运行容器

```bash
#镜像重tag为 asr:jieba
sudo docker tag registry.cn-hangzhou.aliyuncs.com/nationalchip/asr:jieba asr:jieba 

#删除原有的同名asr容器
sudo docker stop asr
sudo docker rm asr

#以asr为容器名运行该镜像
sudo docker run --name asr -dit asr:jieba

```

# 执行Asr tool

```bash
#拷贝语料，text为文本格式的按行分割关键词或语句的语料文件
sudo docker cp text asr:/asr/

#直接进入容器内部，调用asr工具
sudo docker exec -it asr bash

#以下命令为容器内命令
$:cd /asr
#查看asr tool简易帮组文档
$:cat README

#调用asr工具训练，
$:./run.sh text

#训练结果保存在/asr/data/search_Graph中，包括words.txt TLG.fst两个文件
#退出容器
$:exit

#拷贝结果到本地
sudo docker cp asr:/asr/data/search_Graph/words.txt ./
sudo docker cp asr:/asr/data/search_Graph/TLG.txt ./

```



