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
其中 `worksheet_spec`:

- `name`: sempre-overnight-acl2015c
- `uuid`: 0x269ef752f8c344a28383240f7bb2be9c

二者完全等价。以下全部使用 `uuid` 作为 `worksheet_spec`

## 初始化

- 查看 worksheets 信息: `cl p 0x269ef752f8c344a28383240f7bb2be9c`
- 列出依赖：`cl ls -w 0x269ef752f8c344a28383240f7bb2be9c`
- 下载依赖: `for i in $(cl ls -uw 0x269ef752f8c344a28383240f7bb2be9c); do cl down $i; done`
- 本例中 `./run` 是需要执行权限的，因此需要: `chmod +x run`

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
