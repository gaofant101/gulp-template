## gulp

`gulp`是基于`Nodejs`的自动任务运行器, 她能自动化地完成`javascript/sass/less/html/image/css` 等文件的的测试、检查、合并、压缩、格式化、浏览器自动刷新、部署文件生成, 并监听文件在改动后重复指定的这些步骤.

<!-- <a herf="http://www.gulpjs.com.cn/docs/getting-started/" target="_blank">Gulp 中文网 入门指南</a> -->

## 使用

- 安装`Ruby` 环境 (`sass` 需要)
- `windows` 需要配置环境变量 `%userPath%\Ruby24-x64\bin;`
- 安装`Python` 环境 (安装`node-sass`提示)
- `windows` 需要配置环境变量 `%userPath%\Python\Python36-32\Scripts\` `%userPath%\Python\Python36-32\`
- 全局安装 `gulp` `npm install gulp -g`
- 最后一步`npm install` 安装 `package.json` 依赖包
- 起本地服务 `npm run dev` 需要修改服务端口 `gulpfile.js` 任务 `browser` 中修改端口
- 发布 `build` 执行 `npm run build`

### 配置

集成了:
- `babel` `sass` 编译
- `jshint` `csslint` 语法检测
- `rev` `revCollector` 文件`Hash`值
- `uglify` `cleanCSS` `imagemin` `minifyHTML` 文件压缩
- `postcss` `autoprefixer` `px2rem` 样式增强功能
- `cache` 任务优化,减少编译时间
- `browserSync` 起服务,浏览器实时刷新

```javascript
// 修改输出目录

const dist = isProd ? 'build' : 'dist';
```

```javascript
// 修改目录结构

const config = {
    cssSrc: 'src/styles/*.scss',
    cssDist: dist + '/styles',
    cssRev: 'rev/styles',
    jsSrc: ['src/js/*.js', '!src/js/*.min.js'],
    jsDist: dist + '/js',
    jsRev: 'rev/js',
    imgSrc: 'src/images/**/*',
    imgDist: dist + '/images',
    imgRev: 'rev/images',
    htmlSrc: 'src/*.html',
    Rev: 'rev/**/*.json',
}
```

```javascript
// 修改服务配置, 使用代理

gulp.task('browser', ()=> {
    const middleware = proxy(
        '/proxyText',
        {
            target: 'targeturl',
            changeOrigin: true,
            logLevel: 'debug',
            ws: true,
            secure: false,
        }
    );
    browserSync.init({
        port: 8031,
        https: true,
        open: false,
        server: {
            directory: true,
            baseDir: 'dist/',
        },
        middleware: [middleware],
    });
    gulp.watch(dist + '/*.html').on('change', reload);
});
```

## 参考

[gulp 中文网](http://www.gulpjs.com.cn/)   

[移动端适配方案 flexible-Demo](https://github.com/evanhunt/flexible-Demo)
