# 7月8日

## 　`void cv::dilate()`
--------------------
            void cv::dilate(InputArray      src,
                            OutputArray     dst,
                            InputArray      kernel,
                            Point           anchor = Point(-1, -1),
                            INT             iterations = 1,
                            INT             borderType = BORDER_DEFAULT,
                            const Scalar&   borderValue = morphologyDefaultBorderValue()
                            )
---

* 使用特定的结构膨胀图像
* 该函数使用特定的结构膨胀图像，具体是在kernel下的参考点取局部最大值
* 每个通道独立处理，支持就地操作

### 参数
---
* src           输入图像，通道数任意，但是深度应该是 CV_8U, CV_16U, CV_16S, CV_32F, CV_64F之一
* dst           输出图像，与输入图像有相同的尺寸和类型
* kernel        用于扩张的结构元素，如果　element = Mat()，则是用　3 × 3　的结构元素，可以使用 `getStructuring()`创建内核
* anchor        参考点在kernel的位置，Point(-1, -1)表示参考点位于kernel中央
* iterations    函数执行的膨胀操作次数
* borderType    像素外推法
* borderValue   边界值


## `void cv::erode()`
---
            void cv::erode(InputArray       src,
                           OutputArray      dst,
                           InputArray       kernel,
                           Point            anchor = Point(-1, -1),
                           INT              iterations = 1,
                           INT              borderType = BORDER_DEFAULT,
                           const Scalar&    borderValue = morphologyDefaultBorderValue()
                           )
---

* 使用特定的元素腐蚀图像
* 该函数使用特定的结构腐蚀图像，具体是参考点取结构元素中的最小值
* 每个通道单独处理，支持就地操作

### 参数
---
* src           输入图像，要求与dilate相同
* dst           输出图像，与上相同
* kernel        用于扩张的结构元素，与上相同
* anchor        参考点的未知
* iterations    函数执行的腐蚀操作的次数
* borderType    像素外推法
* borderValue   像素值


## `void cv::getStructuringElement()`
---
            void cv::getStructuringElement(INT      shape,
                                           Size     ksize,
                                           Point    anchor = Point(-1, -1)
                                           )
---

* 返回形态操作的指定大小的和形状的结构元素
* 可以构造并返回传递给`cv::erode`，　`cv::dilate`，`cv::morphologyEx`

### 参数
---
* shape         元素值可以取 `MORPH_RECT`，　`MORPH_CROSS`和`MORPH_ELLIPSE`分别表示矩形，十字和椭圆
* ksize         结构元素的大小
* anchor        参考点的位置，只有十字性内核的形状取决于参考点的位置，其他情况下参考点只调节形态操作的结果发生了多少偏移