# SM4 Sbox 塔域实现
本项目完成了国密算法SM4中S盒的硬件实现
实现方法为同构同构映射矩阵，将求逆运算最终转化到GF(2)上进行，比直接用查找表实现节省面积
适合面积限制型的应用
## 2019-04-18更新
整体的实现方案在参考的一篇博士论文中已经写的很详细了，所以本来应该是一次很简单的硬件实现项目。
**但是**，逻辑仿真的时候，发现代数式怎么都和S盒对不上！又倒回matlab做代数式的仿真。
**结果**，matlab仿真发现，即使不通过同构映射转换到塔域，这个代数式还是对不上S盒。各种查阅文献，所有给出的代数式都是一样的，仿射变换的矩阵也是一样的。
仿佛就跟发现了“学术腐败坑”一样，这么多人，不能同时造假吧？！可是我确实又复现不出来。。。
拖了几天都打算上报这个问题了...
终于发现了篇文章，给出了S盒的[代数C代码]!(https://blog.csdn.net/qq_36291381/article/details/80156315)（别误会，不是查找表实现）。
问题出在下图：

这个仿射变换的C，应该换一下顺序。。。真是太坑了有没有。。。而且所有的文献都是直接给出一个代数式，丝毫没有说明下列问题：
1. x输入矢量是MSB_first还是LSB_first
2. 中间运算转到塔域求逆时，行向量转置为列向量，是MSB_first还是LSB_first？
总是很多模糊不定的问题，让我试来试去。。。很烦
