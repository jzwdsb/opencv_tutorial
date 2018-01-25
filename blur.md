# 7月7日


## `void cv::blur()`
---
            cv::blur(InputArray         src,
                     OutputArray        dst,
                     Size               ksize,
                     Point              anchor = Point(-1, -1);
                     INT                borderType = BORDER_DEFAULT
                     )
---

* 使用归一化盒式过滤器模糊图像

### 参数
---
*   src         输入图像，可以有任意数量的通道，每个通道都是独立处理的，但深度应为 CV_8U, CV_16U, CV_16S, CV_32F 或　CV_64F
*   dst         输出与src相同尺寸和类型的图像
*   ksize       模糊内核的大小
*   anchor      参考点
*   borderType  外推图像边框的像素类型


## `void cv::GaussianBlur()`
---
            void cv::GaussianBlur(InputArray    src,
                                  OutputArray   dst,
                                  Size          ksize,
                                  double        sigmaX,
                                  double        sigmaY = 0,
                                  INT           borderType = BORDER_DEFAULT
                                  )
---

* 使用高斯滤波器模糊图像
* 该函数将使用指定的高斯核与输入图像进行卷积，支持就地操作

### 参数
---
*   src         输入图像，与上面的要求相同
*   dst         输出与src相同尺寸和类型图像
*   ksize       高斯核的尺寸，　ksize.height 与　ksize.width 可以不相同，但必须是正奇数，如果为零的话用sigma计算
*   sigmaX      X方向的高斯核标准偏差
*   sigmaY      Y方向的高斯核标准偏差
*   borderType  像素外推法


## `void cv::medianBlur()`
---
            void cv::medianBlur(InputArray      src,
                                OutputArray     dst,
                                INT             ksize
                                )
---

* 使用中值滤波器模糊图像
* 该函数使用中值滤波器平滑图像，独立处理多个通道，支持就地操作

### 参数
---
*   src         输入1, 3 或　4 通道的图像，当ksize为　3 或 5 时，图像深度应为 CV_8U, CV_16U　或　CV_32F，　对于较大的光圈，深度只能为 CV_8U
*   dst         输出与src相同尺寸和类型的图像
*   ksize       光圈的孔径尺寸，必须是正奇数


### `void cv::bilateralFilter()`
---
            void cv::bilateralFilter(InputArray     src,
                                     OutputArray    dst,
                                     INT            d,
                                     double         sigmaColor,
                                     double         sigmaSpace,
                                     INT            borderType = BORDER_DEFAULT
                                     )
---

* 将双边滤镜应用于图像
* 该函数对输入图像进行双边过滤，可以很好去除噪声同时保持边缘的锐利，但是速度非常慢
* sigma：简单的情况下，两个sigma的值可以设为相同，如果很小(<10)那么过滤器的影响不会很大，如果很大(>150)，过滤器的效果会非常强大，使图像看起来很 "卡通"
* 滤波器大小：大滤波器(d > 5)非常慢，建议对实时应用使用　d = 5 ，对需要大噪声滤波的离线应用应用 d = 9　也可以
* 该滤波器不支持就地操作

### 参数
---
*   src         CV_8U 或　CV_32F，单通道或单通道的图像
*   dst         输出与src相同尺寸和类型的图像
*   d           过滤期间使用的每个像素邻域的直径，如果是非正的，将会从sigma计算得出
*   sigmaColor  过滤器在颜色空间的sigma值，sigma较大会使像素邻域中的更多颜色混合到一起，导致较大的半等色区域
*   sigmaSpace  过滤器在坐标空间的sigma值，sigma较大意味着只要颜色足够接近，距离较远的像素也会相互影响。当 d > 0时，无论sigmaSpace如何，都会指定邻域大小，否则，d 与　sigmaSpace成反比
*   borderType  像素外推法

