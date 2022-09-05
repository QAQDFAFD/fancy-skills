# ANIPLEX 的转动效果

![](https://picgo-use-images.oss-cn-shanghai.aliyuncs.com/images/20220522112641.png)

## 总结：
* 字母就是单纯的旋转
* 外框一开始都在一起，然后向右移动，且过程中放缩旋转

## 知识点：

### 1.flex-direction

`flex-direction` 指定了内部元素是如何在flex容器中布局的，定义了主轴的方向（正方向或者反方向）

> <span style="background-color:#C1FFC1">Tip：HTML dir属性：</span>
>
> <span style="background-color:#C1FFC1">规定了在盒子中文字的方向</span>
>
> ```html
> <!DOCTYPE html>
> <html>
> <body>
> 
> <p dir="rtl">Write this text right-to-left!</p>
> 
> </body>
> </html>
> ```
>
> 效果：
>
> ![image-20220522151038225](https://picgo-use-images.oss-cn-shanghai.aliyuncs.com/images/image-20220522151038225.png)
>
> ```
> 
> ```
>
> ```html
> <!DOCTYPE html>
> <html>
> <body>
> 
> <p dir="ltr">Write this text right-to-left!</p>
> 
> </body>
> </html>
> 
> ```
>
> 效果：
>
> ![image-20220522151125497](https://picgo-use-images.oss-cn-shanghai.aliyuncs.com/images/image-20220522151125497.png)

flex-direction的值：

* row（默认）
* row-reverse
* column
* column-reverse

**例子：**

![image-20220522151505500](https://picgo-use-images.oss-cn-shanghai.aliyuncs.com/images/image-20220522151505500.png)

## 2.perspective

<span style="background-color:#C1FFC1">n. （观察问题的）视角</span>

`perspective` 指定了观察者与`z=0`平面的距离，使得具有三维位置变换的元素产生透视的效果。 **z>0 的三维元素比正常大，而 z<0 时则比正常小，大小程度由该属性的值决定。**

> 三维元素在观察者后面的部分不会绘制出来，即 z 轴坐标值大于 `perspective` 属性值的部分。
>
> **三维坐标轴**：遵循右手定则
>
> ![image-20220522152830906](https://picgo-use-images.oss-cn-shanghai.aliyuncs.com/images/image-20220522152830906.png)
>
> 所以可以判断z轴的位置：
>
> ![image-20220522153046479](https://picgo-use-images.oss-cn-shanghai.aliyuncs.com/images/image-20220522153046479.png)

[css3系列之详解perspective - 杨耿 - 博客园 (cnblogs.com)](https://www.cnblogs.com/yanggeng/p/11285856.html)

### 3.translate()

**translateX()**

一个参数，正数右移

**translateY()**

一个参数，正数下移

**translateZ()**

一个参数，参数越大，图片越大

**translate()**

两个参数：X,Y

第二个参数不填默认为0

**translate3d()**

三个参数：X，Y，Z

三个参数都是必填













