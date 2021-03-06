Список отелей
#############

Описание XML схемы получения списка отелей
==========================================

Запрос на получение списка отелей формируется через URL (методом GET)

XSD-схема ответа :

- :download:`www/xsd/dict/hotel/HotelListResponse.xsd <../../themes/hotelbook/static/xsd/dict/hotel/HotelListResponse.xsd>`

Запрос списка отелей
--------------------

Запрос передаётся через URL вместе с учётными данными (``login``, ``password``, ``checksum``,..). Запросом можно также передать параметры:

-  ``?country_id=id_страны``, чтобы получить список отелей только одной страны;
-  ``?city_id=id_города``, чтобы получить список отелей только одного города;
-  ``?update=дата_в_формате_"Y-m-d H:i:s"`` для получения отелей, данные по которым обновлялись после указанной даты.

В запросе ОБЯЗАТЕЛЬНО должен быть один из параметров ``country_id`` или ``city_id``

Запрос формируется по пути: ``/xml/hotel_list``

Ответ на запрос списка отелей, HotelListResponse
------------------------------------------------

::

    <?xml version="1.0" encoding="utf-8"?> 
    <Response>
        <HotelList>
            <Hotel name="..." id="..." city="..." cat="..." updated="..." date_create="..." assoc="0|1" utsluxury="0|1" hotelLatitude="..." hotelLongitude="..."> - список всех найденных отелей
        </HotelList>
        [<Errors>
        	<Error [type="..."] [code="..."] description="..."> - ошибки
      	</Errors>]
    </Response>

Элемент Response
----------------

Корневой элемент.

**Атрибуты:** нет.

**Дочерний элемент:**

+-----------+--------------+---------------+
| Имя       | Обязательный | Описание      |
+===========+==============+===============+
| HotelList | Да           | Список отелей |
+-----------+--------------+---------------+
| Errors    | Нет          | Ошибки        |
+-----------+--------------+---------------+

Элемент HotelList
-----------------

Содержит список всех найденных локаций.

**Атрибуты:** нет.

**Дочерний элемент:**

+-------+--------------+-----------------+
| Имя   | Обязательный | Описание        |
+=======+==============+=================+
| Hotel | Нет          | Найденный отель |
+-------+--------------+-----------------+

Элемент Hotel
-------------

Необязательный элемент (отсутствует, если ни одного отеля не найдено).

**Атрибуты:**

+----------------+------------------------------------------------+--------------+-------------------------------------------------------------------------------------+
| Имя            | Тип                                            | Обязательный | Описание                                                                            |
+================+================================================+==============+=====================================================================================+
| name           | Строка                                         | Да           | Название найденного отеля                                                           |
+----------------+------------------------------------------------+--------------+-------------------------------------------------------------------------------------+
| id             | Число                                          | Да           | id найденного отеля                                                                 |
+----------------+------------------------------------------------+--------------+-------------------------------------------------------------------------------------+
| city           | Число                                          | Да           | id города, в котором находится отель                                                |
+----------------+------------------------------------------------+--------------+-------------------------------------------------------------------------------------+
| сat            | Число от 1 до 5                                | Да           | id категория звездности найденного отеля (из ответа на запрос from /xml/hotel\_cat) |
+----------------+------------------------------------------------+--------------+-------------------------------------------------------------------------------------+
| updated        | Unix-дата (число секунд)                       | Да           | Дата последнего обновления информации об отеле                                      |
+----------------+------------------------------------------------+--------------+-------------------------------------------------------------------------------------+
| date_create    | Unix-дата (число секунд)                       | Да           | Дата создания записи об отеле в таблице                                             |
+----------------+------------------------------------------------+--------------+-------------------------------------------------------------------------------------+
| modifying type | 'add' или 'delete' или 'change' или 'undelete' | Да           | Характер последнего изменения                                                       |
+----------------+------------------------------------------------+--------------+-------------------------------------------------------------------------------------+
| assoc          | 0 или 1                                        | Да           | Асоциирован ли отель хотя бы с одним из поставщиков                                 |
+----------------+------------------------------------------------+--------------+-------------------------------------------------------------------------------------+
| utsluxury      | 0 или 1                                        | Да           | Категория (признак) для отеля                                                       |
+----------------+------------------------------------------------+--------------+-------------------------------------------------------------------------------------+
| hotelLatitude  | Строка                                         | Да           | Широта                                                                              |
+----------------+------------------------------------------------+--------------+-------------------------------------------------------------------------------------+
| hotelLongitude | Строка                                         | Да           | Долгота                                                                             |
+----------------+------------------------------------------------+--------------+-------------------------------------------------------------------------------------+

**Дочерние элементы:** нет.


Элемент Errors
---------------
Смотри страницу :doc:`Ошибки <../errors>`