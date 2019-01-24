# taobaoHomePageDemo

做网页时的笔记整理，有些意识流。。

## 1. demo展示

![image](https://raw.githubusercontent.com/0rainge/taobaoHomePageDemo/master/img/demoPage.png)

## 2. 涉及的问题

1. title目的
2. Css样式引入（style link 行间样式）
3. css选择器，权重问题
4. 滚动条问题
5. 快捷键
6. display
7. 浮动
8. 居中
9. 文字竖直居中
10. 盒模型
11. 伪类与伪元素
12. 背景图片background
13. 定位：position/relative/fixed
14. 盒模型的margin和padding
15. form
16. 背景颜色的渐变 linear-gradient
17. 圆角：border-radius
18. overflow
19. input样式处理 outline/padding/text-indent
20. 文字环绕图片
21. 雪碧图
22. 盒模型的转换
23. 背景定位 

## 3. 笔记整理

### 第0步：布局

#### 0.1 布局划分

先实现结构，后实现样式。
整个页面分为五部分：顶部导航栏，顶部搜索栏，中部横向导航栏，中部图片内容展示区，右侧信息服务区域，细化如下
![image](https://github.com/0rainge/taobaoHomePageDemo/blob/fdb31458a125b24fa7e802a0d77614e9a695e3d7/img/layout.png?raw=true)

#### 0.2 布局过程

#### 设置div

通配符选择器 初始化样式

``` css
*{
    padding: 0;
    margin: 0;
    list-style: none;
    text-decoration: none;
}
```

#### 宽度高度都占满整屏幕

宽度设置占满浏览器，设置父级document-html,body,wrapper 基于父级定位

```css
html,body{
    width: 100%;
    height: 100%;
}
.wrapper{
    width: 100%;
    height: 100%;
}
```

直接设置wrapper高度，将会被内容区撑开

做样式是从外往里面实现：根据结构的嵌套关系从外往里

架构上：加上CSS结构，条理，定位比较快，分块加注释

根据class层级选中导航条的wrap部分

子集div

最外面的区域整条100% 文字内容区域是局中的子集，有

```CSS
.wrapper .top-nav-wrap{
    width: 100%;
    height:  105px ;
}
```

高度包含导航条和广告的高度

当水平超过100%就会出现横向的滚动条

内容区域超出浏览器宽度就会出现横向的滚动条
.wrapper .top-nav-wrap{
    width: 100%;
    height:  105px ;
    background-color: red;
    border: 10px solid #000000;
}

#### 滚动条问题消失：

横向滚动条消失x
overflow-x: hidden; 
给body加上；
如果没有-x 横向竖向都消失了；也不会向下滚屏

宽度100%的父集内有一个子集局中显示

#### 0.3 注意事项

##### 问题：

.wrapper .top-nav-wrap（有空格）和.wrapper.top-nav-wrap（没有空格）有什么区别？

有空格：选中的是子元素，没有空格：选中的是通过两个class并列的

##### 拿到字体颜色

![image](https://github.com/0rainge/taobaoHomePageDemo/blob/master/img/get-font-color.png?raw=true)

##### 如何看高度：

![image](https://github.com/0rainge/taobaoHomePageDemo/blob/master/img/getHeight.png?raw=true)
97+24:height97 padding-top24

导航条部分 不占100% 屏幕大于的时候做居中处理的,大范围的展示区 ,2和3中有导航条 缩小部分没有横向滚动条 

##### 下面两栏实现左右局中：

```CSS
margin: 0 auto;
```

### 第1步：顶部导航栏和广告栏

#### 1.1导航条

#### 1.1.1 导航条展示

![image](https://github.com/0rainge/taobaoHomePageDemo/blob/master/doc_img/demo01nav.png?raw=true)

#### 1.1.2 导航条实现思路

#### 分析：

首先有一个父级包含广告和导航条，然后有一个导航条自己的父级和广告的父级，父级100% 图片有固定的宽度做了局中处理，广告有a标签或者div

导航条的样式如何实现：
上一个div没有高度和宽度

导航栏实现：左侧有一组小列表,右侧有一排小列表,并列的 span a ,左边一组 右边一组 左右 ul li 无序列表 ,左侧3个li  登录注册算一个 右侧7个li

#### 1.1.3 导航条注意事项

小三角符号用 iconfont 字体图库
![image]

#### 快捷键

选中后control+D进行批量操作

control + ？ 开启注释

竖着排列 ul是块级元素 ul水平并列，左侧ul在左侧 右侧ul在右侧：左侧ul在左侧浮动 右侧ul在右侧浮动，讲ul中的li标签变成水平的 行级元素/行级块元素 display 浮动 ：将ul中的li浮动，包含两个ul 左右两个宽高，局中处理：宽度的临界值是1190px
  
浮动：脱离文档流，碰到上一个浮动元素停止

！！！坑：类名多加一个空格就会无法识别

把所有的元素水平横过来:

```HTML
.wrapper .top-nav-wrap .top-nav ul li{
    float: left;
}

```

用ul的浮动跑到左侧和右侧 ,再用ul li中的浮动 让ul把竖着的块级元素变成水平的

处理文字样式，文字包含到了导航栏的a标签


文字竖直居中：文字行高=父级的高度

文字的行高 line-height

盒模型：标准盒模型和IE模式下的盒模型


细节的问题hover 伪类 鼠标覆盖  

input search区域有伪元素

因为可能的命名冲突和权重问题，最好写选择器的时候把层级关系写上

单独选中而非批量li

所有的背景图片有大小的范围

让背景图片先出现 再以背景图片不同的class类名 替换成不同的图片

背景图片有一个相同的类名，并且都是span标签 
需要具有固定宽高，水平排列行级块元素  

选中独立的class名剔除

display inline block的对齐方式 竖直的对齐方式默认是bottom 设置居中对齐
vertical-align: middle;

#### 1.2广告条

#### 1.2.1 广告条展示

#### 1.2.2 广告条实现思路

#### 广告实现：

```HTML
            <div class="ad-wrap ">
                <div class="ad">
                    <img src="" alt="">
                </div>
            </div>

```

#### 1.2.3 广告条注意事项

广告条长度固定，多余部分换成相同颜色的背景

### 第2步：搜索框部分

#### 2.1 搜索框展示

![image](https://github.com/0rainge/taobaoHomePageDemo/blob/master/doc_img/demo02search.png?raw=true)
#### 2.2 搜索框实现思路


架构：

```CSS
        <div class="search-wrap ">
            <div class="search-con">
                <div class="logo-box"></div>
                <div class="search-box"></div>
                <div class="code-box"> </div>
            </div>
        </div>

```

padding把内容区域撑开

固定高度和宽度：1190

大于居中处理，小于做滚动条（over flow）超出滚动条消失

本来是3个块级元素div：竖直排列改为水平——行级块元素/浮动

基于下水平线进行对齐

#### 2.3 搜索框注意事项
定位：
position: relative;
 相对于自身的位置向上 top -10

相对定位 绝对定位 相对浏览器 默认值

一缩小浏览器/发生改动之后有变化

为什么： 要知道是相对谁进行定位
relative——相对自身（默认值？）进行定位

absolute——相对最近的有定位（除了默认的都行：relative absolute fixed）的父级进行定位

一般：想要被定位的元素——父级设为relative  自身设为absolute 然后通过top值等进行控制定位

基础有应用很多

盒模型的margin和padding

margin 外边距
paddign 内边距

两个a标签以背景图片的方法出现

form表单

ul li 通过表格横过来

处于pannel的上面

浮动元素脱离文档流 不能主动撑开父级，可以手动增加 

利用绝对定位：基于search  panel

跑到右边：

     position: absolute;
     top: 0;
     right: 0;

查看动作的颜色，手动触发伪类

渐变色

background: linear-gradient(to right,#ff9000 0, #ff5000 100% )
 
CSS3的内容

input的格式 outline

￼
i标签引入的字体

标签的背景图片 

多个选择器并列

``` CSS
.wrapper .search-wrap .search-con .search-box .magnifier,
.wrapper .search-wrap .search-con .search-box .camera{
    display: inline-block;
    position: absolute;
}
```

### 第3步：中间导航条

#### 3.1 中部导航条展示

![image](https://github.com/0rainge/taobaoHomePageDemo/blob/master/doc_img/demo03midNav.png?raw=true)

#### 3.2 中间导航条注意事项

h2 后面跟了三个ul 标签

缩小到一定程度会有一栏标签消失：媒体查询——子适应

一组消失比较方便

鼠标覆盖时头上出现小动画：伪元素

.wrapper .screen-nav .screen-nav-con ul li :hover::before

伪类和伪元素

伪元素只有两个：before和after，真实的添加一个元素（可以用伪元素来清除浮动）
伪类有很多：hover，可以看成是触发的一个状态

### 第4步：内容标签图片展示区域

两栏 上下 三栏 轮播图+图片展示
![image](https://github.com/0rainge/taobaoHomePageDemo/blob/master/doc_img/demo04content2.png?raw=true)

浮动 伪类 居中

文字属性：line-height text-aligin font-size font-wight

文字环绕图片

 .wrapper .screen-box .main .main-bottom .content a img{
      float: left;
 }

图片浮动之后脱离了当前的文档流 但是没有脱离之前的文本流

### 第5步：右侧信息服务区域
包括：登录，信息展示区域，论坛信息展示区域，模块信息展示区域，APP信息展示区域

![image](https://github.com/0rainge/taobaoHomePageDemo/blob/master/doc_img/demo05colRignt.png?raw=true)

登录，信息论坛等5部分

1. 雪碧图
2. 盒模型的转换
3. 背景定位

雪碧图：通过调整背景图片调整性能

设置了宽度之后 text-align

```CSS
 .wrapper .screen-box .col-right .member .member-head p a span {
     position: absolute;
     display: inline-block;
     width: 16px;
     height: 16px;
     top: 0px;
     left: 0px;
     /* border: 1px solid #000000; */
     background-image: url('./img/pics.png');
 }

 .wrapper .screen-box .col-right .member .member-head p a.icon span {
     background-position: 0 -572.5px
 }

 .wrapper .screen-box .col-right .member .member-head p a.club span {
     background-position: 0 -572.5px
 }
```

盒模型转换

因为左右两边设置了8px的padding值

      width: 100%;
      padding: 0 8px;
把标准模式下的盒模型转换为IE模式下的盒模型

标准模式下的盒模型：width+padding
IE模式下的盒模型：width（里面有padding）

``` CSS
  box-sizing: border-box;
```

选中a标签下的 .active 类
.wrapper .screen-box .col-right .notice .title li a.active

注意没有空格！

让文字下面的线变长：
    padding: 0 2px;

``` CSS

.wrapper .screen-box .col-right .notice .title li a{
    color: #3c3c3c;
    font-size: 13px;
    line-height: 20px; 
    padding: 0 2px;
 }

 .wrapper .screen-box .col-right .notice .title li a.active{
     font-weight: 700;
     border-bottom: 2px solid #f40;
 }

a中加padding width是100% 会溢出


 .wrapper .screen-box .col-right .module{
     width: 100%;
     height: 230px;
     border:  1px solid #000000; 
 }

 .wrapper .screen-box .col-right .module ul li{
     float: left;
     width: 71px;
     height: 75px;
     border: 1px solid #000000; 
     /* box-sizing: border-box; */
 }

```

受盒模型影响 边框+内容区域大于总区域，溢出：

把标准模式下的盒模型 content-box
转移成IE模型下的盒模型 border-box

inline-block 既可以设置宽高 又可以设置 text-align: center 进行居中

position 默认：距离左侧和上侧的距离