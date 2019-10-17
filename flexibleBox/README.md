利用flex布局，写了从一到九的麻将排版格式  
![麻将图片](https://github.com/github-gmm/demo-code/blob/master/assets/p5.jpg)  

父元素（容器）：__flex container__  

 - **flex-direction：** *子元素（项目）的排列方向，默认 ==row==*
	 ```js
	 属性值 + 作用解释
	 1. row（默认值）：主轴为水平方向，起点在左端
	 2. row-reverse：主轴为水平方向，起点在右端
	 3. colunm：主轴为垂直方向，起点在上沿
	 4. colunm-reverse：主轴为垂直方向，起点在下沿
	```
 - **flex-wrap：** *子元素（项目）的总宽度超出时是否换行，默认 ==nowrap==*
	 ```js
	属性值 + 作用解释
	 1. nowrap（默认）：不换行
	 2. wrap：换行，第一行在上方
	 3. wrap-reverse：换行，在第一行的下方
	```
 - **flex-flow：** *上两种属性的简写，默认 ==row nowrap==*
 - **justify-content：** *主轴 __main axis__ 的对齐方式，默认 ==flex-start==*
	 ```js
	属性值 + 作用解释
	 1. flex-start（默认值）：左对齐
	 2. flex-end：右对齐
	 3. center：右对齐
	 4. space-between：两端对齐，项目之间的间隔都相等
	 5. space-around：每个项目两侧的间隔相等。所以，项目之间的间隔比项目与边框的间隔大一倍。
	 6. space-evenly：项目之间的间隔都相等
	```
 - **align-content：** *交叉轴 __cross axis__ 的 __多行__ 的对齐方式，默认 ==stretch==*
	 ```js
	 属性值 + 作用解释
	 1. stretch（默认值）：如果项目未设置高度或设为auto，将占满整个容器的高度。
	 2. flex-start：交叉轴的起点对齐
	 3. flex-end：交叉轴的终点对齐
	 4. center：交叉轴的中点对齐
	 5. space-between：与交叉轴两端对齐，轴线之间的间隔平均分布。
	 6. space-around：每根轴线两侧的间隔都相等。所以，轴线之间的间隔比轴线与边框的间隔大一倍。
	```
 - **align-items：** *交叉轴 __cross axis__ 的 __单行__ 的对齐方式，默认 ==stretch==*
	 ```js
	 属性值 + 作用解释
	 1. stretch（默认值）：如果项目未设置高度或设为auto，将占满整个容器的高度。
	 2. flex-start：交叉轴的起点对齐
	 3. flex-end：交叉轴的终点对齐
	 4. center：交叉轴的中点对齐
	 5. baseline：项目的第一行文字的基线对齐。
	```

子元素（项目）：__flex item__  

 - **order：** *子元素（项目）的排列顺序，数值越小排列在前面，默认 ==0==*
	 ```js
	 属性值<integer>
	 0、1、2、3、4...
	 ```
	- **flex-grow：** *子元素（项目）的放大比例，默认 ==0==*
	 ```js
	 属性值<number>
	 0、1、2、3、4...
	 注：0不放大
	 ```
- **flex-shrink：** *子元素（项目）的缩小比例，默认 ==1==*
	 ```js
	 属性值<number>
	 0、1、2、3、4...
	 注：0不缩小
	 ```
- **flex-basis：** *子元素（项目）的占用空间，默认 ==auto==*
	 ```js
	 属性值<length>
	 1. 自定义：100px、200px、300px...
	 2. 默认大小：auto
	 ```
- **flex：** *上面三种属性的简写，默认 ==0 1 auto==*
	 ```js
	 快捷属性：优先推荐使用这个属性，而不是单独写三个属性
	 1. auto：（1 1 auto）
	 2. none：（0 0 auto）
	 ```
- **align-self：** *交叉轴 __cross axis__  上单个项目的对齐方式，默认 ==auto==*
	 ```js
	 属性值 + 作用解释
	1. auto（默认值）：和父元素上面的align-items属性保持一致
	2. flex-start：交叉轴的起点对齐
	3. flex-end：交叉轴的终点对齐
	4. center：交叉轴的中点对齐
	5. baseline：项目的第一行文字的基线对齐。
	6. stretch：如果项目未设置高度或设为auto，将占满整个容器的高度。
	 ```

麻将布局分析：  
&emsp;&emsp;首先我们可以把上面的几种排版格式分出来，可以发现有几种是一样的。  
1、①筒和⑤筒的中间：子元素在父元素里面居中对齐（水平居中、垂直居中）
 ```css
/* 父元素 */
display: flex;
justify-content: center;
align-items: center;
```

2、②筒、③筒和⑦筒的上部分：父元素排列成一列，子元素不同方式对齐
 ```css
/* 父元素 */
display: flex;
flex-direction: column;

justify-content: space-between; // 主轴两端对齐 （②筒）
align-items: center;

/* 子元素 */
align-self: center; // 交叉轴中点对齐（③筒）
align-self: flex-end; // 交叉轴终点对齐（③筒）
```

3、④筒、⑤筒、⑥筒和⑧筒：属于父元素包含一行的子元素排成一列、一行的子元素在包含两个项目排成一行，两端对齐；
 ```css
/* 父元素 */
display: flex;
flex-direction: column;

/* 子元素 */
display: flex;
justify-content: space-between;
```

4、⑨筒：需要用到超出父元素换行属性
 ```css
/* 父元素 */
display: flex;
flex-wrap: wrap;
justify-content: space-between;
align-content: space-between;
```

##### 总结  
1、flex布局与传统布局在对齐方式的写法上前者要简单许多  
2、flex布局的兼容性没有传统布局的在浏览器好，在旧的浏览器不支持  
3、flex也称之为弹性布局，可以随着窗口大小自动收缩元素的大小，不用写死  
4、flex布局在html5的功能效果显著，不过还是会有很多小问题需要自己处理  

推荐学习网址：  
 1. [Flex 布局教程：语法篇 - 阮一峰](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html)  
 2. [Flex 布局教程：实例篇 - 阮一峰](http://www.ruanyifeng.com/blog/2015/07/flex-examples.html)  
 3. [CSS3 FlexBox 布局完全指南](https://www.html.cn/archives/8629)
