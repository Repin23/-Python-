1. Постройте график
Назовите график
Сделайте именование оси x и оси y
Сделайте выводы

import pandas as pd

df = pd.read_csv('kc_house_data.csv', sep=',')
df.head()
id	date	price	bedrooms	bathrooms	sqft_living	sqft_lot	floors	waterfront	view	...	grade	sqft_above	sqft_basement	yr_built	yr_renovated	zipcode	lat	long	sqft_living15	sqft_lot15
0	7129300520	20141013T000000	221900.0	3	1.00	1180	5650	1.0	0	0	...	7	1180	0	1955	0	98178	47.5112	-122.257	1340	5650
1	6414100192	20141209T000000	538000.0	3	2.25	2570	7242	2.0	0	0	...	7	2170	400	1951	1991	98125	47.7210	-122.319	1690	7639
2	5631500400	20150225T000000	180000.0	2	1.00	770	10000	1.0	0	0	...	6	770	0	1933	0	98028	47.7379	-122.233	2720	8062
3	2487200875	20141209T000000	604000.0	4	3.00	1960	5000	1.0	0	0	...	7	1050	910	1965	0	98136	47.5208	-122.393	1360	5000
4	1954400510	20150218T000000	510000.0	3	2.00	1680	8080	1.0	0	0	...	8	1680	0	1987	0	98074	47.6168	-122.045	1800	7503
5 rows × 21 columns


import sys
import matplotlib
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd

plt.hist(df['price'])
plt.title('Распределение стоимости')
plt.xlabel('Цена')
plt.ylabel('Количество');

вывод:

Колличество домов прямопропорционально их цене

