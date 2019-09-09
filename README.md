<h1 align="center">Welcome to webpack-merge-config 👋</h1>
<p>
[![npm version](https://badge.fury.io/js/webpack-merge-config.svg)](https://www.npmjs.com/package/webpack-merge-config)
  <img src="https://img.shields.io/badge/version-1.0.0-blue.svg?cacheSeconds=2592000" />
  <a href="https://github.com/YIZHUANG/webpack-merge-config">
    <img alt="Documentation" src="https://img.shields.io/badge/documentation-yes-brightgreen.svg" target="_blank" />
  </a>
  <a href="https://github.com/YIZ">
    <img alt="License: MIT" src="https://img.shields.io/badge/License-MIT-yellow.svg" target="_blank" />
  </a>
</p>

> Merges webpack config in a smarter way as an alternative to webpack-merge that promotes code reuse.

## Inspiration

See the followings:

```
const config1 = {
  module: {
    rules: [
      {
        test: /\.css$/,
        loader: [
          {
            loader: "css-loader",
            options: { importLoaders: 1 },
          },
        ],
      }
    ],
  },
}
const config2 = {
  module: {
    rules: [
      {
        test: /\.css$/,
        loader: [
          {
            loader: "style-loader"
          },
        ],
      }
    ],
  },
}

const finalConfig = merge(config1, config2);

In webpack-merge the output will be:
  module: {
    rules: [
      {
        test: /\.css$/,
        loader: [
          {
            loader: "css-loader",
            options: { importLoaders: 1 },
          },
        ],
      },
      {
        test: /\.css$/,
        loader: [
          {
            loader: "style-loader"
          },
        ],
      }
    ],
  },

In webpack-config-merge it will become:
  module: {
    rules: [
      {
        test: /\.css$/,
        loader: [
          {
            loader: "style-loader"
          },
          {
            loader: "css-loader",
            options: { importLoaders: 1 },
          },
        ],
      }
    ],
  },
```

## Install

```
$ npm install webpack-config-merge --save-dev

const merge = require('webpack-config-merge');
module.exports = merge(config1, config2, {
  priority: 2
});
// if priority is 2, the lib will use unshift instead of push, this is useful for CSS related config. //              //Otherwise, leave it empty.
```

## More examples

1.

```
const config1 = {
  plugins: [
    new HtmlWebPackPlugin({
      filename: 'index.html'
    })
  ]
}

const config2 = {
  plugins: [
    new HtmlWebPackPlugin({
      hash: true
    })
  ]
}
const finalConfig = merge(config1, config2);

Output:
const finalConfig = {
    plugins: [
    new HtmlWebPackPlugin({
      filename: 'index.html',
      hash: true
    })
  ]
}

```

2.

```

const config1 = {
  module: {
    rules: [
      {
        test: /\.scss$/,
        loader: [
          {
            loader: "style-loader"
          },
        ],
      }
    ],
  },
  plugins: [
    new CopyWebpackPlugin([
      { from: '/1', to: '/2' },
    ])
  ]
}

const config2 = {
  module: {
    rules: [
      {
        test: /\.scss$/,
        loader: [
          AnyLoader
        ],
      }
    ],
  },
  plugins: [
    new CopyWebpackPlugin([
      { from: '/3', to: '/4' },
    ])
  ]
}

const finalConfig = merge(config1, config2);

Output:
const finalConfig = {
  module: {
    rules: [
      {
        test: /\.scss$/,
        loader: [
         {
            loader: "style-loader"
          },
          AnyLoader
        ],
      }
    ],
  },
  plugins: [
    new CopyWebpackPlugin([
      { from: '/1', to: '/2' },
      { from: '/3', to: '/4' },
    ])
  ]
}
```

## Author

👤 **YIZHUANG**

- Github: [@YIZHUANG](https://github.com/YIZHUANG)

## Show your support

Give a ⭐️ if this project helped you!

## 📝 License

Copyright © 2019 [YIZHUANG](https://github.com/YIZHUANG).<br />
This project is [MIT](https://github.com/YIZ) licensed.

---

_This project structure was generated with ❤️ by [git-repo-npm-bootster](https://github.com/YIZHUANG/git-repo-npm-bootster)_
