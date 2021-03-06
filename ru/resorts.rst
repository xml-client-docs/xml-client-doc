Список регионов (курортов)
##########################

Описание XML схемы получения списка курортов
============================================

Запрос на получение списка курортов формируется через URL (методом GET)

XSD-схема ответа: :download:`www/xsd/dict/geo/ResortsResponse.xsd <../themes/hotelbook/static/xsd/dict/geo/ResortsResponse.xsd>`

Запрос списка курортов
----------------------

В запросе можно передать параметр ``country_id`` (идентификатор страны,
курорты которой нужно вернуть). Сейчас запрос передаётся через URL
вместе с учётными данными (``login``, ``password``, ``checksum``,..).

Запрос формируется по пути: ``/xml/resorts``

Ответ на запрос списка курортов, ResortsResponse
------------------------------------------------

::

    <?xml version="1.0" encoding="utf-8"?>
    <Response>
        <Resorts>
            <Resort id="..." country="...">...</Resort> - список всех найденных курортов
        </Resorts>

    </Response>

Элемент Response
----------------

Корневой элемент.

**Атрибуты:** нет.

**Дочерний элемент:**

+-----------+----------------+-------------------+
| Имя       | Обязательный   | Описание          |
+===========+================+===================+
| Resorts   | Да             | Список курортов   |
+-----------+----------------+-------------------+

Элемент Resorts
---------------

Содержит список всех найденных курортов.

**Атрибуты:** нет.

**Дочерний элемент:**

+--------+--------------+----------------------------------------------------------+
| Имя    | Обязательный | Описание                                                 |
+========+==============+==========================================================+
| Resort | Нет          | Название курорта                                         |
+--------+--------------+----------------------------------------------------------+

Элемент Resort
---------------
Название курорта

**Атрибуты:**
+------------+-----------+----------------------+--------------------------------+
| Имя        | Тип		 |  Обязательный        | Описание                       |
+============+===========+======================+================================+
| id         | Число     |  Да                  | Идентификатор                  |
+------------+-----------+----------------------+--------------------------------+
| country    | Число     |  Да                  | ID страны,где находится курорт |
+------------+-----------+----------------------+--------------------------------+