[1.docx](https://github.com/Repin23/-Python-/files/14602534/1.docx)


2. Скачать следующие данные: kc-house-data и laptop_price
https://gbcdn.mrgcdn.ru/uploads/asset/4266730/attachment/08ec55854637add5247d22396d0f7456.csv
Изучите стоимости недвижимости
Изучите распределение квадратуры жилой
Изучите распределение года постройки

plt.hist(df['sqft_living'])
plt.title('Распределение жилой площади')
plt.xlabel('распределение жилой квадратуры')
plt.ylabel('Количество')

Text(0, 0.5, 'Количество')
[2.docx](https://github.com/Repin23/-Python-/files/14602579/2.docx)


plt.hist(df['yr_built'])
plt.title('Распределение года постройки')
plt.xlabel('год постройки')
plt.ylabel('Количество');
[3.docx](https://github.com/Repin23/-Python-/files/14602603/3.docx)

3. Изучите распределение домов от наличия вида на набережную
vid = df['waterfront'].value_counts()
vid.head()
0    21450
1      163
Name: waterfront, dtype: int64
plt.hist(df['waterfront'])
plt.title('Распределение домов от наличия вида на набережную')
plt.xlabel('вид на набережную')
plt.ylabel('Количество')
Text(0, 0.5, 'Количество')
[4.docx](https://github.com/Repin23/-Python-/files/14602621/4.docx)

Вывод:

Количество домов с видом на набережную в десятки тысяч раз меньше, чем без вида на неё
[5.docx](https://github.com/Repin23/-Python-/files/14602686/5.docx)


Изучите распределение этажей домов
df['floors'].value_counts()
1.0    10680
2.0     8241
1.5     1910
3.0      613
2.5      161
3.5        8
Name: floors, dtype: int64
plt.hist(df['floors'])
plt.title('Изучение распределения этажей домов')
plt.xlabel('Этажи')
plt.ylabel('Количество домов')
Text(0, 0.5, 'Количество домов')
[6.docx](https://github.com/Repin23/-Python-/files/14602695/6.docx)


Изучите распределение состояния домов

df['view'].value_counts()
0    19489
2      963
3      510
1      332
4      319
Name: view, dtype: int64
plt.hist(df['view'])
plt.title('Изучение распределения состояния домов')
plt.xlabel('Оценка')
plt.ylabel('Количество домов')
[7.docx](https://github.com/Repin23/-Python-/files/14602707/7.docx)



Исследуйте, какие характеристики недвижимости влияют на стоимость недвижимости, с применением не менее 5 диаграмм из урока.

Анализ сделайте в формате storytelling: дополнить каждый график письменными выводами и наблюдениями.

corr_matrix = df.corr()
corr_matrix = np.round(corr_matrix, 1)
corr_matrix[np.abs(corr_matrix) < 0.3] = 0
corr_matrix

	id	price	bedrooms	bathrooms	sqft_living	sqft_lot	floors	waterfront	view	condition	grade	sqft_above	sqft_basement	yr_built	yr_renovated	zipcode	lat	long	sqft_living15	sqft_lot15
id	1.0	0.0	0.0	0.0	0.0	0.0	0.0	0.0	0.0	0.0	0.0	0.0	0.0	0.0	0.0	0.0	0.0	0.0	0.0	0.0
price	0.0	1.0	0.3	0.5	0.7	0.0	0.3	0.3	0.4	0.0	0.7	0.6	0.3	0.0	0.0	0.0	0.3	0.0	0.6	0.0
bedrooms	0.0	0.3	1.0	0.5	0.6	0.0	0.0	0.0	0.0	0.0	0.4	0.5	0.3	0.0	0.0	0.0	0.0	0.0	0.4	0.0
bathrooms	0.0	0.5	0.5	1.0	0.8	0.0	0.5	0.0	0.0	0.0	0.7	0.7	0.3	0.5	0.0	0.0	0.0	0.0	0.6	0.0
sqft_living	0.0	0.7	0.6	0.8	1.0	0.0	0.4	0.0	0.3	0.0	0.8	0.9	0.4	0.3	0.0	0.0	0.0	0.0	0.8	0.0
sqft_lot	0.0	0.0	0.0	0.0	0.0	1.0	0.0	0.0	0.0	0.0	0.0	0.0	0.0	0.0	0.0	0.0	0.0	0.0	0.0	0.7
floors	0.0	0.3	0.0	0.5	0.4	0.0	1.0	0.0	0.0	-0.3	0.5	0.5	0.0	0.5	0.0	0.0	0.0	0.0	0.3	0.0
waterfront	0.0	0.3	0.0	0.0	0.0	0.0	0.0	1.0	0.4	0.0	0.0	0.0	0.0	0.0	0.0	0.0	0.0	0.0	0.0	0.0
view	0.0	0.4	0.0	0.0	0.3	0.0	0.0	0.4	1.0	0.0	0.3	0.0	0.3	0.0	0.0	0.0	0.0	0.0	0.3	0.0
condition	0.0	0.0	0.0	0.0	0.0	0.0	-0.3	0.0	0.0	1.0	0.0	0.0	0.0	-0.4	0.0	0.0	0.0	0.0	0.0	0.0
grade	0.0	0.7	0.4	0.7	0.8	0.0	0.5	0.0	0.3	0.0	1.0	0.8	0.0	0.4	0.0	0.0	0.0	0.0	0.7	0.0
sqft_above	0.0	0.6	0.5	0.7	0.9	0.0	0.5	0.0	0.0	0.0	0.8	1.0	0.0	0.4	0.0	-0.3	0.0	0.3	0.7	0.0
sqft_basement	0.0	0.3	0.3	0.3	0.4	0.0	0.0	0.0	0.3	0.0	0.0	0.0	1.0	0.0	0.0	0.0	0.0	0.0	0.0	0.0
yr_built	0.0	0.0	0.0	0.5	0.3	0.0	0.5	0.0	0.0	-0.4	0.4	0.4	0.0	1.0	0.0	-0.3	0.0	0.4	0.3	0.0
yr_renovated	0.0	0.0	0.0	0.0	0.0	0.0	0.0	0.0	0.0	0.0	0.0	0.0	0.0	0.0	1.0	0.0	0.0	0.0	0.0	0.0
zipcode	0.0	0.0	0.0	0.0	0.0	0.0	0.0	0.0	0.0	0.0	0.0	-0.3	0.0	-0.3	0.0	1.0	0.3	-0.6	-0.3	0.0
lat	0.0	0.3	0.0	0.0	0.0	0.0	0.0	0.0	0.0	0.0	0.0	0.0	0.0	0.0	0.0	0.3	1.0	0.0	0.0	0.0
long	0.0	0.0	0.0	0.0	0.0	0.0	0.0	0.0	0.0	0.0	0.0	0.3	0.0	0.4	0.0	-0.6	0.0	1.0	0.3	0.3
sqft_living15	0.0	0.6	0.4	0.6	0.8	0.0	0.3	0.0	0.3	0.0	0.7	0.7	0.0	0.3	0.0	-0.3	0.0	0.3	1.0	0.0
sqft_lot15	0.0	0.0	0.0	0.0	0.0	0.7	0.0	0.0	0.0	0.0	0.0	0.0	0.0	0.0	0.0	0.0	0.0	0.3	0.0	1.0


import seaborn as sns

plt.figure(figsize=(10, 8))
sns.heatmap(corr_matrix, annot=True, linewidths=.5, cmap='coolwarm');


![2](https://github.com/Repin23/-Python-/assets/139049242/58c983d1-5169-4540-aadd-1b1e284c8b2f)



