# 7月13日

---
    void cv::filter2D(  InputArray src,
                        OutputArray dst,
                        int ddepth,
                        InputArray kernel,
                        Point   anchor = Point(-1, -1)
                        double delta = 0,
                        int borfer_type = BORDER_DEFAULT
                        )

---

* 使用核函数(kernel)对输入图像(src)进行卷积操作，输出到dst上
* 参考点(anchor)默认值表示核函数中心
* 该函数实际上并不是卷积操作，而是在计算相关性
* 真正的卷积操作使用`cv::flip()`反转内核并将参考点设置为 `(kernel.cols - anchor.x - 1, kernel.rows - anchor.y - 1)`

### 参数

* ddepth        目标图像的所需深度
* kernel        卷积内核，单通道浮点矩阵，如果要把不同的内核用于不同的通道，用拆分将图像分割成单独的通道平面并单独处理
* delta         将可选值添加到滤波像素中
* border_type   像素外推的方法，也就是处理边界的方法
