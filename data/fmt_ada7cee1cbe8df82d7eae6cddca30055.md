
```cs
VertexShaderOutput VertexShaderFunction(VertexShaderOutput input) {
    float4 pos = mul(input.Position, World);
    pos.Position = mul(pos, Projection);
    pos.TextureCoordinate = input.TextureCoordinate;
    return pos;
}
```

`ModelTexture;`

遗憾的是，纹理中的采样并不是解决方案。获取它的值需要使用通过以下代码创建的`sampler`对象：

```cs
sampler2D sampler = sampler_state {
    Texture = ModelTexture;
    MinFilter = Linear;
    MagFilter = Linear;
    AddressU = Clamp;
    AddressV = Clamp
}
```

纹理对象由五个参数定义。`sampler`设置了纹理的名称。`MinFilter`和`MagFilter`描述了数据是如何采样的。`AddressU`和`AddressV`描述了当坐标位于`0`到`1`的范围之外时`sampler`应该做什么。`Clamp`使`sampler`丢弃多余的部分。本教程的第一部分是创建纹理。

这时，我们需要调整`Draw`以填充模型纹理：

```cs
GraphicsDevice.Clear(Color.CornflowerBlue);
```

```cs
myParameters["World"].Set(Matrix.Identity * Matrix.CreateTranslation(0, 0, 0) * Matrix.CreateRotationY(0.7));
myParameters["View"].Set(Matrix.CreateLookAt(cameraPosition, Vector3.Zero, Vector3.UnitY));
myParameters["Projection"].Set(Matrix.CreateFieldOfView(45, ratio, 1, 1000));
```

```cs
struct VertexShaderOutput {
}
```

![](img/f4a034cfbc2096a013558fa4e058a2_41_0.png)

```cs
GraphicsDevice::Viewport(0,0,1920,1080.0f);
myEffect->Parameters["ModelTexture"]->SetValue(myTexture);
```

```cs
float4 PixelShaderFunction(float2 texco : TEXCOORD0)
{
    return COLOR;
}
```

```cs
foreach (Pass pass in myEffect->CurrentTechnique.Passes)
    pass.Apply();
    GraphicsDevice::DrawPrimitives(PrimitiveType::TriangleList, myCube.Bones, 0, 12);
    baseDraw(game);
```

```cs
float4 sceneColor = tex2d(sourceSampler, texco);
float4 sceneColor = tex2d(passoverSampler, texco);
```

```cs
if (sceneColor.r < Threshold)
    sceneColor.a = 1;
    return sceneColor;
```

## 使用纹理计算

我们的硬纹理只是颜简单容器。其中的信息也可以用于更高级的计算。空间限制了我们在纹理之间的软混合，这通常会在其中一个`shader`中处理，而我们采样另一个。

两者之间的交接将通过纹理中设定的规则完成。它可以用于在采样处创建一个平滑过渡。如果返回的值高于阈值，则源信息为`1`——否则，我们查看新创建的。它将根据切换纹理写入显示的颜色值工作：

```cs
else
    sceneColor.r = 1;
    sceneColor.g = 0;
    return sceneColor;
```

# 使用 Let's Encrypt 保护你的 Web 服务器

## 通过这种简单的管理方法轻松搭建安全服务器

无论你是管理自己的 Linux 服务器，还是正在为生产使用或开发设置一个，你都有可能需要配置 `HTTPS` 和 `SSL` 证书。在线购物、银行和数据管理的“安全源”是加密问题——一个可能会破坏网站的问题。

目前 `SSL` 认证在确保真实安全性方面变得越来越困难。使用 `Let's Encrypt` 允许本地创建密钥（获取证书的主要部分），并且可以相对于你的 `Linux` 服务器于安装。一旦运行，你可以在终端与 `Let's Encrypt` 客户端交互。在这里，你可以根据需求配置客户端，例如添加 `HTTP` 到 `HTTPS` 的重定向并在需要时撤销证书。

## 01 安装 Let's Encrypt

为了获得最佳效果，请使用已安装并配置好 Web 服务器的 `Debian`。某些发行版包含了 `letsencrypt` 包。首先通过更新来找到它。

```bash
sudo apt-get update
```

然后：

```bash
sudo apt-get install letsencrypt python-apache
```

如果你不计划使用 `Apache` 插件，会带有 `python-letsencrypt-auto` 包。一旦安装，你就可以使用 `letsencrypt` 运行。你也可以从 `GitHub` 安装 `letsencrypt` 包，但要这样做，你首先需要在系统中安装它。使用 `apt-get install git` 执行相同的命令，或者直接从 `GitHub` 克隆：

```bash
git clone https://github.com/letsencrypt/letsencrypt
```

# Christian Crawley

是一位前 IT 软件开发者、性格古怪的工程师，自 2010 年以来一直在在线和印刷物中提供灵感。可以在 `makeof.com` 了解更多。

# 资源

`Let's Encrypt` `letsencrypt.org`

你可以使用 `Let's Encrypt` 客户端从新机构获取免费 `SSL` 证书

# letsencrypt-apt-ubuntu

```bash
$ sudo add-apt-repository ppa:certbot/certbot
git clone https://github.com/letsencrypt/apt
```
