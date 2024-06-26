## 一个图像 $f(x, y)$ 经过傅里叶变换后成为 $F(u, v)$，$F(u, v)$ 有什么性质呢？

二维离散傅里叶变换（2D DFT）将空间域的图像 $ f(x, y) $ 转换为频域的表示 $ F(u, v) $。$ F(u, v) $ 在频域中具有一些重要的性质，这些性质在图像处理中非常有用。以下是主要的性质：

### 1. 共轭对称性（Conjugate Symmetry）

对于实值图像 $ f(x, y) $，其傅里叶变换 $ F(u, v) $ 具有共轭对称性，即：

$$ F(u, v) = F^*(-u, -v) $$

这里 $ F^*(u, v) $ 表示 $ F(u, v) $​ 的共轭复数。

​	**如果 $F(u, v) = a + bj， F(u, v) = F^*(-u, -v) $ 那么 $F(u, v) = F^*(-u, -v) = a + bj$，因为 $F^*(-u, -v)$ 是 $F(-u, -v)$ 的共	轭复数，那么  $F(-u, -v)$ 就是 $F^*(-u, -v)$ 的实部不变 + 虚部取反，$F(-u, -v) = a - bj$。**

在实际计算中，离散傅里叶变换的索引是周期性的，因此这个性质可以写成：

$$ F(u, v) = F^*(M - u, N - v) $$

其中，$ M $ 和 $ N $ 分别是图像的宽度和高度。

### 2. 傅里叶变换的周期性（Periodicity）

二维离散傅里叶变换是周期性的，周期为 $ M $ 和 $ N $，即：

$$ F(u + M, v) = F(u, v) $$
$$ F(u, v + N) = F(u, v) $$

这意味着频域中的图像是一个周期性的二维信号。

### 3. 傅里叶变换的线性性（Linearity）

二维傅里叶变换是线性的，即：

$$ \mathcal{F}\{a f_1(x, y) + b f_2(x, y)\} = a \mathcal{F}\{f_1(x, y)\} + b \mathcal{F}\{f_2(x, y)\} $$

其中，$ \mathcal{F} $ 表示傅里叶变换，$ a $ 和 $ b $ 是常数。

### 4. 变换对位移的敏感性（Translation Sensitivity）

图像的位移在频域中会引起相位的变化：

如果 $ f(x, y) $ 位移 $ (x_0, y_0) $，即 $ g(x, y) = f(x - x_0, y - y_0) $，则其傅里叶变换 $ G(u, v) $ 为：

$$ G(u, v) = F(u, v) e^{-j2\pi\left(\frac{ux_0}{M} + \frac{vy_0}{N}\right)} $$

### 5. 尺度变换（Scaling Property）

图像的缩放会影响其频域表示的扩展：

如果 $ g(x, y) = f(ax, by) $，则其傅里叶变换 $ G(u, v) $ 为：

$$ G(u, v) = \frac{1}{|ab|} F\left(\frac{u}{a}, \frac{v}{b}\right) $$

### 6. 傅里叶变换的旋转性（Rotation Property）

如果 $ f(x, y) $ 旋转角度 $ \theta $，则其傅里叶变换 $ F(u, v) $ 也旋转相同的角度 $ \theta $：

如果 $ g(x', y') = f(x, y) $ 表示 $ f(x, y) $ 旋转角度 $ \theta $，则 $ G(u', v') = F(u, v) $ 也旋转相同的角度 $ \theta $。

### 7. 傅里叶变换的能量守恒（Parseval's Theorem）

图像在空间域和频域中的能量是守恒的，即：

$$ \sum_{x=0}^{M-1} \sum_{y=0}^{N-1} |f(x, y)|^2 = \frac{1}{MN} \sum_{u=0}^{M-1} \sum_{v=0}^{N-1} |F(u, v)|^2 $$

### 8. 对称性

在频域中，原图像的中心（零频率）位于左上角，需要通过移动将其移至图像的中心，以便更好地观察和处理。这一操作称为傅里叶频谱中心化。

### 9. 零频率分量

傅里叶变换的零频率分量 $ F(0, 0) $ 表示图像的直流分量或平均亮度值：

$$ F(0, 0) = \sum_{x=0}^{M-1} \sum_{y=0}^{N-1} f(x, y) $$

### 总结

理解傅里叶变换在频域中的这些性质，对于图像处理中的滤波、复原、压缩等操作非常重要。这些性质不仅帮助我们分析和理解图像的频率成分，也提供了强大的工具来实现各种图像处理任务。

------

## 这些性质在图像里是怎么表现的？

