# Привязка и цифрование туристской карты {#map-ref-general}

## Введение

**Цель задания** --- знакомство с привязкой, трансформированием и цифрованием геоизображений.

Параметр                    Значение
--------------------------  ----
*Поток*                     <kbd>Общий</kbd>
*Теоретическая подготовка*  Системы координат и проекции на картах, привязка геоизображений, трансформирование геоизображений, цифрование геоизображений. Методы трансформации: аффинное, проективное, полиномиальное, метод резинового листа (сплайны).
*Практическая подготовка*   Знание основных компонент интерфейса ArcGIS Desktop (каталог, таблица содержания, карта). Работа с базой геоданных. Настройка символики и подписей объектов.
*Исходные данные*           Растровые карты для привязки, база пространственных данных на территорию Швейцарии.
*Результат*                 База данных со следующими слоями: границы природных зон; линии туристического маршрута; остановки вдоль маршрута; проект карты карта с компоновкой
*Ключевые слова*            Системы координат, проекции, трансформирование координат, пространственная привязка, цифрование, классы пространственных объектов, база пространственных данных,

### Контрольный лист

* Привязать растровые карты к опорным данным
* Создать базу геоданных и классы пространственных объектов
* Наполнить классы пространственных объектов путем цифрования привязанных карт
* Наполнить атрибуты объектов значениями
* Разработать символику и подписи для слоев карты
* Подготовить компоновку карты
* Экспортировать карту в графический файл

### Аннотация

Задание посвящено знакомству с привязкой растровых карт, созданием и наполнением баз пространственных данных путем цифрования, оформлением карт на их основе.

В задании предлагается привязать в координатную систему карту природных зон и карту туристического маршрута по территории Швейцарии. По результатам цифрования этих карт вы составите туристскую карту, показывающую прохождение маршрута по разным природным зонам.

