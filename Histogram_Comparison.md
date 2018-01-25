# 7月27日

# 直方图比较

## 原理

* 为了比较两个直方图($H_{1}$ 和 $H_{2}$)，我们要选取一个指标($d(H_{1}, H_{2})$)来表达两个直方图匹配的程度
* opencv实现了函数`cv::compareHist`来完成直方图的比较.该函数提供了四种不同的指标来计算直方图的匹配程度

    1. Corrrelation(CV_COMP_CORREL) 相关性
        $$
            d(H_1,H_2) = \frac{\sum_I (H_1(I) - \bar{H_1}) (H_2(I) - \bar{H_2})}{\sqrt{\sum_I(H_1(I) - \bar{H_1})^2 \sum_I(H_2(I) - \bar{H_2})^2}}
        $$
      在这里
        $$
          \bar{H_k} = \frac{1}{N} \sum_J H_k(J)
        $$
      N是直方图中bins的总数目    

   2. Chi-Square(CV_COMP_CHISQR) 卡方
        $$
          d(H_1,H_2) = \sum_I \frac{\left(H_1(I)-H_2(I)\right)^2}{H_1(I)}
        $$
   3. Intersection(method = CV_COMP_INTERSECT)
        $$
          d(H_1,H_2) = \sum_I \min (H_1(I), H_2(I))
        $$
   4. Bhattacharyya distance(CV_COMP_BHATTACHARYYA)
        $$
          d(H_1,H_2) = \sqrt{1 - \frac{1}{\sqrt{\bar{H_1} \bar{H_2} N^2}} \sum_I \sqrt{H_1(I) \cdot H_2(I)}}
        $$

  ***

## `double cv::compareHist()`
---
```c++
        double cv::compareHist(
                  InputArray      H1,
                  InputArray      H2,
                  int             method
        )
```
---
* 该函数比较两个直方图
* 函数`cv::compareHist`使用指定的方法比较两个稠密或稀疏的直方图
* 该函数在1, 2, 3 维的稠密直方图下工作的很好，但或许并不适合高维度稀疏直方图。在这样的直方图中，由于混叠和采样的问题，非0直方图bin的坐标可能略有偏移。要比较这些直方图或更一般的稀疏配置的加权点，可以考虑使用`cv::EMD`函数
### 参数
---
* H1    首先比较的直方图
* H2    第二比较的直方图，尺寸和H1相同
* method  比较的方法，定义在`cv::HistCompMethods`

## `cv::HistCompMethods`
---

* HISTCMP_CORRRL 同Corrrelation
* HISTCMP_CHISQR 同Chi-Square
* HISTCMP_INTERSECT 同Intersection
* HISTCMP_BHATTACHARYYA 同Bhattacharyya distance
* HISTCMP_HELLINGER
* HISTCMP_CHISQR_ALT
* HISTCMP_KL_DV
