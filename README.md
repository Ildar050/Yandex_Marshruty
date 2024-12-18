# Яндекс.Маршруты

 ## Проект 1 спринта 

Яндекс Маршруты — сервис, который строит маршруты для транспорта разных видов, рассчитывает время и стоимость поездки. 
В рамках спринта предстоит подготовить тестовый набор и протестировать: валидацию полей ввода времени и адресов, и логику расчета стоимости и времени поездки на собственном автомобиле.

<details> <summary> Требования по проекту </summary>


 #### Общее описание. 
Яндекс.Маршруты — сервис, который строит маршруты для транспорта разных видов. Рассчитывает время и стоимость поездки.
Чтобы построить маршрут пользователь вводит время отправления, улицу и номер дома. Пользователь может выбрать несколько режимов передвижения по маршруту: «Оптимальный», «Быстрый», «Свой».

#### Макеты.
![image](https://github.com/Ildar050/Yandex_Marshruty/blob/main/assets/m1.jpg)
![image](https://github.com/Ildar050/Yandex_Marshruty/blob/main/assets/m2.jpg)
![image](https://github.com/Ildar050/Yandex_Marshruty/blob/main/assets/m3.jpg)

#### Описание работы интерфейса.
В интерфейсе есть поля «Время начала поездки», «Откуда», «Куда». Переключатели режимов маршрута: «Оптимальный», «Быстрый» и «Свой», а также переключатели видов транспорта: свой автомобиль, каршеринг, такси, самокат, велосипед и пешком.
В стартовом состоянии поля «Время начала поездки», «Откуда» и «Куда» пустые. Режимы маршрутов «Оптимальный», «Быстрый и «Свой» не выбраны; панель переключения видов транспорта неактивна.

#### "Режим "Оптимальный" и "Быстрый".
Если выбрать режим «Оптимальный» или «Быстрый», система автоматически назначит вид транспорта; построится маршрут; отобразится время и стоимость поездки. Выбрать транспорт в этих режимах нельзя — панель видов транспорта неактивна.

#### "Свой".
Если выбрать режим «Свой», панель видов транспорта активна — можно выбрать вид транспорта: Собственный автомобиль, Пешком, Такси, Велосипед, Самокат, Каршеринг. Под каждый вид транспорта строится маршрут; рассчитывается время и стоимость поездки. 
Если сменить вид транспорта или поменять значение в любом поле, маршрут перестроится; время и стоимость поездки пересчитается.

#### Требования к валидации данных в полях.
Валидация полей срабатывает, если фокус уходит из поля. 

Фокус — это состояние элемента интерфейса, когда элемент активен. К нему относятся все действия пользователя. 

Поле ввода часов: Формат 24 часа. Нули перед однозначным числом система выставляет автоматически. Например, 09. Корректны только целые числа от 0 до 23 включительно. При некорректном вводе подсвечивается красным, ошибка «Вы ввели некорректное время». 

Поле ввода минут: Только целые числа. Нули перед однозначным числом система выставляет автоматически. Например, 09. При некорректном вводе подсвечивается красным, ошибка «Вы ввели некорректное время».

Поле ввода адреса (для полей «Откуда» и «Куда»): Только фиксированные адреса из списка (см. пункт требований «Доступные адреса»). Пробелы до и после адреса удаляются при снятии фокуса. При некорректном вводе подсвечивается красным, ошибка «Вы ввели некорректный адрес».

#### Логика расчета маршрута.
Если время начала поездки и адреса заполнены валидными данными, на карте отображаются точки А и В. Если поле «Откуда» заполнено невалидными данными, точка А не отображается. Если поле «Куда» заполнено невалидными данными, точка В не отображается.

На данный момент система построит маршрут только по следующим адресам:

Усачева, 3; Комсомольский проспект, 18; Зубовский бульвар, 37; 
М. Пироговская, 25; Хамовнический Вал, 34; Фрунзенская набережная, 46; 3-я Фрунзенская улица, 12.

Функционал будет дорабатываться, чтобы в будущем можно было вводить любые существующие на карте адреса.

#### Подробнее про логику расчета маршрута.
Система получает данные о начале поездки, точке А и точке В. После этого рассчитывает продолжительность и стоимость поездки по определённому алгоритму.

Стоимость и время поездки зависят от скорости и длины маршрута.
Скорость зависит от времени начала поездки.
Длина маршрута – от точек А и Б на карте и построенного маршрута.

Расчёт времени поездки происходит по формуле: 

t = S/V

Расчёт стоимости поездки происходит по формуле:

Р (итоговая) = S * P (за километр) ИЛИ t * P (за время).

Яндекс Маршруты рассчитывают время и стоимость поездки, в том числе на своем автомобиле. По стоимости указано, что за 1 км. расход составляет 20 руб.


#### Матрица значений скорости и стоимости в зависимости от вида транспорта.

Расстояние, скорость и стоимость за минуту или километр можно получить из таблиц. Этих данных достаточно, чтобы рассчитать время и стоимость поездки для каждого вида транспорта.


| Вид транспорта      |        Скорость        | Стоимость |
| ------------ | :----------------: | ----: |
| Пешком    |  Средняя скорость 4 км/ч   | 0 р / км |
| Шеринг самокатов    | Средняя скорость 10 км/ч |   5,5 р / км |
| Шеринг велосипедов |     Средняя скорость 12 км/ч     |    3 р / км |
|Каршеринг|см. Таблицу «Средняя скорость автомобиля»|9 р / мин|
|Такси|см. Таблицу «Средняя скорость такси»|11 р / мин|
|Собственное авто|см. Таблицу «Средняя скорость автомобиля»|20 р / км|


#### Матрица значений средней скорости автомобиля в зависимости от времени суток поездки
| Время суток | Средняя скорость автомобиля |
| ----------- | :-------------------------: |
| 00:01-08:00 |           45 км/ч           |
| 08:01-12:00 |           30 км/ч           |
| 12:01-18:00 |           40 км/ч           |
| 18:01-22:00 |           25 км/ч           |
| 22:01-00:00 |           45 км/ч           |

#### Матрица расстояний между адресами для автомобильных дорог, в километрах
| Адрес | Усачева, 3 | Комсомольский проспект, 18 | Зубовский бульвар, 37 |Хамовнический Вал, 34
| ------|:---:|:-------:|:---------:|:---------:|
| Усачева, 3 |0 |1.4|1.5|2.6
| Комсомольский проспект, 18|1.4|0|2.9|2.3
| Зубовский бульвар, 37|1.4|1.5|0|3.8
| Хамовнический Вал, 34 |1.5|1.5|2.4|0

#### Алгоритм выбора скорости автомобиля в зависимости от времени поездки

Чтобы рассчитать время и стоимость маршрута, тестировщикам доступны таблицы со скоростью движения разных видов транспорта в разное время суток. 

Если взять такие тестовые значения, что поездка захватит несколько временных интервалов, алгоритм выберет скорость автомобиля из того диапазона, в котором поездка началась

 </details>

 <details> <summary> Задачи </summary>

1. Провести тест-анализ требований на валидацию полей.
2. Создать набор тест-кейсов на проверку валидации полей формы Яндекс Маршрутов. Применить техники тест-дизайна: классы эквивалентности и граничные значения.
3. Протестировать валидацию полей и завести баг-репорты, если есть баги.
4. Провести тест-анализ требований расчёта времени и стоимости маршрута на собственном автомобиле. 
5. Применить технику тест-дизайна «Классы эквивалентности» и создать набор тест-кейсов на проверку правильности расчета времени и стоимости поездки на собственном автомобиле.
6. Протестировать расчеты и завести баг-репорты, если есть баги.
 
  </details>

 <details> <summary> Реализация </summary> 
 
 #### Тестовая документация включающая в себя: Тест-анализ, Классы эквивалентности и граничные значения, Тест-кейсы, Баг-репорты.

  [Проект 1 спринта](https://docs.google.com/spreadsheets/d/1rWzQs96ot4CXB1geR6YU4wnvvPzNokVEJbn--QOsTng/edit?usp=sharing)

 </details>

 ## Проект 2 спринта

 Текущая версия Яндекс Маршрутов отличается от версии из первого спринта. Теперь в приложении можно заказать каршеринг. 

 <details> <summary> Требования по проекту </summary> 
 
 #### Общее описание.

 Пользователю нужно открыть Яндекс.Маршруты и корректно заполнить поля «Откуда» и «Куда». Приложение построит маршрут, а под полями «Откуда» и «Куда» отобразятся режимы поездки: «Оптимальный», «Быстрый», «Свой».

- Если выбрать режим «Оптимальный» или «Быстрый», система автоматически назначит способ передвижения: на авто, пешком, на такси, на самокате, на велосипеде, на каршеринге. Выбрать его самостоятельно нельзя — иконки неактивны.
- Если выбрать режим «Свой», способ передвижения можно поменять — иконки активны.

#### Аренда машины.
Арендовать машину можно в двух случаях:

- Если приложение предлагает тип транспорта «Каршеринг» в режиме «Оптимальный» или «Быстрый».
- Если пользователь выбирает тип транспорта «Каршеринг» в режиме «Свой».

Под названиями режимов появится информация о стоимости и продолжительности поездки, а также кнопка «Забронировать».

Если нажать кнопку «Забронировать», вместо панели с названиями режимов появится форма бронирования. В форме нужно выбрать тариф, добавить информацию о водительских правах, указать способ оплаты. Дополнительно можно перечислить требования к заказу.Под «Требованиями к заказу» расположена кнопка «Забронировать». 

![image](https://github.com/Ildar050/Yandex_Marshruty/blob/main/assets/m2_1.jpg)

#### Форма бронирования.

На экране бронирования можно удалять адреса — они необязательны для заказа каршеринга. Пользователь может выбрать нужную машину на карте.

Ограничения полей

|Наименование поля | Тип поля|Возможные значения|Обязательность|
| --- | :-----: |:----: |:----: |
| Откуда | текстовое поле  |Только буквы русского алфавита, цифры, пробел, тире, точка, запятая. Длина не менее 5 и не более 50 символов. Пробелы до и после адреса исчезают при снятии фокуса. Если пользователь не соблюдает любое из требований, рамка поля подсвечивается красным, а под ней появляется текст ошибки: «Введите корректный адрес».|Нет|
| Куда |   текстовое поле  |Один из вариантов: «Повседневный», «Походный», «Роскошный».|Нет|
| Выбор тарифа каршеринга |  одиночный выбор  |Один из вариантов: «Повседневный», «Походный», «Роскошный».|Да|
| Права |  текстовое поле  |В поля «Имя» и «Фамилия» можно ввести только буквы русского алфавита. В поля «Дата рождения» и «Номер» — только цифры. См. ограничения поля «Добавить права».|Да|
| Способ оплаты |  одиночный выбор |Пользователю доступен один способ оплаты — карта. В поля «Номер карты» и «Код» можно ввести только цифры. См. ограничения поля «Способ оплаты».|Да|
| Требования к заказу |  выпадающее меню  |При клике появляется панель с дополнительными параметрами. См. пункт «Требования к заказу».|Нет|

![image](https://github.com/Ildar050/Yandex_Marshruty/blob/main/assets/m2_2.jpg)

По умолчанию выбран тариф «Повседневный», поля «Добавить права» и «Способ оплаты» не заполнены.

Выбранный тариф подсвечивается серым. Под ним расположен блок с деталями тарифа и информацией о ближайшей машине:

- марка;
- описание тарифа;
- время в пути от пункта «Откуда» до машины — не будет отображаться, если пользователь удалит адрес в поле «Откуда»;
- время бесплатного ожидания;
- изображение машины;
- дополнительные параметры.

Система автоматически выбирает ту машину, которая находится ближе всего к пользователю. На карте иконка ближайшей машины увеличивается, над ней появляется чёрная плашка с маркой машины.

Остальные свободные машины продолжают отображаться на карте в виде иконок. При этом показываются автомобили всех тарифов. Пользователь может выбрать машину на карте и забронировать: он нажимает на иконку, она увеличивается, над ней появляется чёрная плашка с маркой, а на левой панели — обновлённая информация о машине.

Если пользователь ещё не привязал банковскую карту, вместо слова «Карта» стоит слово «Добавить». Без карты забронировать машину нельзя.

По умолчанию приложение показывает точную стоимость поездки. Она рассчитывается по формуле — см. пункт «Формула расчёта тарифов». Если удалить хотя бы один адрес из полей «Откуда» или «Куда», отобразится стартовая цена за минуту.

#### Панель "Выбор тарифа". Описание тарифов

Есть три тарифа. Каждый элемент состоит из иконки автомобиля, названия тарифа, цены.
Один из тарифов всегда выбран. По умолчанию это тариф «Повседневный», но его можно изменить.

Под списком тарифов есть блок с подробным описанием выбранного тарифа

| Тариф | Марка |Заголовок|Подзаголовок|Фичи|
| --- | :--: |:--: |:--: |:--: |
| Повседневный | BMW 750  |Просто по делам, ничего лишнего|n мин — 15 минут бесплатного ожидания|-видеорегистратор -зарядка для телефона|
| Походный | Kia Rio |Для путешествий|n мин — 12 минут бесплатного ожидания|-Bluetooth-двери -походное снаряжение|
| Роскошный |  Porsche 911  |Блеск, мощь, глянец|n мин — 10 минут бесплатного ожидания|-светомузыка -напитки для гостей|

#### Формула расчета стоимости тарифов

Стоимость тарифа рассчитывается по формуле:

*фиксированная стоимость аренды в рублях + (60 * стоимость минуты поездки в рублях * продолжительность поездки в часах) * коэффициент тарифа = стоимость поездки*

Например, стоимость поездки по тарифу «Повседневный»:

*150 + (60 * 6 * 1.25) * 1.5 = 825*

Пояснения к формуле:

- **150** — фиксированная стоимость аренды в рублях;
- **60** — минут в одном часе;
- **6** — стоимость минуты поездки на каршеринге в рублях;
- **1.25** — продолжительность поездки в часах;
- **1.5** — коэффициент тарифа «Повседневный».

**Коэффициенты:**

- Повседневный: 1.5.
- Походный: 2.
- Роскошный: 3.

**Продолжительность поездки** **в часах** рассчитывается так: расстояние / скорость.

- Расстояние — см. таблицу с адресами в общих требованиях.
- Скорость — см. таблицу со скоростями в общих требованиях.

#### Поле "Добавить права"

![image](https://github.com/Ildar050/Yandex_Marshruty/blob/main/assets/m2_3.jpg)

Если не добавить водительское удостоверение, забронировать машину не получится.

По умолчанию поле «Добавить права» не заполнено. Когда пользователь нажимает на поле, появляется окно «Добавление прав». В нём нужно ввести имя, фамилию, дату рождения и номер водительского удостоверения.

Текст, который вводит пользователь, чёрного цвета.

Когда пользователь внёс все данные, появляется сообщение: «Спасибо! Документы отправлены на проверку. Скоро расскажем о результатах». Под сообщением — кнопка «Понятно».

Если нажать кнопку «Понятно», окно закроется, а в поле «Добавить права» появится таймер на 30 секунд. Через 30 секунд система сообщает, прошли ли документы верификацию.

| Наименование поля  | Тип поля | Возможные значения  | Обязательность |
| ----- | :---: | :-------: | :------------: |
| Имя                  | текстовое поле  | Только буквы русского алфавита, пробел, тире. Длина не менее 2 и не более 14 символов. Если пользователь не соблюдает любое из требований, поле подсвечивается красным, появляется текст ошибки: «Введите корректное имя». |      Да        |
| Фамилия                    | текстовое поле  | Только буквы русского алфавита, пробел, тире. Длина не менее 2 и не более 14 символов. Если пользователь не соблюдает любое из требований, поле подсвечивается красным, появляется текст ошибки: «Введите корректную фамилию». |      Да        |
| Дата рождения | цифры| Формат дд.мм.ггггТолько цифры.Ограничения для дд — от 01 до 31 включительно.Ограничения для мм — от 01 до 12 включительно.Ограничения для гггг — от 1880 до 2006 включительно.Точки ставятся автоматически, когда пользователь введёт дату рождения и снимет фокус.Система не даёт вводить иные символы или цифры, которые не входят в диапазон требований. |       Да       |
| Номер                   | цифры  | Формат nn nn nnnnnnТолько цифры.Ограничения для nn — от 01 до 99 включительно.Ограничения для nnnnnn — от 000001 до 999999 включительно.Пробелы ставятся автоматически, когда пользователь введёт номер и снимет фокус.Система не даёт вводить иные символы или цифры, которые не входят в диапазон требований.|       Да       |

#### **После верификации**

Если документы прошли верификацию, рамка поля подсвечивается зелёным, у правого края внутри поля появляется зелёная галочка. Пользователь больше не сможет редактировать данные водительского удостоверения. Несколько водительских удостоверений добавить нельзя.

Если документы не прошли верификацию, рамка поля подсвечивается красным, у правого края внутри поля появляется красный крестик. Если нажать на поле, снова откроется форма «Добавление прав». Над формой — текст сообщения: «Ваши документы не прошли верификацию. Попробуйте ещё раз».

#### Поле «Способ оплаты»

По умолчанию поле не заполнено. Чтобы забронировать машину, нужно ввести реквизиты хотя бы одной карты и нажать кнопку «Привязать». Можно добавить неограниченное количество карт. 

При нажатии на поле «Способ оплаты» открывается окно «Способ оплаты» с возможностью привязать новую карту или выбрать уже привязанную.

Чтобы добавить новую, нужно нажать на кнопку «Добавить карту». После этого откроется окно «Добавление карты».

При успешном добавлении новой карты и нажатии на кнопку «Привязать» происходит переход обратно на форму выбора карт.

Чтобы выбрать карту, её нужно отметить и нажать на кнопку выхода из формы. Если карта одна, она выбирается автоматически.

После выхода из формы поле «Способ оплаты» заполнено данными выбранной карты.

#### Окно «Добавление карты»

![image](https://github.com/Ildar050/Yandex_Marshruty/blob/main/assets/m2_4.jpg)

**Ограничения окна «Добавление карты»**

| Наименование поля | Ограничения |
| ----------- | :-------------------------: |
| Номер карты | Формат nnnn nnnn nnnnТолько цифры. 12 символов.Ограничения для nnnn — от 0000 до 9999 включительно.Пробелы ставятся автоматически, когда пользователь введёт номер и снимет фокус.Если ввести меньше 12 символов, кнопка «Привязать» остаётся неактивной.Больше 12 символов ввести нельзя.Система не даёт вводить иные символы или цифры, которые не входят в диапазон требований.  |
| Код | Формат nnТолько цифры. 2 символа.Ограничения для nn — от 01 до 99 включительно.Если ввести меньше 2 символов, кнопка «Привязать» остаётся неактивной.Больше 2 символов ввести нельзя.Система не даёт вводить иные символы или цифры, которые не входят в диапазон требований.|

Когда карта добавлена, в интерфейсе отображаются последние 4 цифры её номера. Так пользователь может узнавать и отличать свои карты.


#### Панель «Требования к заказу»

Это выпадающий список. Он свёрнут, если выбран тариф по умолчанию — «Повседневный». Если пользователь выбирает другой тариф, список автоматически раскрывается. И наоборот: если вернуться к тарифу «Повседневный», панель «Требования к заказу» свернётся.

У каждого тарифа содержимое панели разное.

Панель можно скроллить.

**Требования к заказу**

| Тариф | Состояние панели |Содержимое панели|Вид|Действие|
| --- | :-: |:-: |:-: |:-: |
| Повседневный | Закрыто |Зарядка для телефона|Чекбокс|Выбран/не выбран|
|  |   |Светомузыка Доступно в тарифе «Роскошный»|Кнопка/гиперссылка|Меняет тариф на «Роскошный»|
| Походный|  Раскрывается автоматически|-Спрей от комаров -Спальник|Счетчик|Ограничения на счётчик: спрей от 0 до 2 включительно; спальник от 0 до 5 включительно|
|  | |СветомузыкаДоступно в тарифе «Роскошный»|Кнопка/гиперссылка|Меняет тариф на «Роскошный»|
| Роскошный|Раскрывается автоматически|Светомузыка|Чекбокс|	Выбран/не выбран|
|  | |-Развлечься -Шампанское для пассажиров -Вино для пассажиров|Радиокнопка|Можно выбрать только 1 вариант|
|  | |Очки для крутоты|Счётчик|Ограничения на счётчик:от 0 до 3 включительно|

#### Кнопка «Забронировать»

Кнопка закреплена в левом нижнем углу экрана.

**Состояние кнопки**

| Заполненность полей|Текст|Действие|
| --- | :---: | :---: |
| Все обязательные поля и адреса заполнены | ЗабронироватьМаршрут составит .. км и займет .. мин |Появляется окно «Машина забронирована»|
| Все обязательные поля и адреса заполнены, кроме прав| Добавить права и забронироватьМаршрут составит .. км и займет .. мин |Появляется окно «Добавление прав»|
| Все обязательные поля и адреса заполнены, кроме способа оплаты |  Добавить оплату и забронироватьМаршрут составит .. км и займет .. мин |Появляется окно «Добавление карты»|
| Все обязательные поля заполнены, адреса удалены |Забронировать|Появляется окно «Машина забронирована»|
|Обязательные поля не заполнены и адреса удалены| Добавить права и забронировать|Появляется окно «Добавление прав»|

#### Бронь машины

Если пользователь корректно заполнил все поля и нажал кнопку «Забронировать», в центре экрана появится окно с заголовком «Машина забронирована». Внутри — марка, номер, иконка и адрес машины, а также стоимость поездки и таймер, который отсчитывает время бесплатного ожидания.

Если поля «Откуда» и «Куда» заполнены, отображается точная стоимость поездки. Если нет — стоимость за минуту.

 </details>

  <details> <summary> Задачи </summary> 

1. Подготовить чек-лист на верстку полей.
   Составить чек-лист на вёрстку следующих блоков:
- форма бронирования;
- элементы на навигационной карте: это иконки автомобилей и действия с ними.

2. Подготовить чек-лист и тест-кейсы на логику работы окон.
Составить следующую тестовую документацию: 

- чек-лист на логику окон «Способ оплаты» и «Добавление карты»,
- тест-кейсы на кнопку «Забронировать».

3. Протестировать приложение и завести баг-репорты в YouTrack.

   </details>

<details> <summary> Реализация </summary> 

#### Тестовая документация включающая в себя: Чек-листы, Тест-кейсы, Баг-репорты.

  [Проект 2 спринта](https://docs.google.com/document/d/1qyDCJE3-fBoWzS4bscsr6p0fnhl3QE_Cv2U8Dpf0QOg/edit)


 </details>
