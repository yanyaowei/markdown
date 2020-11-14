### webpack loader注意事项

webpack1.X可以不带-loader，如：

```js
{test: /\.css$/ ,use: ['style','']}
```

但是webpack2.X,3.X...都需要带-loader

```js
{test: /\.css$/ ,use: ['style-loader','css-loader']}
```

