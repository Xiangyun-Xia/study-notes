#### SCSS简介

SCSS 是 Sass 3 引入新的语法，其语法完全兼容 CSS3，并且继承了 Sass 的强大功能。也就是说，任何标准的 CSS3  样式表都是具有相同语义的有效的 SCSS 文件。另外，SCSS 还能识别大部分 CSS hacks（一些 CSS  小技巧）和特定于浏览器的语法，例如：[古老的 IE `filter` 语法](http://msdn.microsoft.com/en-us/library/ms532847%28v=vs.85%29.aspx#Defining_Visual_Filt)。

由于 SCSS 是 CSS 的扩展，因此，所有在 CSS 中正常工作的代码也能在 SCSS 中正常工作。也就是说，对于一个 Sass  用户，只需要理解 Sass 扩展部分如何工作的，就能完全理解 SCSS。大部分扩展，例如变量、parent references 和  指令都是一致的；唯一不同的是，SCSS 需要使用分号和花括号而不是换行和缩进。

```scss
.my-table {
  .paper-title {
    cursor: pointer;
    &:hover {
      color: #5ad29d;
    }
  }
  .table-btn {
    font-size: 14px;
    color: #5ad29d;
    &:hover {
      color: #28D489
    }
  }
}
```

#### SCSS使用

- 安装

  > 参考：[如何安装Sass](https://www.sass.hk/install)

- 编译
  1. 编译方式
     - 命令行编译
     - 软件编译
     - 自动化编译等
  2. 输出方式
     - nested 编译排版格式
     - expanded 编译排版格式
     - compact 编译排版格式
     - compressed 编译排版格式

#### SCSS语法

- 使用变量
- 选择器
- 嵌套及混合
- 编程式语法

> 参考： 
>
> 1. [快速入门](https://www.sass.hk/guide)
> 2. [scss常见用法](https://blog.csdn.net/leadn/article/details/78562873?locationNum=6&fps=1)