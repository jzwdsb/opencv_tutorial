#July 19, 2017 9:30 AM

## Canny 边缘检测

* 对于很多应用来说相当于最理想边缘检测，
* 步骤
	1. 消除噪音，使用高斯过滤器，当 ksize = 5 时可能使用的高斯内核如下
		$$
			K = \dfrac{1}{159}\begin{bmatrix} 2 & 4 & 5 & 4 & 2 \\ 4 & 9 & 				12 & 9 & 4 \\ 5 & 12 & 15 & 12 & 5 \\ 4 & 9 & 12 & 9 & 4 \\ 2 				& 4 & 5 & 4 & 2 \end{bmatrix}
		$$
	2. 计算图像的梯度，与 Sobel 的过程类似，然后使用公式计算梯度强度的方向
		$$
			\begin{array}{l}\theta = \arctan(\dfrac{ G_{y} }{ G_{x} }) 				\end{array}
		$$
	3. 应用非最大抑制，这将删除不认为时边缘的像素，因此只有细线会被保留
	4. 滞后：最后一步， Canny 使用两个阈值 (上下两个阈值)
		a. 如果像素梯度高于上限阈值，则该像素被接受为边缘并保留
		b. 如果像素梯度低于下限阈值，则该像素会被拒绝
		c. 如果像素梯度介于上限和下限之间，那么只有当其与 a 类像素相连时才会被保留
	*  Canny 推荐上下限的比例应为 2 ： 1 或 3 ： 1

- - -

## `void cv::Canny()`

- - -
		void cv::Canny(
						InputArray		image,
						OutputArray		edges,
						double			threshold1,
						double			threshold2,
						int				apertureSize = 3,
						bool			L2gradient = false
						)
- - -

* 该函数使用 Canny 函数检测图像中的边缘

### 参数

- - -

* image			输入图像，深度应为 8 bit
* edges			输出图像，包含检测到的边，单通道 8 bit 深度，尺寸与原图像相同
* threshold1	滞后操作的阈值下限
* threshold2	滞后操作的阈值上限
* apertureSize	Sobel 算子的孔径大小
* L2gradient	一个标志，指示 是否使用更加精确的计算公式 $$$=\sqrt{(dI/dx)^2 + (dI/dy)^2}$$$
还是使用默认的公式$=|dI/dx|+|dI/dy|$ (L2gradient = false 即为使用默认的公式)