在图像处理中，二维离散傅里叶变换（2D DFT）的性质通过各种方式表现出来。下面详细描述这些性质在图像处理中的具体表现：

### 1. 共轭对称性（Conjugate Symmetry）

对于实值图像 $ f(x, y) $，其傅里叶变换 $ F(u, v) $ 具有共轭对称性。这意味着频谱图像中心对称。具体表现为：
- 在频谱图像中，中心点是直流分量（平均亮度）。
- > 频谱的左上角和右下角，以及右上角和左下角的对称点处的值是共轭对称的（实部相等，虚部相反）。

### 2. 傅里叶变换的周期性（Periodicity）

二维离散傅里叶变换是周期性的，这意味着频域表示 $ F(u, v) $ 是一个周期性的二维信号。具体表现为：
- 频谱图像在水平和垂直方向上是周期性的，即频谱图像可以无缝地平铺。

### 3. 傅里叶变换的线性性（Linearity）

傅里叶变换的线性性质在图像处理中体现在：
- 对两个图像进行线性组合后再进行傅里叶变换，与分别对两个图像进行傅里叶变换后再线性组合，得到的结果是相同的。这在滤波和混合处理图像时非常有用。

### 4. 变换对位移的敏感性（Translation Sensitivity）

图像的位移在频域中引起相位的变化。具体表现为：
- 当图像在空间域中平移时，其频谱的幅度保持不变，但**相位**会发生变化。这在图像配准和运动分析中非常重要。

### 5. 尺度变换（Scaling Property）

图像的缩放会影响其频域表示的扩展。具体表现为：
- 当图像在空间域中进行缩放时，其频谱也会相应地缩放。图像缩小会导致频谱拉伸，图像放大会导致频谱压缩。

### 6. 傅里叶变换的旋转性（Rotation Property）

图像的旋转在频域中表现为相同角度的旋转。具体表现为：
- 如果图像在空间域中旋转了一个角度，那么其频谱也会旋转相同的角度。这在图像旋转不变特征提取中很有用。

### 7. 傅里叶变换的能量守恒（Parseval's Theorem）

图像在空间域和频域中的能量是守恒的。具体表现为：
- 空间域中的总能量（像素值的平方和）等于频域中的总能量（频谱系数的平方和）。这在图像分析和信号处理中的能量计算和归一化中很有用。

### 8. 对称性

傅里叶变换的频谱图像通常通过中心化处理，使零频率成分位于图像中心。具体表现为：
- 通过傅里叶频谱中心化，频谱图像的低频成分（图像的大尺度特征）集中在中心，高频成分（图像的细节和噪声）在周围。这有助于更直观地分析和处理图像的频率成分。

### 9. 零频率分量

傅里叶变换的零频率分量代表图像的直流分量或平均亮度值。具体表现为：
- 零频率分量位于频谱图像的中心点，其值代表图像的整体亮度水平。

### 应用示例

#### 去噪

低通滤波器（如高斯滤波器）通过**抑制高频成分（噪声）**，在频域中实现去噪处理。表现为频谱图像的外围（高频区域）被衰减。

#### 边缘检测

高通滤波器通过抑制低频成分（平滑区域），在频域中实现边缘检测。表现为频谱图像的中心区域（低频区域）被衰减。

#### 图像增强

通过增强某些频率成分，可以实现图像的锐化或其他特定的增强效果。表现为频谱图像中对应频率成分的幅值被放大。

### 例子：图像的傅里叶变换和逆变换

假设有一幅大小为 $ M \times N $ 的图像 $ f(x, y) $：

1. 计算其二维傅里叶变换 $ F(u, v) $：
   $$ F(u, v) = \sum_{x=0}^{M-1} \sum_{y=0}^{N-1} f(x, y) \cdot e^{-j2\pi\left(\frac{ux}{M} + \frac{vy}{N}\right)} $$

2. 频谱中心化：
   $$ F_{\text{centered}}(u, v) = F((u + \frac{M}{2}) \% M, (v + \frac{N}{2}) \% N) $$

3. 应用滤波器（如理想低通滤波器）：
   $$ \hat{F}(u, v) = H(u, v) \cdot F(u, v) $$

4. 计算逆傅里叶变换 $ \hat{f}(x, y) $ ：
   $$ \hat{f}(x, y) = \frac{1}{MN} \sum_{u=0}^{M-1} \sum_{v=0}^{N-1} \hat{F}(u, v) \cdot e^{j2\pi\left(\frac{ux}{M} + \frac{vy}{N}\right)} $$

通过以上步骤，可以在频域中处理图像，并利用傅里叶变换的性质实现各种图像处理任务。

