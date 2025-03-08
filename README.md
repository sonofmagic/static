# 利用 Github 构建你自己的免费图床

> 本文用到了 Github + jsdelivr + Picgo 这些工具

大体的流程非常简单，使用 `Picgo` 上传图片，利用 `Github` 的 `repo` 作为存储图床再通过 `jsdelivr` `cdn` 进行加速

## 1. 安装 Picgo

[`Picgo`](https://github.com/Molunerfinn/PicGo) 是一个图片上传客户端，支持许多平台的图片上传。

首先我们去 [PicGo/releases](https://github.com/Molunerfinn/PicGo/releases) 下载最新版本的 `PicGo`，比如我下载的是 `2.4.0-beta.9` 版本。

我是 `Mbp` 所以下载的 `PicGo-2.4.0-beta.9-arm64.dmg`, 其他平台自己看 `CPU` 指令集架构选择。

然后安装`mac` 会显示安装安装包损坏，然后看 [FAQ](https://github.com/Molunerfinn/PicGo/blob/dev/FAQ.md) 发现是由于软件包没有签名，所以会被 macOS 的安全检查所拦下导致的。

所以需要信任开发者，会要求输入密码, 执行:

```sh
sudo spctl --master-disable
```

然后放行 `PicGo` :

```sh
xattr -cr /Applications/PicGo.app
```

然后就能正常打开。

## 2. 设置 Github

流程也很简单，创建一个仓库，然后创建一个 `PAT` 给一下仓库权限，然后在客户端设置一下即可。

详见 [`Picgo` Github图床文档](https://picgo.github.io/PicGo-Doc/zh/guide/config.html#github%E5%9B%BE%E5%BA%8A)

## 3. jsdelivr

默认情况下，国内访问 `Github` 资源会被墙，所以需要 `jsdelivr` `cdn` 进行分发。

首先访问 [jsdelivr官网](https://www.jsdelivr.com/?docs=gh)，发现它有 `Github` 加速，路径下方所示:

```sh
https://cdn.jsdelivr.net/gh/user/repo@version/file
```

然后填充一下你自己的用户和 `repo` 名，比如这个仓库就是:

```sh
https://cdn.jsdelivr.net/gh/sonofmagic/static/{your_path}
```

然后把对应的配置，在 `Picgo` 填充即可。

![](https://cdn.jsdelivr.net/gh/sonofmagic/static/v1/picgo-github-setting.png)

## 例子

![](https://cdn.jsdelivr.net/gh/sonofmagic/static/logo.png)

```md
![](https://cdn.jsdelivr.net/gh/sonofmagic/static/logo.png)
```

## 总结

最后总结一下方案的优势和劣势

### 优势

1. 免费

### 劣势

1. 国内访问有可能被墙
2. `Repo` 后期会很大，假如不小心上传敏感资源，不懂 `git` 的小白不会真正删除里面的资源。
3. 仓库整个资源可以被一键打包带走