## A simple example to wrap Vue inside Nginx

Tetsing env: Win10
tutorial : https://juejin.im/post/5dbbb4df51882522c14f81a8

1. get Nginx exe from http://nginx.org/en/docs/windows.html
2. Use vue cli to have a hello world version of vue app ready
3. write up a `vue.config.js` as below

```
    module.exports = {
    // 开发环境中使用的端口
    devServer: {
        port: 8001
    },
    // 取消生成map文件（map文件可以准确的输出是哪一行哪一列有错）
    productionSourceMap: false,
    // 开发环境和部署环境的路径
    publicPath: process.env.NODE_ENV === 'production'
        ? '/'
        : '/my/',
    configureWebpack: (config) => {
        // 增加 iview-loader
        config.module.rules[0].use.push({
        loader: 'iview-loader',
        options: {
            prefix: false
        }
        })
        // 在命令行使用 vue inspect > o.js 可以检查修改后的webpack配置文件
    }
    }
```

4. `npm run build` to get vue `/dist`
5. get all files inside `/dist/` into another created folder `webapp`
6. put this `webapp/` into nginx dir
7. Inside `conf/nginx.conf`, change root (in location) to `webapp`
8. start nginx or reload to see the result


