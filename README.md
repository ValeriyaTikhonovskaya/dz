# Анализ рынка труда в сфере IT
## Цель проекта
Данный проект сделан с целью анализа предложения труда на рынке в сфере IT-специалистов. Основной его целью является анализ неценовых факторов предложения труда и с последующим разделением работников на группы по качеству предоставляемых услуг.
## Основные этапы
1. ### Сбор данных

Сбор данных осущетсвлялся путем парсинга сайта hh.ru. Единицей наблюдения является человек, выставляющий свои услуги, с целью поиска работы.

Основными признаками предварительно были выбраны все возможные факторы, указанные на сайте, влиющие на возможность и качество работы соискателя:

*  `опыт работы` -- непрерывный признак, отоображающий количество лет, которое человек проработал;
*  `регион` -- категориальный признак, город, область где человек ищет работу;
*  `пол` -- категориальный признак, мужчина или женщина (третьего не дано);
*  `возраст` -- непрерывный признак, показывающий сколько лет человеку,;
*  `вуз` -- категориальный признак, вуз, в котором человек учился (без образования, если такового не имеется);
*  `образование` -- категориальный признак, показывающее, какое образование у человека;
*  `язык` -- категориальный признак, языки, которые знает соискатель и на каком уровне;
*  `желаемая з/п` -- непрерывный признак, отображает зарплату, которую человек выставил, в качестве желаемой;
*  `занятость` -- категориальный признак, показывает, в каком режиме, хотел бы работать айтишник.

2. ### Очистка данных

Как уже было сказано раннее, сбор данных проводился с сайта hh.ru, где большая часть заполняется самим пользователем произвольной информацией. По этой причине, итоговый датасет был сильно упрощен, а именно:

* `язык` остался только английский, поэтому данный столбец после OHE-кодировния имеет значение в ячейке 1, если человек знает английски на B2+, или 0 в остальных случаях;
* столбец `регион` стал иметь три возможных значения: Москва, Санкт-Петербург и другое, позже данный признак был преобразован в dummy-переменную;
* столбец `ВУЗ` был удален, так как оказалось, что их (ВУЗов) примерно столько же, сколько и наблюдний;
* `образование` было переделано в двоичную кодировку по следующему приницпу: есть высшее образование -- 1, нет -- 0.
Оставшиеся признаки были подвергнуты рутинной чистке, с целью сделать их более удобными для дальнейшего анализа.

3. ###  EDA

В данном разделе мы представили:

* гистограммы непрерывных переменных;
* ящики с усами для непрерыных перменных (и споследующее удаление выбросов);
* столбчатые диаграммы для категиориальных;
* облака точек, где по оси ординат представлены значения переменной `желаемая з/п`, а по оси абсцисс значения всех возможных оставшихся признаков;

4. ###  Машинное обучение
   
Изначально, основной целью данного раздела являлось построение регрессии `желаемая з/п`. Однако ни линейная, ни полиномиальная, ни логарифмическая, ни модель случайного леса, градиентного бустинга нам не подошли в силу особенностей наших данных.
Поэтому было выбрано сосредоточиться на задаче кластеризации, отбросив желание построить регрессию (с неудачными результатами можно ознакомиться в первой части данного раздела)

Как итог получаем 4 кластера -- 4 основные группы, что не сложно интерпретировать: джуны, мидлы, синьоры, и тим лиды


