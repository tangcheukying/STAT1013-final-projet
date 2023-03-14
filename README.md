# STAT1013-final-projet

---
jupyter:
  colab:
  kernelspec:
    display_name: Python 3
    name: python3
  language_info:
    name: python
  nbformat: 4
  nbformat_minor: 0
---

<div class="cell markdown" id="HKyU5zKzvAvS">

# CUHK-STAT1013: Practical Assignment Part 1: Sharing Your Idea and Data

</div>

<div class="cell markdown" id="ByrcqMDUvK10">

## DSE results dataset background

**Description**:

Dataset describing the HKDSE results of candidates in Mathematics.

**Sample size**: 80

**Feature documentation**:

| Feature         | Dtype   |
|:----------------|:--------|
| NAME            | string  |
| SEX             | string  |
| MARK PERCENTAGE | float64 |
| GRADE           | flaot64 |

</div>

<div class="cell markdown" id="qwsc2k2v2b1S">

## Hypothesis

-   Tell us what your idea is and why you have chosen to pursue this
    idea.
    -   We are interested in "*Did male has a better performance in
        Mathematics?*"
-   What two groups you are comparing:
    -   **G1**: Mathematics score percentage of male in 2022 DSE;
        **G2**: Mathematics score percentage of female in 2022 DSE
-   What you will be measuring (i.e., what your response variable will
    be)
    -   `MARK PERCENTAGE (%)`
-   Is your response variable quantitative rather than categorical?
    -   `MARK PERCENTAGE (%)` is numerical, which can be ranked, it is
        regarded as a quantitative variable.
-   Make a prediction about what kind of difference you expect to see
    between your samples and WHY.
    -   We'd expect that **G1** \> **G2** since [Boys are better at
        mathematics than
        girls](https://www.bbc.com/ukchina/trad/50863077)
-   Talk about how you will gather your data
    -   survey friends and classmates
-   If you had unlimited resources (time, money, staff, etc.) how would
    you collect your data?
    -   \(i\) collect a bigger sample size; (ii) try to survey all 2022
        DSE candidates

</div>

<div class="cell markdown" id="QuXJYRkv0dtF">

##Prepare your dataset

</div>

<div class="cell code" execution_count="4" id="7hhbuSNhKpUy">

``` python
from google.colab import drive
```

</div>

<div class="cell code" execution_count="3"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;}"
id="PsPG3NvQKy7d" outputId="adada25d-d7e8-487b-9362-ea9c98722483">

``` python
drive.mount('/content/gdrive')
```

<div class="output stream stdout">

    Mounted at /content/gdrive

</div>

</div>

<div class="cell code" execution_count="5" id="kfH9WLGaK6wO">

``` python
import pandas as pd
```

</div>

<div class="cell code" execution_count="6" id="EyuGbT46s2Lg">

``` python
Data = pd.read_excel(r'/content/gdrive/My Drive/STAT.PROJ/STAT proj data.xlsx')
```

</div>

<div class="cell code" execution_count="7"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;,&quot;height&quot;:419}"
id="cAAcTtvUuRsg" outputId="862062ed-8b62-49fa-e9e5-4c0294264999">

``` python
display (pd.DataFrame(Data))
```

<div class="output display_data">

                    NAME     SEX  MARK PERCENTAGE (%)  GRADE
    0         AU LOK HEI  FEMALE                 62.1    3.0
    1         AU PAK HEI    MALE                 84.2    5.0
    2         AU TSZ YAN  FEMALE                 82.5    5.0
    3       CAI WING LAM  FEMALE                 72.0    4.0
    4         CHAN KA KI  FEMALE                 88.4    6.0
    ..               ...     ...                  ...    ...
    75   YEUNG CHING YAN  FEMALE                 83.7    5.0
    76        YUENG WANG    MALE                 80.6    5.0
    77  YIP YI LAM NAOMI  FEMALE                 54.3    3.0
    78       YIU TSZ HIM    MALE                 82.4    5.0
    79         ZOU QILIN    MALE                 86.8    5.0

    [80 rows x 4 columns]

</div>

</div>

<div class="cell code" execution_count="8"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;,&quot;height&quot;:204}"
id="ZFbX1zpn0_PA" outputId="5aa9d2cd-16cb-447e-c556-726664f92e8e">

``` python
import pandas as pd

df = pd.read_excel(r'/content/gdrive/My Drive/STAT.PROJ/STAT proj data.xlsx')
df.head(5)
```

<div class="output execute_result" execution_count="8">

               NAME     SEX  MARK PERCENTAGE (%)  GRADE
    0    AU LOK HEI  FEMALE                 62.1    3.0
    1    AU PAK HEI    MALE                 84.2    5.0
    2    AU TSZ YAN  FEMALE                 82.5    5.0
    3  CAI WING LAM  FEMALE                 72.0    4.0
    4    CHAN KA KI  FEMALE                 88.4    6.0

