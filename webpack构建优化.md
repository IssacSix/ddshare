[TOC]

## webpack构建优化

构建优化需要数据支撑，如何借助工具，进行速度以及体积的分析呢？

### 1. 构建速度分析

#### 1.1 stats

```js
// dev
devServer: {
	stats: 'normal' / 'verbose'
}

// build
module.exports = {
	stats: 'normal' / 'verbose'
}
```

但是通过stats打出的时间分析，颗粒度比较粗，进一步优化



#### 1.2 speed-measure-webpack-plugin

```js 
const smp = new SpeedMeasureWebpackPlugin({
    outputFormat: 'humanVerbose',
});

module.exports = smp.wrap({
	xxx: '',
	xxx: '',
	plugins: [
		new
	]
})

```



### 2. bundle 体积分析

借助 webpack-bundle-analyzer 插件分析

```js
const { BundleAnalyzerPlugin } = require('webpack-bundle-analyzer')

module.exports = smp.wrap({
	xxx: '',
	xxx: '',
	plugins: [
		new BundleAnalyzerPlugin()
	]
})
```



### 3. 构建优化

#### 3.1 多进程构建

##### 3.1.1 happypack

```js
module.exports = {
  rules: [
    {
      test: /.js$/,
      // 1) replace your original list of loaders with "happypack/loader":
      // loaders: [ 'babel-loader?presets[]=es2015' ],
      use: 'happypack/loader',
      include: [ /* ... */ ],
      exclude: [ /* ... */ ]
    }
  ],
  plugins: [
    new HappyPack({
      // 3) re-add the loaders you replaced above in #1:
      loaders: [ 'babel-loader?presets[]=es2015' ]
    })
  ]
}
```



##### 3.1.2 thread-loader

```js
module.exports = {
  module: {
    rules: [
      {
        test: /\.js$/,
        use: [
          {
          	loader: 'thread-loader',
          	options: {
          		worker: 3 // open 3 worker
          	}
          }
        ]
      }
    ]
  }
}
```



#### 3.2 多进程压缩

terser-webpack-plugin

```js
optimization: {
    minimizer: [
      new TerserWebpackPlugin({
        parallel: true
      })
    ]
  },
```



### 3.3 分包

#### 3.3.1 splitChunkPlugin (内置)

```js
optimization: {
    splitChunks: {
      cacheGroups: {
        commons: {
          minChunks: 2,
          name: 'vendors',
          chunks: 'all'
        },
      },
    }
  }
```



#### 3.3.2 DllPlugin

```js
// dll.webapck.config.js example
const path = require('path')
const webpack = require('webpack')

module.exports = {
    mode: 'none',
    entry: {
        library: [
            'react',
            'react-dom'
        ]
    },
    output: {
        filename: '[name]_[chunkhash].dll.js',
        path: path.join(__dirname, '../library'),
        library: '[name]'
    },
    plugins: [
        new webpack.DllPlugin({
            context: path.join(__dirname, '../library'),
            name: '[name]_[hash]',
            path: path.join(__dirname, '../library/[name].json')
        })
    ]
 }

// prod.webpack.config.js
new webpack.DllReferencePlugin({
  context: path.join(__dirname, '../library'),
  manifest: require(path.join(__dirname, '../library/library.json'))
}),
```



### 4. 充分利用缓存

有多种方式

1. TerserWebpackPlugin 设置cache:true
2. HardSourceWebpackPlugin

```js
plugins: [
	new HardSourceWebpackPlugin()
]
```



### 5. 缩小构建目标

```js
resolve: {
    alias: {
      'react': path.resolve(__dirname, '../node_modules/react/umd/react.production.min.js'),
      'react-dom': path.resolve(__dirname, '../node_modules/react-dom/umd/react-	dom.production.min.js'),
    },
    extensions: ['.js'],
    mainFields: ['index']
  }
```



### 6. tree shaking 擦去无用js、css代码

#### 6.1 js tree shaking

在 mode: 'production' 下，自动进行tree shaking 优化，优化规则

1. 一个module中所有方法都没被调用
2. 只定义，不调用的function
3. 只定义未使用的变量

#### 6.2 css tree shaking

PurgecssPlugin

```js
plugins: [
		new PurgecssPlugin({
      paths: glob.sync('xxxx/xxx/xx', { nodir: true }),
    })
]
```



### 7. 图片压缩

```js
{
	module: {
		rules: [
			{
				test: /.(png|jpg|gif|jpeg)$/,
				use: [
					{
						loader: 'url-loader'
						options: {}
					},
					{
						loader: 'image-webpack-loader',
						options: {}
					}
				]
			}
		]
	}
}
```









