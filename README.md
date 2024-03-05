## 1.git备忘

提交到暂存区

```bash
git add .
```

提交代码

```bash
git commit -m "init project"
```

上传代码至github

```bash
git remote add origin git@github.com:yuan-shuo/Grad.git
git push -u origin master
```

使用前请阅读协议

## 2.参数说明

### 2.1.archi

```python
# 模块
class Archi:
    def __init__(
            self, s_l:float, n_l:int,
            qu_b:int, qd_b:int, r_b:float, n_b:int, c_b:float,
            enter:dict,
            div_b=2, m_b=0, k=1.4, w_n=3, tm=4, bn=1.25, ct=3200,
            ab=0.15
            ):
        
# 需指定的参数
s_l 列车每节长度
n_l 列车节数
qu_b 上下行上车人数总和
qd_b 上下行下车人数总和
r_b 站台人流密度
n_b 横向柱子个数
c_b 柱宽
enter 通道及对应人流数量

# 可以修改的默认参数
div_b=2,发车间隔时间
m_b=0,站台边缘至屏蔽门立柱内侧的距离
k=1.4,超高峰系数
w_n=3,步行楼梯宽度
tm=4,逃生最大限制时间
bn=1.25,出入口客流不均匀系数
ct=3200,步行楼梯通过能力
ab=0.15,加宽系数

# 实例
archi = Archi(
        s_l=22.8, n_l=4,
        qu_b=1950, qd_b=1934, r_b=0.5, n_b=2, c_b=0.7,
        enter={
            "A1":810,
            "A2":810,
            "B1":448,
            "B2":471,
            "C":938
        }
        )
```

