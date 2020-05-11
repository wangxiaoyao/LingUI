# LingUI

A React.js UI Toolkit for Web.


## 规范

- 1 文件夹命名：components下的子文件夹为单独的组件。名称统一大写开头（PascalCase）
- 2 文件命名：属于Api的，统一加上Api后缀,   *.less统一使用kebab-case命名风格。（&-）


## webpack配置

### less以及css modules

> 使用less进行css的解析。并配置localIdentName 作为class的命名规则：就可以实现class 命名了 在生产环境下修改规则，生成更短的 class 名，可以提高 CSS 的压缩率。选择base64的5个字符。

```
// 添加 less 解析规则
const lessRegex = /\.less$/;
const lessModuleRegex = /\.module\.less$/;

// Less 解析配置:注意在file-loader 的解析规则上面，以及配置localIdentName
{
  test: lessRegex,
  exclude: lessModuleRegex,
  use: getStyleLoaders(
    {
      importLoaders: 2,
      modules: {
        localIdentName: "[path][name]__[local]--[hash:base64:5]",
      },
      sourceMap: isEnvProduction && shouldUseSourceMap,
    },
    "less-loader"
  ),
  sideEffects: true,
},
{
  test: lessModuleRegex,
  use: getStyleLoaders(
    {
      importLoaders: 2,
      sourceMap: isEnvProduction && shouldUseSourceMap,
      modules: true,
      getLocalIdent: getCSSModuleLocalIdent,
    },
    "less-loader"
  ),
},
```

```
## 配置localIdentName
modules:true 换成：

modules: {
  localIdentName: "[path][name]__[local]--[hash:base64:5]",
},
```
 

