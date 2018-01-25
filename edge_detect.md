# 7月18日

## 边缘检测

* 重要的卷积的应用之一就是计算图像的导数
* 观察图像的边缘可以看到，在图像的边缘像素的强度是以非常强烈的形式变化

> ![](Sobel_Derivatives_Tutorial_Theory_0.jpg)

* 下面的图显示啦一个 1D 图像的在边缘上像素变化趋势

> ![](Sobel_Derivatives_Tutorial_Theory_Intensity_Function.jpg)

* 如果用一阶导数的形式可以更容易看出，边缘上的跳跃显示为一阶导数上的极大值
> ![](Sobel_Derivatives_Tutorial_Theory_dIntensity_Function.jpg)

* 因此可以通过定位其梯度高于周围的像素推导出一种边缘检测的算法

## sobel 边缘检测

* sobel 是一个离散差分算子，计算图像强度函数的梯度的近似值
* sobel 结合来高斯平滑和微分

### 公式

* 计算两个方向上的导数
	a.	x 方向导数： 这是通过奇数大小的内核对图像 I 卷积得到的，例如一个尺寸为3的内核应该如下
	$$
	G_{x} = \begin{bmatrix} -1 & 0 & +1 \\ -2 & 0 & +2 \\ -1 & 0 & +1 		\end{bmatrix} * I
	$$

	b.	y方向导数： 这是通过奇数大小的内核对图像 I 卷积得到的，例如一个尺寸为3的内核应该如下
	$$
	G_{y} = \begin{bmatrix} -1 & -2 & -1 \\ 0 & 0 & 0 \\ +1 & +2 & +1 		\end{bmatrix} * I
	$$
* 在每个像素点上我们将上面得到的两个方向上的导数用下面的公式合并
	$$
	G = \sqrt{G_{x}^ {2} + G_{y}^{2}}
	$$
* 有时候会用简单的公式
	$$
	G = |G_{x}| + |G_{y}
	$$

## `void cv::Sobel()`

- - -
		void cv::Sobel(InputArray		  src,
					   OutputArray		 dst,
					   int 				ddepth,
					   int 				dx,
					   int 				dy,
					   int 				ksize = 3,
					   double			  scale = 1,
					   double 			 delta = 0,
					   int 				borderType = BORDER_DEFAULT
					   )
- - -

* 使用扩展的 Sobel 算子计算图像的 1, 2, 3 或者混合导数
* 一般情况下 一个 ksize × ksize 的内核会用来计算梯度，只有在 ksize = 1 的情况下除外，这个时候内核的大小会是 3 × 1 或 1 × 3 (没有使用过高斯模糊)，ksize = 1 只能用来计算 x 或 y 的一阶或二阶导
* 除此之外还有 ksize 还可以使用特殊值 ksize = CV_SCHARR(-1) 来使用 3 × 3 的Scharr 过滤器得到更精确的结果，Scharr 内核如下

	$$
	\begin{bmatrix}-3 &	0 & 3 \\ -10 & 0 & 10 \\ -3 & 0 &-3 \end{bmatrix}
	$$
* 以上内核用来计算 x 方向梯度，或者经过转置后计算 y 方向的梯度

### 参数说明

---

* src			输入图像
* dst			输出图像，与输入图像有相同的尺寸和通道数
* ddepth		输出图像的深度，在输入图像为 8位的情况下导数会被截断
* dx			x 方向上求导的阶数
* dy			y 方向上求导的阶数
* ksize			扩展的 Sobel 的大小，取值必须为 1, 3, 5, 7
* scale			计算 导数值的可选比例因子，默认情况下不使用缩放
* delta			将结果输出到 dst 时可选的增量
* borderType	像素外推法

***

## Laplacian 边缘检测

* 由 Sobel 算法可以得知在一阶导数极大值的地方可以找到边缘，同样的应用于二阶导数

	![](Laplace_Operator_Tutorial_Theory_ddIntensity.jpg)

* 可以得知在二阶导数为零的地方为边缘，也可以使用这个标准检测边缘，但是二阶导数为零也会出现在一些无意义的地方

* Laplacian 算子
	$$
	Laplace(f) = \dfrac{\partial^{2} f}{\partial x^{2}} + 				  \dfrac{\partial^{2} f}{\partial y^{2}}
	$$
* Laplacian 算子通过函数 ` cv::Laplacian` 在opencv中实现，由于计算了图像的梯度，所以在内部调用了Sobel来计算

## `void cv::Laolacian()`

- - -
		void cv::Laplacian(
							InputArray		src.
							OutputArray		dst.
							int				ddepth,
							int 			ksize = 1,
							int 			scale = 1,
							int 			delta = 0,
							int 			borderType = BORDER_DEFAULT
							)
- - -

* 计算图像的 Laplacian 导数
* 当 ksize 大于 1 的时候使用 Sobel 算子计算 x 方向和 y 方向的导数并将其合并得到 Laplacian 导数
* 当 ksize == 1 的时候， Laplacian 使用以下内核过滤图像得到结果
$$
	\begin{bmatrix}0 & 1 & 0 \\ 1 & -4 & 1 \\ 0 & 1 & 0\end{bmatrix}
$$

### 参数说明
* src 	&emsp;&emsp;输入图像
* dst	&emsp;&emsp;输出图像，与输入图像有相同的尺寸和通道数
* ddepth&emsp;输出图像的深度
* ksize		&emsp;用来计算第二阶导数所使用的过滤器的孔径，取值必须时正奇数
* scale		&emsp;可选的输出比例因子
* delta		&emsp;可选的输出增量因子
* borderType	&emsp;像素外推法
