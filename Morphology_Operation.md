# 7月9日

# `void cv::morphologyEx()`
---
            void cv::morphology(InputArray      src,
                                OutputArray     dst,
                                INT             op,
                                InputArray      kernel,
                                Point           anchor = Point(-1, -1),
                                INT             iterations = 1,
                                INT             borderType = BORDER_CONSTANT,
                                const scalar&   borderValue = morphologyDefaultBorderValue()
                                )
---

* 该函数提供高级的形态学操作，具体操作类型由　op 参数提供
* 高级的形态学操作是以膨胀和腐蚀为基础进行的
* 任何操作都支持就地操作，当图像是多通道时，每个通道都会单独的处理

### 参数
---
* src           输入图像，通道数任意，但是图像深度应该是 CV_8U, CV_16U, CV_16S, CV_32F, CV_64F之一
* dst           输出图像，与输入相同尺寸和类型
* op            形态操作的类型
* kernel        结构元素，通过`cv::Mat cv::getStructuringElement()`得到
* anchor        参考点的位置，默认是在图像中央
* iterations    腐蚀和膨胀的次数
* borderType    像素外推法
* borderValue   边界的常量像素值，默认值有特殊含义


# 形态学操作

* 所有形态学操作类型都在 `cv::MorphTypes` 枚举类型中定义


## open(开运算)

### `cv::MorphTypes::MORPH_OPEN`

* 先将图像腐蚀，再将图像膨胀得到的
* 用于去除小物体(假设物体在黑暗的前景上是明亮的)

---
## close（闭运算）
### `cv::MorphTypes::MORPH_CLOSE`

* 与open(开运算)相反，是先将图像膨胀，再将图像腐蚀得到的
* 用于去除小孔(假设小孔是在明亮的前景上是黑暗的)

---
## Morphological Gradient(形态学梯度)
### `cv::MorphTypes::MORPH_GRADIENT`

* 将图像分别做膨胀和腐蚀运算后两结果做差得到
* 用于找到物体的轮廓
---
## Top Hat(礼帽)
### `cv::MorphTypes::TOPHAT`

* 原图像与图像做开运算后做差得到

---
## Black Hat(黑帽)
## `cv::MorphTypes::BLACKHAT`

* 图像做闭运算与原图像做差得到

