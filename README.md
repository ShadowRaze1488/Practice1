# Practice1
Pratice-1

In [19]:
# КЛАСТЕРИЗАЦИЯ МЕТОДОМ K-СРЕДНИХ.

# Импорт необходимых библиотек.

import numpy as np
import matplotlib.pyplot as plt
from sklearn.datasets import make_blobs
In [20]:
# Генерируем датасет при помощи функции make_blobs() - она генерирует данные 
# из изотропных гауссовых распределений. В качестве аргумента можно указать 
# количество объектов, количество центров и стандартное отклонение каждого кластера.

dataset = make_blobs(n_samples=200,
                    centers=4,
                    n_features=2,
                    cluster_std=1.6,
                    random_state=50)
In [21]:
points = dataset[0]
In [22]:
# Для использования метода K-средних, импортируем соответствующий класс из scikit-learn.

from sklearn.cluster import KMeans
In [23]:
# Создадим экземпляр класса KMeans с параметром n_clusters=4 и присвоим его переменной kmeans.

kmeans = KMeans(n_clusters=4)
In [24]:
# Обучим нашу модель, вызвав на ней метод fit
# и передав объект KMeans в наш датасет.

kmeans.fit(points)
Out[24]:
KMeans(n_clusters=4)
In [25]:
# Создадим диаграмму рассеяния, используя plt.scatter().

plt.scatter(dataset[0][:,0], dataset[0][:,1])
Out[25]:
<matplotlib.collections.PathCollection at 0x2314e90e520>

In [26]:
# Центры кластеров в соответствии с оценкой K-средних.

clusters = kmeans.cluster_centers_
In [27]:
# Выведем координаты центров кластеров.

print(clusters)
[[-2.40167949 10.17352695]
 [ 0.05161133 -5.35489826]
 [-5.56465793 -2.34988939]
 [-1.92101646  5.21673484]]
In [28]:
# Сохранение новых кластеров для диаграммы.

y_km = kmeans.fit_predict(points)
In [29]:
# Визаулизация алгоритма кластеризации K-средних. 
# Центры кластеров подсвечены маркером.

plt.scatter(points[y_km == 0,0], points[y_km == 0,1], s=50, color='red')
plt.scatter(points[y_km == 1,0], points[y_km == 1,1], s=50, color='green')
plt.scatter(points[y_km == 2,0], points[y_km == 2,1], s=50, color='yellow')
plt.scatter(points[y_km == 3,0], points[y_km == 3,1], s=50, color='cyan')

plt.scatter(clusters[0][0], clusters[0][1], marker='*', s=50, color='black')
plt.scatter(clusters[1][0], clusters[1][1], marker='*', s=50, color='black')
plt.scatter(clusters[2][0], clusters[2][1], marker='*', s=50, color='black')
plt.scatter(clusters[3][0], clusters[3][1], marker='*', s=50, color='black')

plt.show()
