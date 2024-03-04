
# 用于 splitstree 绘制枝条颜色的数据处理
20240303 黄玮


## 步骤一
1. 用 `splistree6` 打开 `.nex` 文件，另存为 `.tree6` 文件， 使用 `VScode` 等编辑器打开 `.tree6` 文件    
    + *在进行后续操作之前，注意备份好 `.nex` 和 `.tree6` 文件*
2. 搜索 `Input Taxa`，将其下的`TAXLABELS`复制保存为 **TAXLABELS.txt** ，注意不要与 `Working Taxa` 中的内`TAXLABELS`相混。
内容如：
```md
[1] 'UIGHUR_XINJIANG_YILI_YINING'
[2] 'KAZAKH_XINJIANG_HABAHE'
[3] 'KAZAKH_XINJIANG_CHABUCHAER'
[4] 'KIRGHIZ_XINJIANG_KEZILESU'
[5] 'UZBEK_XINJIANG_ULUMUQI'
[6] 'TATAR_XINJIANG_ULUMUQI'
[7] 'TUVA_XINJIANG_ALETAI_BUERJIN'
[8] 'SALAER_QINGHAI_HAIDONG_XUNHUA'
[9] 'YUGU_GANSU_SUNAN_LIANHUA'
[10] 'AYNU'
[11] 'UYGHUR'
[12] 'WEST_YUGUR'

## 注释：上面方括号中的是 taxa id，右边引号中是语档名称
## 顶格，空格分隔。
```

3. 搜索`BEGIN SPLITS;`，将其下的`MATRIX`下的内容复制保存为 **MATRIX.txt** 内容如：

```md
 [1, size=1]    1.01405344    1, 
 [2, size=2]    0.76986088    1 11, 
 [3, size=3]    0.16998447    1 10 11, 
 [4, size=5]    0.16988877    1 7 8 9 10 11 12, 
 [5, size=4]    0.1643407    1 2 7 8 9 10 11 12, 
 [6, size=1]    1.37015191    1 2 3 4 6 7 8 9 10 11 12, 
 [7, size=1]    2.23683057    1 2 3 4 5 6 7 8 9 10 12, 
 [8, size=5]    0.25397301    1 3 4 5 6, 
 [9, size=3]    0.10568184    1 5 6, 
 [10, size=2]    0.25042598    1 5, 
 [11, size=1]    5.87411191    1 2 3 4 5 6 7 8 9 11 12, 
 [12, size=2]    0.27483692    1 2 3 4 5 6 8 9 11 12, 
 [13, size=5]    0.1345841    1 2 3 4 5 6 11, 
 [14, size=5]    0.21406404    1 4 5 6 11, 
 [15, size=3]    0.03583032    1 5 11, 
 [16, size=1]    3.02197665    1 2 3 4 5 6 8 9 10 11 12, 
 [17, size=2]    0.02813038    1 2 3 4 5 6 9 10 11 12, 
 [18, size=3]    0.16969986    1 2 3 4 5 6 10 11 12, 
 [19, size=1]    2.50250332    1 2 3 4 5 6 7 9 10 11 12, 
 [20, size=2]    0.40667705    1 2 3 4 5 6 7 10 11 12, 
 [21, size=1]    1.94496825    1 2 3 4 5 6 7 8 10 11 12, 
 [22, size=2]    0.73234611    1 2 3 4 5 6 7 8 10 11, 
 [23, size=3]    0.12562682    1 3 4 5 6 7 8 10 11, 
 [24, size=1]    3.15754692    1 2 3 4 5 6 7 8 9 10 11, 
 [25, size=1]    2.19893964    1 3 4 5 6 7 8 9 10 11 12, 
 [26, size=2]    0.34752397    1 4 5 6 7 8 9 10 11 12, 
 [27, size=3]    0.19409975    1 5 6 7 8 9 10 11 12, 
 [28, size=4]    0.22481508    1 5 7 8 9 10 11 12, 
 [29, size=1]    0.80291046    1 2 4 5 6 7 8 9 10 11 12, 
 [30, size=2]    0.23789141    1 2 5 6 7 8 9 10 11 12, 
 [31, size=1]    0.98172901    1 2 3 5 6 7 8 9 10 11 12, 
 [32, size=1]    1.54206049    1 2 3 4 5 7 8 9 10 11 12, 

## 注释：方括号里的第一个数字 是节点的 id 或者叫 nsplits id，
## 注意与上面的 taxa id 不同，而后面指定枝条的颜色需要使用的是这个nsplits id， 
## size 后面的数字表示该节点有几个 taxa，
## 中间一列在这个任务中没有用，
## 最后一列列出的数字是 taxa id，后面的任务需要根据这个进行反推，
## 即通过这堆数字推测出该 taxa 所在的 nsplits id，然后指定枝条的颜色。
## 顶格
```

4. 制作一个语档分组，即想把语档的标签文字、标签背景、线条分别设置成什么颜色，同一个方言或符合相同预设条件的分为同一个组，存为 **docu_color.txt** 如（使用 `tab` 分隔）：

| docu | label_c | label_background_c | edge_c |
| -- | -- | -- | -- |
| UIGHUR_XINJIANG_YILI_YINING | 1 | 0 | 1 |
| KAZAKH_XINJIANG_HABAHE | 1 | 0 | 1 |
| KAZAKH_XINJIANG_CHABUCHAER | 1 | 0 | 1 |
| KIRGHIZ_XINJIANG_KEZILESU | 2 | 0 | 2 |
| UZBEK_XINJIANG_ULUMUQI | 2 | 0 | 2 |
| TATAR_XINJIANG_ULUMUQI | 2 | 0 | 2 |
| TUVA_XINJIANG_ALETAI_BUERJIN | 2 | 0 | 2 |
| SALAER_QINGHAI_HAIDONG_XUNHUA | 3 | 0 | 3 |
| YUGU_GANSU_SUNAN_LIANHUA | 3 | 0 | 3 |
| AYNU | 3 | 0 | 3 |
| UYGHUR | 4 | 0 | 4 |
| WEST_YUGUR | 4 | 0 | 4 |

注意：如果不想要标签的背景颜色，则 `label_background_c` 列均设置为0。一般`label_c` 和 `edge_c` 可以设置为一样，这样标签和枝条的颜色是一样的。如果超过20个类别，需要修改 python 代码中的颜色字典，增加颜色。


## 步骤二
1. 在 `jupyter lab` 中依次运行 `HW_准备绘制枝条颜色数据.ipynb` 的单元格
2. 得到输出文件 **df_color.txt** 和 **df_edgcolor.txt**
3. 将 **df_color.txt** 中的内容复制，替换掉 `.tree6` 中 `Input Taxa` 下的`TAXLABELS`
4. 将 **df_edgcolor.txt** 中的内容复制，替换掉 `.tree6` 中 `TITLE 'SplitsNetwork';` 下的 `Edits = `后的内容，注意最后有一个英文的逗号不要误删了

## 步骤三
1. 保存 `.tree6` 文件，做好备份
2. 打开 `splitstree6` 读取文件

<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>

