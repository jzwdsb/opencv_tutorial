# 7月4日

---

    void cv::addWeighted( InputArray  src1,
                          double      alpha,
                          InputArray  src2,
                          double      beta,
                          double      gamma,
                          OutputArray dst,
                          INT         dtype = -1
                         )

---

* 计算两个矩阵的权和，对图像而言是将两个图像alpha融合，公式如下

        dst(I) = saturate(src(I) * alpha + src(I) * beta + gamma)

> 注：在多通道图像的情况下，每个通道都会单独进行处理

### 参数说明

* src1          第一个图像
* alpha         第一个图像的权重
* src2          第二个图像
* beta          第二个图像的权重
* gama          两图像融合式的所相加的偏移量
* dtype         输出矩阵的可选深度，当两个矩阵具有相同的深度时，dtype设置为-1，相当于src1.depth()