## Привязка карт
[К содержанию ⇡](#привязка-и-цифрование-туристской-карты)

1. Добавьте на карту слой *Countries* из базы данных упражнения 3.

2. Добавьте на карту растр *SwissRegions.gif*. Появится диалог, предупреждающий вас, что добавляемый файл не имеет пространственной привязки. Нажмите **ОК**:

    ![](images/Ex07/image8.png)

1. Убедитесь, что контур страны отображается примерно посередине экрана.

2. Откройте панель инструментов **Georeferencing**. Выберите в меню команду **Fit to Display**, чтобы переместить непривязанный растр на середину области отображения:

    ![](images/Ex07/image9.png)

1. Сделайте растровый слой прозрачным на *50%*.

2. Используя **инструмент расстановки контрольных точек**, укажите *3-6* соответствующих точек по границе страны на характерных выступах контура:

    ![](images/Ex07/image10.png)

1. Выберите команду меню **Georeferencing > Update Georeferencing**, чтобы завершить привязку растра. При этом по умолчанию будет примененоаффинное преобразование с минимизацией среднеквадратической ошибки отклонения исходных и целевых координат:

    ![](images/Ex07/image11.png)

1. Добавьте на карту слой *WineSafariRoute.jpg*.

2. Выберите его в списке на панели **Georeferencing**:

    ![](images/Ex07/image12.png)

1. Отключите слой *SwissRegions.gif* в таблице содержания.

2. Привяжите растр *WineSafariRoute* аналогично предыдущему растру, используя контрольные точки:

    ![](images/Ex07/image13.png)

1.Выберите команду **Georeferencing > Update georeferencing**, чтобы завершить привязку второго растра.

## Создание базы данных и классов пространственных объектов
[К содержанию ⇡](#привязка-и-цифрование-туристской-карты)

1. Создайте в папке *Ex5* базу геоданных под названием *RouteMap.gdb*.

2. Создайте в базе данных *классы пространственных объектов* со следующими параметрами:

Название  Модель пространственных объектов  Атрибутивные поля Проекция
--------  --------------------------------- ----------------- --------  
*Regions* Полигональная (polygon features)  NAME (text)       `WGS_1984_UTM_Zone_32N` (импортируйте у слоя карты)
*Routes*  Линейная (line features)          -                 `WGS_1984_UTM_Zone_32N` (импортируйте у слоя карты)
*Places*  Точечная (point features)         NAME (text)       `WGS_1984_UTM_Zone_32N` (импортируйте у слоя карты)

По завершению создания слоев они автоматически будут добавлены на карту:

![](images/Ex07/image14.png)

## Цифрование регионов
[К содержанию ⇡](#привязка-и-цифрование-туристской-карты)

1. Оставьте включенными только слои *Regions*, *SwissRegions* и *Countries*.

2. Уберите *прозрачность* у слоя *SwissRegions*.

3. Откройте сеанс редактирования для слоя *Regions*. Появится панель редактирования **Editor**, а также окно шаблонов объектов **Create Features**:

    ![](images/Ex07/image15.png)

1. Щелкните на шаблоне объекта *Regions* в окне **Create Features** и выберите режим цифрования **Polygon**:

    ![](images/Ex07/image16.png)

1. Оцифруйте регион *Prealpine Zones* в центре карты. По завершению дважды щелкните мышкой:

    ![](images/Ex07/image17.png)

1. Чтобы появилась возможность пристыковать остальные регионы к границам стран, **выделите** в слое *Countries* все страны, кроме Швейцарии, **скопируйте** их в буфер обмена и **вставьте** в слой *Regions*:

    ![](images/Ex07/image18.png)

1. Выделите опять шаблон *Regions* в окне **Create Features**.

2. Используя режим **Auto-Complete Polygon**, оцифруйте границы оставшихся регионов в следующем порядке:

    - Сначала небольшие регионы, примыкающие к границам:

        ![](images/Ex07/image19.png)

    - Затем область второго порядка (горы *Юра*):

        ![](images/Ex07/image20.png)

    - Наконец, границу между центральными регионами:

        ![](images/Ex07/image21.png)

1. Выделите в слое *Regions* границы стран и удалите их.

2. Выберите команду **Editor > Save Edits**, чтобы сохранить результаты редактирования.

*Результат*:
![](images/Ex07/image22.png)

## Атрибутирование регионов
[К содержанию ⇡](#привязка-и-цифрование-туристской-карты)

1. Уберите заливку регионов, линии сделайте толщиной 1.5-2 пиксела:

    ![](images/Ex07/image23.png)

1. Откройте атрибутивную таблицу слоя *Regions*.

2. Поочередно выделяя каждый объект в таблице или на карте, заполните его атрибуты в соответствии с легендой:

    ![](images/Ex07/image24.png)

1. Сохраните изменения и завершите сеанс редактирования.

## Цифрование маршрутов и точек интереса
[К содержанию ⇡](#привязка-и-цифрование-туристской-карты)

1. Выключите слои *Regions* и *SwissRegions.gif*.

2. Включите слои *WinSafariRoute*, *Routes* и *Places*.

3. Оцифруйте объекты слоев *Places* и *Routes*, используя инструменты панели **Сreate Features**:

    - Начните с расстановки точек:

        ![](images/Ex07/image25.png)

    - Увеличьте масштаб, чтобы были хорошо видны изгибы линий:

        ![](images/Ex07/image26.png)

    - Проведите линии через получившиеся точки, повторяя контур исходной линии на растровой подложке. Каждую линию начинайте в точке и завершайте двойным щелчком в перекрестке:

        ![](images/Ex07/image27.png)

    *Результат*:
    ![](images/Ex07/image28.png)

1. Заполните названия городов в слое *Places*.

    ![](images/Ex07/image29.png)

1. Сохраните изменения и завершите сеанс редактирования.

## Оформление карты
[К содержанию ⇡](#привязка-и-цифрование-туристской-карты)

1. Оставьте включенными слои *Regions*, *Routes*, *Places* и *Countries*. Остальные слои выключите.

2. Уберите заливку у слоя *Countries*.

3. Оформите слой *Regions* методом категорий по полю *NAME*:

    ![](images/Ex07/image30.png)

1. Оформите слои *Routes* и *Places* по аналогии с нижеприведенным фрагментом:

    ![](images/Ex07/image31.png)

1. Откройте панель **Labeling** и включите **Maplex** для размещения подписей.

2. Включите подписи для слоя *Places* со следующими настройками:

    Параметр                Значение
    ----------------------- ---------
    *Поле для подписей*     NAME
    *Шрифт*                 Tahoma
    *Кегль (размер)*        12
    *Цвет*                  Черный
    *Начертание*            Обычное

    *Результат*:
    ![](images/Ex07/image32.png)

Некоторые подписи могут быть размещены не очень удачно. Чтобы они не перекрывали линии маршрута и значки выполните следующие действия:

1. Откройте *настройки весов подписей* **Label Weight Ranking** на панели **Labeling**

2. Установите вес равным $1000$ слоям *Places* и *Routes:*

    ![](images/Ex07/image33.png)

    *Результат*:
    ![](images/Ex07/image34.png)

1. Добавьте на карту слой *Hillshade* из базы данных упражнения 3, разместите его над слоем Regions и установите прозрачность $80%$.

    *Результат*:
    ![](images/Ex07/image35.png)

1. Добавьте на карту слой *Lakes* и присвойте ему символ полигона с голубой заливкой без обводки.

    *Результат*:
    ![](images/Ex07/image36.png)

## Компоновка карты
[К содержанию ⇡](#привязка-и-цифрование-туристской-карты)

1. Переключитесь в **режим компоновки**.

2. Установите альбомную ориентировку листа.

3. Оформите компоновку в соответствии с нижеприведенным образцом:

    ![](images/Ex07/image37.png)

1. Экспортируйте карту в формат <kbd>PNG</kbd> с разрешением $300~dpi$.

2. Сохраните документ карты.

## Контрольные вопросы
[К содержанию ⇡](#привязка-и-цифрование-туристской-карты)