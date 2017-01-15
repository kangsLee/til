#Webpack 뽀개기

Webpack 2.x 가 나왔지만, 우선은 Webpack 1.x 부터 뽀개고 시작하려 한다.

## 기본

####설치

webpack은 npm을 통해서 설치할 수 있다.

```
npm install webpack -g
```

> 실제로 프로젝트를 빌드할 때는 --save-dev 옵션으로 devDependency에 설치해주면 된다.



#### 빠른시작을 위한 기본 셋팅

webpack은 `webpack.config.js`에 기술한 내용에 따라서 동작한다.

##### 최소셋팅

```javascript
module.exports = {
  entry: {
    app: './src/main.js'
  },
  output: {
    path: path.resolve(__dirname, "build"),
    filename: 'bundle.js'
  }
}
```

> webpack이 동작하는 기본 셋팅
>
> entry point를 설정하고, 묶여진 파일이 위치할 곳을 적어주었다.
>
> 결과는 main.js의 파일이 ./build/bundle.js에 생성된다.

##### 모듈 추가

```javascript
module: {
        loaders: [
            {
                test: /\.vue$/,
                loader: 'vue-loader'
            },
	        ...
        ]
    },
```

> .vue 라는 확장자를 가진 파일에 vue-loader를 사용하여 bundle.js로 묶어준다.
>
> 마찬가지로 babel loader를 이용하면 es2015 문법이 해당 로더를 통해 트랜스파일링 되어 bundle.js 에 묶인다.





#### 사용해보기

```shell
webpack
```

> 지정한 path에 bundle.js 를 확인!



## 플러그인

### `ExtractTextPlugin`

```javascript
var ExtractTextPlugin = require("extract-text-webpack-plugin");
module.exports = {
    module: {
        loaders: [
            { test: /\.css$/, loader: ExtractTextPlugin.extract({
                fallbackLoader: "style-loader",
                loader: "css-loader"
            }) }
        ]
    },
    plugins: [
        new ExtractTextPlugin("styles.css")
    ]
}
```

> 정규식 조건에 맞는 파일들을 하나의 파일로 묶어주며, 위 예제는 .css 파일들을 style.css로 만들어준다.

**자세한 내용은 [ExtractTextPlugin](https://github.com/webpack/extract-text-webpack-plugin)**	

### `HtmlWebpackPlugIn`

```javascript
new HtmlWebpackPlugin({
      filename: 'index.html',
 	  minify: {
        removeComments: true,
        collapseWhitespace: true,
        removeAttributeQuotes: true
      },
    }),
```

html 파일을 초기 설정한 webpack output 이하 경로로 이동시켜준다.
이동 및 minify 외에도 다양한 옵션을 제공한다.

**자세한 내용은 [HtmlWebpackPlugIn](https://github.com/ampedandwired/html-webpack-plugin)**

### `UglifyJsPlugin`

```javascript
new webpack.optimize.UglifyJsPlugin({
      compress: {
        warnings: false
      }
    }),
```

bundle이 묶여진 Javascript 파일의 최소화를 도와주는 플러그인,
compress option으로 warnings (경고) 메세지를 숨길 수 있다.

**자세한 내용은 [UglifyJsPlugin](https://webpack.github.io/docs/list-of-plugins.html#uglifyjsplugin)**

### `OccurrenceOrderPlugin`

```javascript
new webpack.optimize.OccurrenceOrderPlugin()
```

빈번도에 따라 module과 chunk id를 낮게 (짧게) 할당하여 전체 파일을 줄이는데 사용된다.
webpack 2.x 스펙에 기본적으로 포함되어 있다.