### my-ndm-library

ndm ライブラリを作ってみるレポジトリ

以下の形式でインストールできるnpmライブラリを作る

```bash
npm install github:hazukit/my-ndm-library
```

### 1. プロジェクト構成

```
my-ndm-library/
├── src/
│   └── index.js
├── dist/
│   └── bundle.js (webpackで生成)
├── package.json
├── webpack.config.js
├── .gitignore
└── README.md
```

### 2. package.json の設定
package.jsonの設定を行います。

devDependenciesのあたりは、パッケージのインストール時に追加されます。
```
{
  "name": "my-ndm-library",
  "version": "1.0.0",
  "description": "Trying to create an NDM library",
  "main": "dist/bundle.js",
  "scripts": {
    "build": "webpack --mode production",
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "repository": {
    "type": "git",
    "url": "git+https://github.com/hazukit/my-ndm-library.git"
  },
  "keywords": [
    "ndm",
    "library"
  ],
  "author": "hazukit",
  "license": "MIT",
  "bugs": {
    "url": "https://github.com/hazukit/my-ndm-library/issues"
  },
  "homepage": "https://github.com/hazukit/my-ndm-library#readme",
  "devDependencies": {
    "@babel/core": "^7.25.8",
    "@babel/preset-env": "^7.25.8",
    "babel-cli": "^6.26.0",
    "babel-loader": "^9.2.1",
    "webpack": "^5.95.0",
    "webpack-cli": "^5.1.4"
  }
}
```

### 3. webpack.config.js の設定

Webpackの設定を行います。

src/index.js をエントリーポイントにして、dist/bundle.js を出力する設定にします。

```
const path = require('path');

module.exports = {
  entry: './src/main.js',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'bundle.js'
  },
  module: {
    rules: [
      {
        test: /\.js$/,
        exclude: /node_modules/,
        use: {
          loader: 'babel-loader'
        }
      }
    ]
  }
};
```

### 4. src/index.js の実装

ライブラリの主要機能をここに書きます。適当です。
```
function helloWorld() {
  return 'Hello, World!';
}

export default helloWorld;
```

### 5. ライブラリのビルド

ライブラリをビルドします。
```bash
npm install
npm run build
```
これで、dist/bundle.js が生成されます。

### 6. GitHubリポジトリのコードをコミットします。
distフォルダもコミットします。

これで、npm install github:hazukit/my-ndm-library を使ってライブラリをインストールし、他のプロジェクトで使える構成が完成します。