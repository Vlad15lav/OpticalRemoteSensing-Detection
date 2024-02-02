# Optical Remote Sensing Detection
Детектирование объектов на спутниковых снимках 🌍🛰

Этот кейс представляет собой систему для детектирования объектов на спутниковых снимках. Система основана на архитектуре YOLOv3 и предназначена для обнаружения объектов, таких как здания, автомобили и другие на спутниковых снимках Земли.

## Оглавление
1. [Постановка задачи](https://github.com/Vlad15lav/ors-detection#постановка-задачи)
2. [Requirements](https://github.com/Vlad15lav/ors-detection#requirements)
3. [Набор данных DIOR](https://github.com/Vlad15lav/ors-detection#набор-данных-dior)
4. [Обучение модели](https://github.com/Vlad15lav/ors-detection#обучение-модели)
5. [Оценка модели](https://github.com/Vlad15lav/ors-detection#оценка-модели)
6. [Демо Inference](https://github.com/Vlad15lav/ors-detection#демо-inference)
7. [Телеграмм бот](https://github.com/Vlad15lav/ors-detection#телеграмм-бот)
8. [Web приложение](https://github.com/Vlad15lav/ors-detection#web-приложение)
9. [Ссылки](https://github.com/Vlad15lav/ors-detection#ссылки)

## Постановка задачи
Целью данного проекта - разработка системы детектирования объектов на оптических спутниковых снимках. На вход подается спутниковое изображение, необходимо выявить расположение и классифицировать разнообразные интересующиеся объекты.

## Requirements
Для установки необходимых зависимостей выполните следующую команду:
```
pip install -U -r requirements.txt
```

Вы также можете ознакомиться с данным репозиторием, преобразование набора данных для задачи детектирования объектов  - [Набор инструментов для детектирования объектов](https://github.com/Vlad15lav/ObjectDetection-Toolkit)

## Набор данных DIOR
Для обучения модели использовался набор данных Detection in Optical Remote.  
DIOR представляет собой крупномасштабный и общедоступный набор изображений для детектирования объектов на оптических спутниковых снимках. В наборе данных содержится 23463 изображения с 192472 объектами, охватывающими 20 классов объектов. DIOR отличается большим разнообразием размеров объектов, различными условиями съемки (погода, сезоны) и качеством изображений. Этот набор данных предоставляет исследователям возможность разрабатывать и проверять методы обнаружения объектов, а также служит базой для сравнения современных подходов в этой области.

Набор данных на [Google Disk](https://drive.google.com/file/d/16JeLkqdOA1oF0WtyYdKnJhq3i9eEcX4_/view?usp=sharing)

### Примеры изображений:
![Пример набора данных](/images/diorset.png)


## Обучение модели
Для начала обучения модели выполните следующую команду:
```bash
python train.py --path data/DIOR-full --cfg dior --img_size 512 --lr 0.005 --epoches 50 --batch_size 12 --debug
```
Для продолжения обучения модели используйте следующую команду:
```bash
python train.py --path data/DIOR-full --cfg dior --img_size 512 --load_train --epoches 50 --batch_size 12 --debug
```

### График обучения:  
![График обучения](/images/YOLOv3-training.jpg)

## Оценка модели
Для оценки модели выполните следующую команду:
```bash
python eval.py --path data/DIOR-full --cfg dior --img_size 512 --batch_size 12
```

**Средний показатель точности обнаружения (mAP):** 73.1%

Для каждого класса объектов был рассчитан показатель точности (AP):

| Класс                     | AP     |
|---------------------------|--------|
| airplane                  | 81.6   |
| airport                   | 76.1   |
| baseballfield             | 84.6   |
| basketballcourt           | 88.6   |
| bridge                    | 48.9   |
| chimney                   | 75.9   |
| dam                       | 61.1   |
| Expressway-Service-area   | 82.9   |
| Expressway-toll-station   | 78.0   |
| golffield                 | 69.1   |
| groundtrackfield          | 86.5   |
| harbor                    | 56.3   |
| overpass                  | 90.4   |
| ship                      | 51.9   |
| stadium                   | 78.4   |
| storagetank               | 88.9   |
| tenniscourt               | 61.1   |
| trainstation              | 56.0   |
| vehicle                   | 89.2   |
| windmill                  | 57.8   |

### Примеры детектирования:  
<img src="/images/test.gif" alt="drawing" width="500"/>

Для загрузки весов YOLOv3 используйте следующую команду:

```bash
wget https://github.com/Vlad15lav/ors-detection/releases/download/weights/dior_weights.pth -O states/dior_weights.pth
```

## Демо Inference
Вы можете использовать следующий простой скрипт:
```bash
python inference.py -p images/test_sample.jpg --cfg dior --img_size 512
```
Этот скрипт позволяет вам быстро проверить работу модели на отдельном изображении без необходимости использовать веб-приложение или выполнения обучения.

### Результат скрипта:
![Результат скрипта](/images/test_sample_result.png)

## Телеграмм бот
Загрузите базу данных MySQL для телеграмм бота:
```bash
mysql -u root -p detector_bot < db/detector_bot.sql
```
В скрипте bot.py укажите данные для MySQL сервера и Token Bot Father:
```python
# Данные для входа в БД и токен Телеграмма
DATABASE_ADDRESS = "YOUR ADDRESS"
DATABASE_USER = "YOUR USER"
DATABASE_PASW = "YOUR PASSWORD"
DATABASE_NAME = "YOUR DATABASE NAME"
BOT_TOKEN = "YOUR TOKEN"
```
Запустите приложение с помощью команды:
```bash
python bot.py
```

## Web приложение
Наше приложение развернуто на платформе Streamlit и готово к использованию прямо сейчас! Теперь вы можете легко ознакомиться с функционалом и возможностями системы для детектирования объектов на оптических спутниковых снимках. Просто перейдите по ссылке [сюда](https://space-detector.streamlit.app/) и начните использовать приложение.

С помощью Web-интерфейса, вы можете загрузить спутниковые снимки, посмотреть результаты обнаружения объектов на снимках и попробовать ввести координаты любой точки Земли, чтобы сразу получить снимок.

![Web-приложение](/images/stremlit-preview.png)

## Ссылки
- [Detection in Optical Remote Sensing Dataset](https://arxiv.org/ftp/arxiv/papers/1909/1909.00133.pdf)
- [You Only Look Once V3](https://arxiv.org/pdf/1804.02767.pdf)