</div>

</div>

<div class="cell markdown" id="1nSZt2Vo7FZQ">

-   Tell us what groups you want to compare in the dataset
    -   **G1** (MARK PERCENTAGE (%)\| SEX = MALE) vs. **G2** (MARK
        PERCENTAGE (%)\| SEX = FEMALE)

</div>

<div class="cell markdown" id="VcMhos6_-Zwc">

## Print first 5 records of each group respectively.

</div>

<div class="cell code" execution_count="24"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;}"
id="7OIR-toTtF1G" outputId="0f48a8a3-0cd3-4fba-f50c-40c41deba404">

``` python
## First 5 records of G1 (MALE)
(df[df['SEX'] == 'MALE']['MARK PERCENTAGE (%)']).head(5)
```

<div class="output execute_result" execution_count="24">

    1     84.2
    5     52.0
    6     55.6
    9     45.7
    11    87.9
    Name: MARK PERCENTAGE (%), dtype: float64

</div>

</div>

<div class="cell code" execution_count="25"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;}"
id="J9iEjgHDtnoq" outputId="5172879f-9d39-4bdc-d42c-3fb258a3a891">

``` python
## First 5 records of G1 (FEMALE)
(df[df['SEX'] == 'FEMALE']['MARK PERCENTAGE (%)']).head(5)
```

<div class="output execute_result" execution_count="25">

    0    62.1
    2    82.5
    3    72.0
    4    88.4
    7    88.2
    Name: MARK PERCENTAGE (%), dtype: float64

</div>

</div>

<div class="cell markdown" id="Ot-ChS9vwOmA">

##Print the mean, std, min and max values for MARK PERCENTAGE (%) and
GRADE based on MALE and FEMALE

</div>

<div class="cell code" execution_count="27"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;,&quot;height&quot;:173}"
id="AM_Z_lG5tx8F" outputId="1b825f30-5e09-4759-e1d9-7f91bf0769dc">

``` python
df.groupby('SEX')[['MARK PERCENTAGE (%)', 'GRADE']].agg(['mean', 'std', 'min', 'max'])
```

<div class="output execute_result" execution_count="27">

           MARK PERCENTAGE (%)                         GRADE                    
                          mean        std   min   max   mean       std  min  max
    SEX                                                                         
    FEMALE             61.8200  21.241737  15.8  95.3  3.550  1.484104  1.0  7.0
    MALE               66.5075  20.411678  21.0  97.2  3.875  1.555594  1.0  7.0

</div>

</div>

<div class="cell markdown" id="EFBunIVf36H1">

## Print overall histplot and violinplot of bp_before via sns.histplot and sns.violinplot

</div>

<div class="cell code" execution_count="51" id="kxYNuQx54Gxu">

``` python
import matplotlib.pyplot as plt
import seaborn as sns
plt.rcParams['figure.figsize'] = [10, 5]

sns.set()
```

</div>

<div class="cell code" execution_count="52"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;,&quot;height&quot;:661}"
id="Kh81000G4RwQ" outputId="26b7d6e4-7313-478b-cde2-914cdb5097dd">

``` python
sns.histplot(df, x='MARK PERCENTAGE (%)')
plt.show()

sns.violinplot(x=df['MARK PERCENTAGE (%)'])
plt.show()
```

<div class="output display_data">

![](802581cc93111e08563e7059224a4836640ad34f.png)

</div>

<div class="output display_data">

![](5710cd37300c7438fd55a75b86e67a87c6ca1496.png)

</div>

</div>

<div class="cell markdown" id="upak4e1Q5Mro">

## How many MARK PERCENTAGE (%) higher than 80 in the dataset?

</div>

<div class="cell code" execution_count="57"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;}"
id="pK9D-_RF5MWf" outputId="7c0bec80-7633-4e12-f06e-8cc7df3c0a79">

``` python
len(df[df['MARK PERCENTAGE (%)'] > 80])
```

<div class="output execute_result" execution_count="57">

    25

</div>

</div>

<div class="cell markdown" id="EnLLnwqmxbWj">

## Which SEX results higher on average

</div>

<div class="cell code" execution_count="28"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;}"
id="MIU_b-Haxa-2" outputId="dc9be071-8d1a-4d4a-805e-88eb92f223f6">

``` python
df.groupby('SEX')['MARK PERCENTAGE (%)'].mean()
```

<div class="output execute_result" execution_count="28">

    SEX
    FEMALE    61.8200
    MALE      66.5075
    Name: MARK PERCENTAGE (%), dtype: float64

</div>

</div>

<div class="cell markdown" id="6srnB7p4yHwN">

The result of male is higher than female.

</div>
