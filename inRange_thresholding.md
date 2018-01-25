# 7月16日

## `void cv::inRange()`
---
            void cv::inRange(InputArray         src,
                             InputArray         lowerb,
                             InpurArray         upperb,
                             OutputArray        dst
                             )
---

* 检查数组元素是否位于另外两个数组之间
* 函数用下面的方式检查元素是狗在区间内
    1. 单通道的每个元素

            dst(I) = lowerb(I) <= src(I) <= upperb(I)
    2. 对于多通道的每个元素

            dst(I) = lowerb(I1) <= src(I1) <= upperb(I1)
                        &&  lowerb(I2) <= src(I2) <= upperb(I2)
* 因此，如果像素在区间内的话酒鬼被设置为 255 ，否则就会设置为 0
* 如果 lowerb 或 upperb　是 cv::scalars , 那么下标就可以省略

### 参数
---
* src           输入图像
* lowerb        区间的下界或一个标量
* upperb        区间的上界或一个标量
* dst           输出图像，与src有相同的尺寸，深度为 CV_8U