------

## 关于共轭对称性：频谱的左上角和右下角，以及右上角和左下角的对称点处的值是共轭对称的（实部相等，虚部相反）。

好的，让我们举一个具体的例子来说明二维离散傅里叶变换（2D DFT）中的共轭对称性。

假设我们有一个简单的 2x2 图像 $ f(x, y) $：

$$ f(x, y) = \begin{bmatrix} 1 & 2 \\ 3 & 4 \end{bmatrix} $$

### 计算二维离散傅里叶变换 $ F(u, v) $

二维离散傅里叶变换的公式为：

$$ F(u, v) = \sum_{x=0}^{M-1} \sum_{y=0}^{N-1} f(x, y) \cdot e^{-j2\pi\left(\frac{ux}{M} + \frac{vy}{N}\right)} $$

对于 2x2 的图像，$ M = 2 $ 和 $ N = 2 $。我们需要计算 $ u, v \in \{0, 1\} $ 的情况。

#### 计算 $ F(0, 0) $

$$ F(0, 0) = \sum_{x=0}^{1} \sum_{y=0}^{1} f(x, y) \cdot e^{-j2\pi\left(\frac{0x}{2} + \frac{0y}{2}\right)} $$
$$ = f(0, 0) \cdot 1 + f(0, 1) \cdot 1 + f(1, 0) \cdot 1 + f(1, 1) \cdot 1 $$
$$ = 1 + 2 + 3 + 4 = 10 $$

#### 计算 $ F(0, 1) $

$$ F(0, 1) = \sum_{x=0}^{1} \sum_{y=0}^{1} f(x, y) \cdot e^{-j2\pi\left(\frac{0x}{2} + \frac{1y}{2}\right)} $$
$$ = f(0, 0) \cdot 1 + f(0, 1) \cdot e^{-j\pi} + f(1, 0) \cdot 1 + f(1, 1) \cdot e^{-j\pi} $$
$$ = 1 + 2(-1) + 3 + 4(-1) $$
$$ = 1 - 2 + 3 - 4 = -2 $$

#### 计算 $ F(1, 0) $

$$ F(1, 0) = \sum_{x=0}^{1} \sum_{y=0}^{1} f(x, y) \cdot e^{-j2\pi\left(\frac{1x}{2} + \frac{0y}{2}\right)} $$
$$ = f(0, 0) \cdot 1 + f(0, 1) \cdot 1 + f(1, 0) \cdot e^{-j\pi} + f(1, 1) \cdot e^{-j\pi} $$
$$ = 1 + 2 + 3(-1) + 4(-1) $$
$$ = 1 + 2 - 3 - 4 = -4 $$

#### 计算 $ F(1, 1) $

$$ F(1, 1) = \sum_{x=0}^{1} \sum_{y=0}^{1} f(x, y) \cdot e^{-j2\pi\left(\frac{1x}{2} + \frac{1y}{2}\right)} $$
$$ = f(0, 0) \cdot 1 + f(0, 1) \cdot e^{-j\pi} + f(1, 0) \cdot e^{-j\pi} + f(1, 1) \cdot e^{-j2\pi} $$
$$ = 1 + 2(-1) + 3(-1) + 4 \cdot 1 $$
$$ = 1 - 2 - 3 + 4 = 0 $$

### 傅里叶变换矩阵 $ F(u, v) $

将这些计算结果汇总，我们得到傅里叶变换矩阵 $ F(u, v) $：

$$ F(u, v) = \begin{bmatrix} 10 & -2 \\ -4 & 0 \end{bmatrix} $$

### 共轭对称性

对于实值图像 $ f(x, y) $，其傅里叶变换 $ F(u, v) $ 具有共轭对称性。根据共轭对称性，**应该满足：**

$$ F(u, v) = F^*(M - u, N - v) $$

具体到我们的例子中：

- $ F(0, 0) $ 和 $ F^*(2-0, 2-0) = F^*(0, 0) $ 显然是相等的。
- $ F(0, 1) $ 和 $ F^*(2-0, 2-1) = F^*(0, 1) $ 也是相等的。
- $ F(1, 0) $ 和 $ F^*(2-1, 2-0) = F^*(1, 0) $ 也是相等的。
- $ F(1, 1) $ 和 $ F^*(2-1, 2-1) = F^*(1, 1) $ 也是相等的。

在这个例子中，由于图像大小较小且值较简单，共轭对称性在实部和虚部上表现不明显，但在更大、更复杂的图像中，这种对称性会更加显著。共轭对称性确保了频域表示在中心对称点上的值是共轭复数关系，实部相等，虚部相反。