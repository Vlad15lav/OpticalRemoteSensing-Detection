# Optical Remote Sensing Detection
Детектирование объектов на оптических спутниковых снимках 🌍🛰

Этот кейс представляет собой систему для детектирования объектов на оптических спутниковых снимках. Система основана на архитектуре YOLOv3 и предназначена для обнаружения объектов, таких как здания, автомобили и другие на спутниковых снимках Земли.

## Оглавление
1. [Requirements](https://github.com/Vlad15lav/ors-detection#requirements)
2. [Обучение модели YOLOv3](https://github.com/Vlad15lav/ors-detection#обучение-модели-yolov3)
3. [Оценка модели](https://github.com/Vlad15lav/ors-detection#оценка-модели)
4. [Набор данных DIOR](https://github.com/Vlad15lav/ors-detection#набор-данных-dior)
5. [Ссылки](https://github.com/Vlad15lav/ors-detection#ссылки)

## Requirements
Для установки необходимых зависимостей выполните следующую команду:
```
pip install -U -r requirements.txt
```

Вы также можете ознакомиться с данным репозиторием - [Набор инструментов для детектирования объектов](https://github.com/Vlad15lav/ObjectDetection-Toolkit)

## Обучение модели YOLOv3
Для начала обучения модели выполните следующую команду:
```
python train.py --path data/DIOR-full --cfg dior --img_size 512 --lr 0.005 --epoches 50 --batch_size 12 --debug
```
Для продолжения обучения модели используйте следующую команду:
```
python train.py --path data/DIOR-full --cfg dior --img_size 512 --load_train --epoches 50 --batch_size 12 --debug
```

## Оценка модели
Для оценки модели выполните следующую команду:
```
python eval.py --path data/DIOR-full --cfg dior --img_size 512 --batch_size 12
```

![Пример детектирования](/images/test.gif)

## Набор данных DIOR
![Пример набора данных](/images/diorset.png)

Для загрузки весов YOLOv3 используйте следующую команду:

```
wget https://github.com/Vlad15lav/ors-detection/releases/download/weights/dior_weights.pth -O states/dior_weights.pth
```

## Ссылки
- [Detection in Optical Remote Sensing Dataset](https://arxiv.org/ftp/arxiv/papers/1909/1909.00133.pdf)
- [You Only Look Once V3](https://arxiv.org/pdf/1804.02767.pdf)
