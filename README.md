# Проект 5. Выбираем авто выгодно  
## Юнит 6. Основные алгоритмы машинного обучения. Часть II  
### skillfactory_rds  
![https://img.shields.io/badge/Python-3.7.4-blue](https://img.shields.io/badge/Python-3.7.4-blue)

## Оглавление  
[1. Описание модуля](https://github.com/dst10rds6/rds6/blob/master/README.md#Описание-модуля)  
[2. Какой кейс решаем?](https://github.com/dst10rds6/rds6/blob/master/README.md#Какой-кейс-решаем?)  
[3. Краткая информация о данных](https://github.com/dst10rds6/rds6/blob/master/README.md#Краткая-информация-о-данных)  
[3. Этапы работы над проектом](https://github.com/dst10rds6/rds6/blob/master/README.md#Этапы-работы-над-проектом)  
[4. Результат](https://github.com/dst10rds6/rds6/blob/master/README.md#Результат)  

### Описание модуля  
Вы работаете в компании, которая занимается продажей автомобилей с пробегом в Москве. В этом модуле вам предстоит выполнить просьбу руководства компании и создать модель, которая будет предсказывать стоимость автомобиля по его характеристикам  

***Чем мы будем заниматься?***  
- Применим на практике знания о парсинге  
- Применим на практике знания ML и то чему мы обучились на предыдущих юнитах в создании модели по предсказанию цен на авто.  
- Поучаствуем в соревновании на kaggle  
:arrow_up:[к оглавлению](https://github.com/dst10rds6/rds6/blob/master/README.md#Оглавление)

### Какой кейс решаем?
Вы работаете в компании, которая занимается продажей автомобилей с пробегом в Москве.  
Основная задача компании и её менеджеров — максимально быстро находить выгодные предложения (проще говоря, купить ниже рынка, а продать дороже рынка).  
Руководство компании просит вашу команду создать модель, которая будет предсказывать стоимость автомобиля по его характеристикам.  
Если такая модель будет работать хорошо, то вы сможете быстро выявлять выгодные предложения (когда желаемая цена продавца ниже предсказанной рыночной цены). Это значительно ускорит работу менеджеров и повысит прибыль компании.  
Только вот незадача: исторически сложилось, что компания изначально не собирала данные. Есть только небольшой датасет с историей продаж за короткий период, которого для обучения модели будет явно мало. Его мы будем использовать для теста, остальное придется собрать самим.  

**Условия соревнования:**  
[Ссылка](https://www.kaggle.com/c/sf-dst-car-price/overview) на закрытое соревнование. 
- Данное соревнование является бессрочным и доступно для всех потоков.
- Срок выполнения соревнования устанавливаеться индивидуально в каждом потоке.
- Тестовая выборка представлена в ЛидерБорде целиком.
- По этому лучшие и победные решения буду проверяться на их "адекватность" (чтоб не было подгонки под тестовую выборку).
- Разрешено использовать внешние данные. (но их источник должен быть публичным и доступен всем участникам соревнования)
- Разрешено использовать любые ML алгоритмы и библиотеки. (кроме DL)
- Даже если удасться найти исходные объявления из теста - нельзя просто указать их цену.   Делаем реальный ML продукт, который потом сможет нормально работать на новых данных.

**Метрика качества**
Результаты оцениваются по метрике MAPE.  
MAPE  (Mean Percentage Absolute Error) расшифровывается выражение как средняя абсолютная ошибка в процентах.
$MAPE=\frac{1}{n}\sum_{t=1}^{n}\frac{\left | Y_t-\hat{Y_t} \right |}{Y_t}$
,  
где:  
- $Y_t$ — фактическое значение за анализируемый период;  
- $\hat{Y_t}$ — значение прогнозной модели за анализируемый период;  
- $n$ — количество периодов.  
:arrow_up:[к оглавлению](https://github.com/dst10rds6/rds6/blob/master/README.md#Оглавление)

### Краткая информация о данных
Train датасета (для обучения моделей) нет. Вам его нужно собрать самим! Вспоминаем модуль по парсингу сайтов или ищем готовые датасеты.  

Мы спарсили все объявления авто.ру на 9.9.2020 за примерно 1 час. С ноутбуком для парсинга можно ознакомиться [тут](https://github.com/dst10rds6/rds6/tree/master/parsing
)

Тренировочный датасет содержит характеристики автомобилей из объявлений про продаже авто с сайта.  

Описание полей датасета:  
- bodyType - тип кузова автомобиля (https://ru.wikipedia.org/wiki/Типы_автомобильных_кузовов)
- brand - марка (бренд) автомобиля
- color	- цвет автомобиля (16 цветов: чёрный, красный, синий, серебристый, зелёный, белый, серый, голубой, пурпурный, коричневый, золотистый, фиолетовый, жёлтый, оранжевый, розовый)
- fuelType - тип топлива (5 видов топлива: бензин, дизель, электро, гибрид, газ)
- modelDate - дата выпуска модели (не путать с датой производства)
- name - комбинация нескольких характеристик (модели, объема двигателя и привода)
- numberOfDoors - кол-во дверей
- productionDate - дата производства авто
- vehicleConfiguration - комбинация типа трансмиссии, объема двигателя и мощности двигателя
- vehicleTransmission - тип трансмиссии (коробки передач) (4 вида: автоматическая, механическая, роботизированная, вариатор)
- engineDisplacement - объем двигателя в литрах
- enginePower - мощность двигателя (л.с.)
- description - дополнительные характеристики по комплектации авто
- mileage - пробег автомобиля (км.) - представляет собой общее количество километров, которое это транспортное средство проехало по дорогам с момента своего схода с конвейера производителя. 
- Комплектация - дополнительные характеристики по комплектации авто
- Привод - характеристика привода автомобиля, которое передает энергию от двигателя на колеса. Переднеприводные автомобили получают всю энергию двигателя на передние колеса. При заднем приводе энергия двигателя целиком поступает на задние колеса. Когда энергия двигателя передается на все четыре колеса автомобиля, такой привод является полным ('полный', 'передний', 'задний')
- Руль - характеристика руля по стороне расположения руля в автомобиле (Левый, Правый)
- Состояние - характеристика (необходимости проведения ремонта - требует ремонта или не требует ремонта)
- Владельцы - кол-во владельцев (3 значения: 1 владелец, 2 владельца, 3 и более)
- ПТС - тип ПТС (паспорт технического средства)(2 значения - оригинал, дубликат)
- Таможня - информация о том расстаможен автомобиль или нет (2 значения - Растаможен, Не ратаможен)
- Владение - срок владения автомобилем в годах и месяцах
- price - цена указанная в объявлении на авто.ру
- start_date - дата размещения объявления на авто.ру
- hidden - характеристика объявления на авто.ру
- model - название модели автомобиля (не путать с маркой (брендом), например: бренд или марка - BMW, модель - M6)

датасет всех объявлений по Москве с радиусом 200 км на 9.9.2020 - [тут](https://www.kaggle.com/sokolovaleks/parsing-all-moscow-auto-ru-09-09-2020)
датасет с всеми возможными марками и моделями авто для сайта авто_ру - [тут](https://www.kaggle.com/sokolovaleks/all-brands-and-models-for-auto-ru-09-09-2020)
:arrow_up:[к оглавлению](https://github.com/dst10rds6/rds6/blob/master/README.md#Оглавление)

### Этапы работы над проектом  
- это был групповой проект Альмира, Андрей и Соколов (в рамках груповой работы мы сформировали отдельный [гит на гитхабе](https://github.com/dst10rds6/rds6) для удобной работы с одной веткой мастер и [дешборд](https://github.com/dst10rds6/rds6) со всей необходимой информацией для совместной работы)
- первоначально мы работали с Альмирой, но позже к нам присоединился Андрей, который взял на себя EDA и сильно усилил нас  
- Альмира успешно взяла на себя модели 
- я взял на себя парсинг и предподготовку датасета к EDA
- во время работы мы использовали случайный лес, логистическую регессию в метамодели, беггинг на экстраделевьях и стеккинг
- существенное различие первоначальных датасетов для соревнования очень усложнилос работу, но мы смогли подобрать коэффициенты для корректировки цен из-за курса доллара  
:arrow_up:[к оглавлению](https://github.com/dst10rds6/rds6/blob/master/README.md#Оглавление)

### Результат  
score на kaggle = 0.955 (10 место)  
не хватило времени попробовать больше моделей и интелектуально заполнить параметр модели, которые мы скачали во время парсинга  
:arrow_up:[к оглавлению](https://github.com/dst10rds6/rds6/blob/master/README.md#Оглавление)