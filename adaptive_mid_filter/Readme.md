# Readme

刘暢: 19309088  

吴甜裕: 18307060

## 自适应的中值滤波器

### 简介

* 属于自适应滤波器, 参数为滤波模板的大小和滤波器模板最大值
* 主要用来处理脉冲噪声, 尽量保持非脉冲噪声细节
* 相比于中值滤波器, 其工作流程增加了判断是否是校验噪声以及扩大模板范围, 具体来说, 可以分为
  * 找到非椒盐噪声的中值: 在`init kernel size`的范围内确定中值, 最大值, 最小值, 判断是否是椒盐噪声, 如果是的话就扩大`kernel size`尝试找到非椒盐噪声的中值点
  * 找到中值后检查窗口本身的像素值是否是椒盐噪声, 如果是的话输出中值点, 不是的话输出原像素值

### 结果

* 实现的函数 `void mid_filter(Mat &src, Mat &dst, int kernel_size, int max_size)`
  * 参数是输入输出图片, 起始模板大小, 最大可允许搜索模板大小

* 效果对比

| 原图                         | 自适应滤波的结果              | OpenCV中值滤波结果                  |
| ---------------------------- | ----------------------------- | ----------------------------------- |
| ![](lena256-pepper&salt.bmp) | ![](result/中值滤波结果.png)  | ![](result/中值滤波OpenCV结果.png)  |
| ![](girl256-pepper&salt.bmp) | ![](result/中值滤波结果2.png) | ![](result/中值滤波OpenCV结果2.png) |

可以看出经过自适应中值滤波的结果图像细节保存的很好, 且消除噪声的能力也很强, 达到了设计的目的