# codalab-example

Codalab 介绍:

- [官网](https://worksheets.codalab.org/)
- [微软](https://www.microsoft.com/en-us/research/project/codalab/)
- [Github Wiki](https://github.com/codalab/codalab-worksheets/wiki)

## 准备

- 网络连接
- 一个 Codalab 账号和 `cl` 命令(请参考 [Quickstart](https://github.com/codalab/worksheets-examples/tree/master/00-quickstart))
- Docker (请参考 [Insatll Docker CE](https://docs.docker.com/install/))

以下将以 [Building a Semantic Parser Overnight](https://worksheets.codalab.org/worksheets/0x269ef752f8c344a28383240f7bb2be9c) 为例。

## 初始化

- 查看 worksheets 信息: `cl p 0x269ef752f8c344a28383240f7bb2be9c`
- 手动添加所有依赖的 uuid, 例如:

```sh
$ cat deps.txt
0xc8664b6bbc6d4b1c910dda0d4e15f40b
0xbc64a5bc37294e8398f4521456b69ed4
0x9053b5b245f54d29b5fec32af75995f6
0x3e57c0a4b6e544b8b2c732b5807ebc96
0x40d0664a7a3c4afc853e0509e546c6c4
0x7cff4434e6ee412b94eb602e984d1d98
0x524dadd68c5244aaabf5374bd1fc162b
```

- 下载: `for i in $(cat deps.txt); do cl down $i; done`
- 本例中`run` 是需要执行权限的，因此需要: `chmod +x run`

## 运行测试

使用方法:

```sh
# 前台运行
docker run --rm -v `pwd`:/app -w /app <image> [<command>]

# 后台运行
docker run -d --rm -v `pwd`:/app -w /app <image> [<command>]

# 交互式运行
docker run -it --rm -v `pwd`:/app -w /app <image> bash
```

其中:

- **image**: 执行镜像；点开一个测试，右侧详细信息中的 `metadata.docker_image`, 本例都是 `codalab/ubuntu:1.8`
- **command**: 执行命令，*可选*；点开一个测试，右侧详细信息中的 `command`

例如 *Ablation tests* 中第一个:

```bash
docker run --rm -v `pwd`:/app -w /app codalab/ubuntu:1.8 ./run @mode=overnight @domain=housing -OvernightFeatureComputer.featureDomains match skip-bigram root lf simpleworld -trainFrac 1 -devFrac 0 -maxExamples train:2000 test:500
```
