# 7月１日　opencv 笔记

### `cv::Mat cv::imread(const string& filename, int flag = IMREAD_COLOR)`

* 这个函数从filename文件中载入一个图像并返回cv::Mat
* 如果这个图像载入失败，那么就会返回一个空的cv::Mat
* 注意，函数以文件内容判断图像的格式而不是文件的后缀名
* 对于彩色图像来说，解码后图像的通道的顺序是　B G R

### 参数说明
* filename 图像的文件名
* flag      可以从[cv::ImreadModes](http://docs.opencv.org/3.2.0/d4/da8/group__imgcodecs.html#ga61d9b0126a3e57d9277ac48327799c80)中取值


## `void cv::cvtColor(InputArray src, OutputArray dst, int code, int dstCn = 0)`

* 将src图像从一个颜色空间转换到另一个颜色空间，输出到dst中

### 参数说明
* src 输入图像
* dst  输出图像，要与src一样大小和形状
* code 色彩空间转换码，[cv::ColorConversionCodes](http://docs.opencv.org/3.2.0/d7/d1b/group__imgproc__misc.html#ga4e0972be5de079fed4e3a10e24ef5ef0)