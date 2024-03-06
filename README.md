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

将远程仓库的更改拉取到本地

```bash
git pull
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

接口案例：

```json
# in  =>
ek = json.loads(request.POST.get("enterk"))
ev = json.loads(request.POST.get("enterv"))
s_l, n_l, qu_b, qd_b, r_b, n_b, c_b, enterk, enterv = (
float(request.POST.get('s_l')),
int(request.POST.get('n_l')),
int(request.POST.get('qu_b')),
int(request.POST.get('qd_b')),
float(request.POST.get('r_b')),
int(request.POST.get('n_b')),
float(request.POST.get('c_b')),
ek, ev
        )
# out =>
{
    "len":str,
    "stair":list,
    "width":list,
    "equip":list,
    "enter":list[list1, list2]
}

{
    "len": "本站过站车辆为4辆编组，列车每节长度为22.8m，故本站站台有效长度为4*22.8+1~2=92.2~93.2m，取为93m。",
    "stair": [
        "考虑在93m站台长度内，至少设置2个出站口，因此选取2部1m宽自动扶梯，同时为保证事故疏散时间的要求，采用2部3m宽楼梯。",
        "人行楼梯和自动扶梯总量布置除应满足上、下乘客的需要外，还应按站台层的事故疏散时间不大于4min进行验算，消防专用梯及垂直电梯不计入事故疏散用。",
        "计算中，考虑1台自动扶梯损坏不能运行，(N-1)台自动扶梯和人行楼梯的通过能力按9折折减，式子中“1”为人的反应时间，单位为min；T=3.893min<4min，满足规范防灾要求。"
    ],
    "width": [
        "通过两种方式求得的b分别为0.749m、0.696m，取b=2.5m",
        "已知b=2.5m，计算岛式站台宽度B=10.4m，考虑到自动扶梯安装宽度及楼梯扶手宽度等，站台宽度取12m。"
    ],
    "equip": [
        "根据计算，所需自动售票机台数为1.6台，取4台，每边各2台。",
        "根据计算，所需人工窗口数为0.8间，由于同时设置了自动售票机，因此设置4间来满足要求，每边2间。",
        "根据计算，进站检票机台数为1.6台，取4台，每边各2台。同时在检票机旁设置一具有一定宽度的人工开启栅栏门以便于处理较大行李出入的问题。",
        "根据计算，出站检票机台数为1.6台，取4台，每边各2台。出站检票口附近各设一补票亭，以便乘客补票。"
    ],
    "enter": [
        [
            "根据计算得A1通道宽度为0.4，同时出入口宽度不小于2.5m，取2.5m。",
            "根据计算得A2通道宽度为0.4，同时出入口宽度不小于2.5m，取2.5m。",
            "根据计算得B1通道宽度为0.2，同时出入口宽度不小于2.5m，取2.5m。",
            "根据计算得B2通道宽度为0.3，同时出入口宽度不小于2.5m，取2.5m。",
            "根据计算得C通道宽度为0.5，同时出入口宽度不小于2.5m，取2.5m。"
        ],
        [
            "根据计算得A1通道楼梯宽度为0.6，取2.5m。",
            "根据计算得A2通道楼梯宽度为0.6，取2.5m。",
            "根据计算得B1通道楼梯宽度为0.3，取2.5m。",
            "根据计算得B2通道楼梯宽度为0.3，取2.5m。",
            "根据计算得C通道楼梯宽度为0.7，取2.5m。"
        ]
    ]
}

```

