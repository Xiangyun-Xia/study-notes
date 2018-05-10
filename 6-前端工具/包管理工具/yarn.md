## Yarn

#### 优点

- yarn.lock确保使用的库的版本相同；
- 运行速度得到了显著的提升，整个安装时间也变得更少；
- 无需互联网连接就能安装本地缓存的依赖项，它提供了离线模式；
- 允许合并项目中使用到的所有的包的许可证；
- [一文看懂npm、yarn、pnpm之间的区别](http://geek.csdn.net/news/detail/197339)

#### 使用

- [`yarn add`](https://yarnpkg.com/zh-Hans/docs/cli/add)：为当前正在开发的包新增一个依赖包；
- [`yarn init`](https://yarnpkg.com/zh-Hans/docs/cli/init)：初始化包；
- [`yarn install`](https://yarnpkg.com/zh-Hans/docs/cli/install)：安装`package.json` 文件里定义的所有依赖包；
- [`yarn publish`](https://yarnpkg.com/zh-Hans/docs/cli/publish)：发布一个包到包管理器；
- [`yarn remove`](https://yarnpkg.com/zh-Hans/docs/cli/remove)：从当前包里移除一个未使用的包。