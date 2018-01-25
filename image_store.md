# 7月2日

## `cv::Mat`　类

* `Mat` 有两个数据部分，一个是矩阵头header，一个是包含像素值的矩阵matrix
* `Mat` 采用引用计数功能，普通的拷贝构造和赋值运算只拷贝header，当计数器达到零时，数据部分便会释放
* `cv::Mat::clone()` 和 `cv::Mat::copyto()`可以提供深复制
* opencv函数的输出图像的分配是自动的(除非另有说明)

## 存储方法

* RGB是最常见的，opencv标准显示系统使用BGR空间组成颜色
* HSV和HLS将颜色分为色调，饱和度和值/亮度三个分量，有时可以忽略最后一个分量使算法对亮度不敏感
* YCrCb被JPEG格式图像使用
* CIEL * a * b *是感知上统一的色彩空间，可以用来测量一种颜色到另一种颜色的距离