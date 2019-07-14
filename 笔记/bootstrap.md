#1.bootstrap :NO1 响应式前端框架
1. bootstrap是基于JQ的
2. 如果用到bootstrap的js必须先引入jQ。只用到样式时可以不引js文件

>JQ是js库,bootstrap/layui  前端框架

#class
1. .center-block; 块级元素在父元素中居中，（要设宽度）
2. .text-center;元素中的文本居中

#2.容器
container:固定宽度。
container-fluid:百分比宽度，100%宽
#3.栅格系统
1. .col-针对所有设备
2. .col-sm-屏幕宽度等于或大于576px
3. .col-md-屏幕宽度大于或等于768px
4. .col-lg-屏幕宽度等于或大于992px
5. .col-xl-屏幕宽度大于或等于1200px
6. 如果只写col会自动等分

##响应式列重置
	<div class="row">
        <div class="col-xs-6 col-sm-3 border1">{1}.col-xs-6 .col-sm-3Resize your viewport or check it out on your phone for an example.</div>
        <div class="col-xs-6 col-sm-3 border1">{2}.col-xs-6 .col-sm-3</div>

        <!-- <div class="clearfix visible-xs-block"></div> -->

        <div class="col-xs-6 col-sm-3 border1">{3}.col-xs-6 .col-sm-3</div>
        <div class="col-xs-6 col-sm-3 border1">{4s}.col-xs-6 .col-sm-3</div>
    </div>
当在xs视口下，4个div占了24列，正常应该分为两列，但是，当第一个div比较高时，就会出现下面的情况，第三个div并没有到第二行
![](https://i.imgur.com/LmW2XjV.png)

加上`<div class="clearfix visible-xs-block"></div>`就可以解决（clearfix清除浮动）
![](https://i.imgur.com/BYurpOG.png)


#列偏移 .col-md-offset-3

#标题 .h1,.h2.........给【行内元素】赋予h1，h2...的样式
<small></small>负标题  或者.small 

#中心内容
.lead 可以让【段落】更加突出
#强调
.text-left左对齐 .text-center .text-right
.text-muted 文本内容减弱（即颜色是灰色的）
.text-primary 文本是primary色 .text-success 文本是success色.text-info 文本是info色   .text-warning  .text-danger

#列表
.list-unstyled 移除列表样式  .list-inline 列表变为水平，且没有样式

#描述dl、dt、dd
.dl-horizontal 可以让dt，dd水平排列

#表格

#表单 
1.设置了.form-control类的input、textarea、select默认宽度都是100%

2.将一组lable和表单标签放在.form-group的div内可以获得最好的排列

3.给form标签添加form-inline，里面的标签会排成一行（在屏幕大于768的时候，小于768会垂直排列），每个表单元素的宽度为auto

