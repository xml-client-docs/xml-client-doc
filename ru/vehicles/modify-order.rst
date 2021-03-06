Изменения заказа
################

Описание XML-схемы
==================

XSD-схема:

:download:`www/xsd/order/ModifyOrderRequest.xsd <../../themes/hotelbook/static/xsd/order/ModifyOrderRequest.xsd>`

:download:`www/xsd/order/ModifyOrderResponse.xsd <../../themes/hotelbook/static/xsd/order/ModifyOrderResponse.xsd>`

После того, как заказ создан, Вы можете модифицировать один или
несколькоавто в созданном заказе. Для изменения заказа укажите id заказа
и список егоэлементов (с id элементов), которые Вы желаете изменить. Вы
можете указать параметры мест получени и возврата авто, информацию о
водителе, дополнительные опции, а также информацию для ваучера.Все
идентификаторы (id заказа, элементов) можно получить в OrderInfoResponse
Обратите внимание, что конкретное авто может запрещать изменения. На это
указывает параметрEditable для авто в OrderInfoResponse.

Запрос
------

XML-схема:

::

    <?xml version="1.0" encoding="utf-8"?>
    <ModifyOrderRequest>
      [<ContactInfo> - contact information
        <Name>..</Name> - имя
        <Email>..</Email> - email
        <Phone>..</Phone> - телефон
        <Comment>..</Comment> - комментарий
      </ContactInfo>]
      <OrderId>..</OrderId> - id заказа
      [<AccountComment>..</AccountComment>] - Комментарий для счета
      [<Partner>  - Контрагент
        [<PartnerId>...</PartnerId>] - номер контрагента
        [<PartnerBase>...</PartnerBase>] - номер базы контрагента
        [<PartnerName>...</PartnerName>] - имя клиента
      </Partner>] 
      [<PayForm>cash|cashless</PayForm>] - форма оплаты заказа (необязательно)
      <Items> - элементы заказа
        <VehicleItem> - авто
            <PickUp>
              <PickUpStation>..</PickUpStation> - id станции получения авто
              <PickUpFlightNum>..</PickUpFlightNum> - номер рейса самолёта (если станция поддерживает обслуживание аэропорта)
              <PickUpHotel [hotelId=".."]>
                <HotelInfo [hotelName=".."]
                   [hotelAddress=".."]/>
              </PickUpHotel> 
            </PickUp>
            <DropOff>
              <DropOffStation>..</DropOffStation> - id станции возврата авто
            </DropOff>
            <Driver>
              <Title>Mr|Mrs|Ms|Chld</Title> - обращение
              <FirstName>..</FirstName> - имя (латинские)
              <LastName>..</LastName> - фамилия (латинские)
              <BirthDate>..</BirthDate> - дата рождения (YY-mm-dd)
            </Driver>
            <Extras>    
               <Extra>..</Extra> - id дополнительных опций
            </Extras>
            <VoucherInfo>..</VoucherInfo> - информация для ваучера
        </VehicleItem>
      </Items>
    </ModifyOrderRequest>

Элемент ModifyOrderRequest
--------------------------

Родительский элемент.

- Атрибуты: нет.

Дочерние элементы:

+--------------------+------------------+-------------------------+--------------------------------------------+---------------------------------------------------+
| **Элемент**        | **Обязательный** | **Описание**            |                                            |                                                   |
+====================+==================+=========================+============================================+===================================================+
| ``ContactInfo``    | нет              | контактная информация   |                                            |                                                   |
+--------------------+------------------+-------------------------+--------------------------------------------+---------------------------------------------------+
|                    | **Элемент**      | **Обязательный**        | **Описание**                               |                                                   |
+--------------------+------------------+-------------------------+--------------------------------------------+---------------------------------------------------+
|                    | ``Name``         | да                      | полное имя                                 |                                                   |
+--------------------+------------------+-------------------------+--------------------------------------------+---------------------------------------------------+
|                    | ``Email``        | да                      | электронная почта                          |                                                   |
+--------------------+------------------+-------------------------+--------------------------------------------+---------------------------------------------------+
|                    | ``Phone``        | да                      | телефон                                    |                                                   |
+--------------------+------------------+-------------------------+--------------------------------------------+---------------------------------------------------+
|                    | ``Comment``      | да                      | комментарий (может быть пустым)            |                                                   |
+--------------------+------------------+-------------------------+--------------------------------------------+---------------------------------------------------+
| ``OrderId``        | да               | id существующего заказа |                                            |                                                   |
+--------------------+------------------+-------------------------+--------------------------------------------+---------------------------------------------------+
| ``AccountComment`` | нет              | Комментарий для счета   |                                            |                                                   |
+--------------------+------------------+-------------------------+--------------------------------------------+---------------------------------------------------+
| ``Partner``        | нет              | Контрагент из ЮТС24     |                                            |                                                   |
+--------------------+------------------+-------------------------+--------------------------------------------+---------------------------------------------------+
|                    | **Элемент**      | **Обязательный**        | **Описание**                               |                                                   |
+--------------------+------------------+-------------------------+--------------------------------------------+---------------------------------------------------+
|                    | ``PartnerId``    | нет                     | Номер контрагента                          |                                                   |
+--------------------+------------------+-------------------------+--------------------------------------------+---------------------------------------------------+
|                    | ``PartnerBase``  | нет                     | Номер базы                                 |                                                   |
+--------------------+------------------+-------------------------+--------------------------------------------+---------------------------------------------------+
|                    | ``PartnerName``  | нет                     | Имя клиента                                |                                                   |
+--------------------+------------------+-------------------------+--------------------------------------------+---------------------------------------------------+
| ``PayForm``        | нет              | Форма оплаты заказа     |                                            |                                                   |
+--------------------+------------------+-------------------------+--------------------------------------------+---------------------------------------------------+
| ``Items``          | да               | Элементы заказа         |                                            |                                                   |
+--------------------+------------------+-------------------------+--------------------------------------------+---------------------------------------------------+
|                    | **Элемент**      | **Обязательный**        | **Описание**                               |                                                   |
+--------------------+------------------+-------------------------+--------------------------------------------+---------------------------------------------------+
|                    | ``VehicleItem``  | да                      | Элемент заказа (может быть много в заказе) |                                                   |
+--------------------+------------------+-------------------------+--------------------------------------------+---------------------------------------------------+
|                    |                  | **Элемент**             | **Обязательный**                           | **Описание**                                      |
+--------------------+------------------+-------------------------+--------------------------------------------+---------------------------------------------------+
|                    |                  | ``ItemId``              | да                                         | Идентификатор элемента заказа                     |
+--------------------+------------------+-------------------------+--------------------------------------------+---------------------------------------------------+
|                    |                  | ``PickUp``              | да                                         | Параметры места получения                         |
+--------------------+------------------+-------------------------+--------------------------------------------+---------------------------------------------------+
|                    |                  | ``DropOff``             | да                                         | Параметры места возврата                          |
+--------------------+------------------+-------------------------+--------------------------------------------+---------------------------------------------------+
|                    |                  | ``Driver``              | да                                         | Водитель (обращение, имя, фамилия, дата рождения) |
+--------------------+------------------+-------------------------+--------------------------------------------+---------------------------------------------------+
|                    |                  | ``Extras``              | нет                                        | Список выбранных дополнительных опций             |
+--------------------+------------------+-------------------------+--------------------------------------------+---------------------------------------------------+
|                    |                  | ``VoucherInfo``         | нет                                        | Информация для ваучера                            |
+--------------------+------------------+-------------------------+--------------------------------------------+---------------------------------------------------+

Элемент ContactInfo
-------------------

- Атрибуты: нет.

Дочерние элементы:

+-------------+------------------+----------------------------------------------------+
| **Элемент** | **Обязательный** | **Описание**                                       |
+=============+==================+====================================================+
| ``Name``    | да               | Полное имя пользователя (максимально 100 символов) |
+-------------+------------------+----------------------------------------------------+
| ``Email``   | да               | электронный адрес (максимально 100 символов)       |
+-------------+------------------+----------------------------------------------------+
| ``Phone``   | да               | телефон (максимально 15 символов)                  |
+-------------+------------------+----------------------------------------------------+
| ``Comment`` | да               | комментарий (может быть пустым)                    |
+-------------+------------------+----------------------------------------------------+

Элемент Partner
---------------
Контрагент из ЮТС24
- *Необязательный элемент*
- *Аттрибутов нет.*

Дочерние элементы ``Partner``:

+-----------------+------------------+-------------------------------------------------+---------------------+
| **Элемент**     | **Обязательный** | **Описание**                                    | **Тип**             |
+=================+==================+=================================================+=====================+
| ``PartnerId``   | нет              | Номер контрагента.                              | Строка (8 символов) |
+-----------------+------------------+-------------------------------------------------+---------------------+
| ``PartnerBase`` | нет              | Номер базы контрагента.                         | Число               |
+-----------------+------------------+-------------------------------------------------+---------------------+
| ``PartnerName`` | нет              | Имя клиента                                     | Имя клиента         |
+-----------------+------------------+-------------------------------------------------+---------------------+

Элемент Items
-------------

- Элементы заказа.
- Обязательный элемент.
- Атрибуты: нет.

Дочерние элементы:

+-----------------+------------------+--------------------------------------------+--------------------------------------------------------+
| **Элемент**     | **Обязательный** | **Описание**                               |                                                        |
+=================+==================+============================================+========================================================+
| ``VehicleItem`` | да               | Элемент заказа (может быть много в заказе) |                                                        |
+-----------------+------------------+--------------------------------------------+--------------------------------------------------------+
|                 | **Элемент**      | **Обязательный**                           | **Описание**                                           |
+-----------------+------------------+--------------------------------------------+--------------------------------------------------------+
|                 | ``ItemId``       | да                                         | Идентификатор элемента заказа                          |
+-----------------+------------------+--------------------------------------------+--------------------------------------------------------+
|                 | ``PickUp``       | да                                         | Параметры места получения                              |
+-----------------+------------------+--------------------------------------------+--------------------------------------------------------+
|                 | ``DropOff``      | да                                         | Параметры места возврата                               |
+-----------------+------------------+--------------------------------------------+--------------------------------------------------------+
|                 | ``Driver``       | да                                         | Водитель авто (обращение, имя, фамилия, дата рождения) |
+-----------------+------------------+--------------------------------------------+--------------------------------------------------------+
|                 | ``Extras``       | нет                                        | Выбранные дополнительные опции                         |
+-----------------+------------------+--------------------------------------------+--------------------------------------------------------+
|                 | ``VoucherInfo``  | нет                                        | Информация для ваучера                                 |
+-----------------+------------------+--------------------------------------------+--------------------------------------------------------+

Элемент VehicleItem
^^^^^^^^^^^^^^^^^^^

Элемент заказа - авто.

- Обязательный элемент.
- Атрибуты: нет.

Дочерние элементы:

+-----------------+------------------+--------------------------------------------------------+
| **Элемент**     | **Обязательный** | **Описание**                                           |
+=================+==================+========================================================+
| ``ItemId``      | да               | Идентификатор элемента заказа                          |
+-----------------+------------------+--------------------------------------------------------+
| ``PickUp``      | да               | Параметры места получения                              |
+-----------------+------------------+--------------------------------------------------------+
| ``DropOff``     | да               | Параметры места возврата                               |
+-----------------+------------------+--------------------------------------------------------+
| ``Driver``      | да               | Водитель авто (обращение, имя, фамилия, дата рождения) |
+-----------------+------------------+--------------------------------------------------------+
| ``Extras``      | нет              | Выбранные дополнительный опции                         |
+-----------------+------------------+--------------------------------------------------------+
| ``VoucherInfo`` | нет              | Информация для ваучера                                 |
+-----------------+------------------+--------------------------------------------------------+

Элемент PickUp
''''''''''''''

Параметры места получения авто.
- Обязательный элемент.
- Аттрибутов элемента нет.

Дочерние элементы:

+---------------------+---------------------------------------------------------------+------------------+------------------------------------------------------------------------------+
| **Элемент**         | **Тип**                                                       | **Обязательный** | **Описание**                                                                 |
+=====================+===============================================================+==================+==============================================================================+
| ``PickUpStation``   | число                                                         | да               | id станции получения                                                         |
+---------------------+---------------------------------------------------------------+------------------+------------------------------------------------------------------------------+
| ``PickUpFlightNum`` | строка                                                        | да               | номер рейса (если станция обслуживает аэропорты)                             |
+---------------------+---------------------------------------------------------------+------------------+------------------------------------------------------------------------------+
| ``PickUpHotel``     | Элемент, содержащий id или же название и адрес отеля доставки | нет              | информация об отеле доставки авто, если данная опция поддерживается станцией |
+---------------------+---------------------------------------------------------------+------------------+------------------------------------------------------------------------------+

Элемент PickUpHotel
'''''''''''''''''''

Параметры отеля доставки (если данная опция поддерживается станцией получения авто).

- Необязательный элемент.

Аттрибуты элемента ``PickUpHotel``:

+--------------+---------+------------------+------------------------+
| **Аттрибут** | **Тип** | **Обязательный** | **Описание**           |
+==============+=========+==================+========================+
| ``hotelId``  | число   | да               | id отеля доставки авто |
+--------------+---------+------------------+------------------------+

Дочерние элементы:

+---------------+--------------------------------------------------------------------+------------------+------------------------------------------------------------------------------+
| **Элемент**   | **Тип**                                                            | **Обязательный** | **Описание**                                                                 |
+===============+====================================================================+==================+==============================================================================+
| ``HotelInfo`` | Элемент, содержащий, как атрибуты, название и адрес отеля доставки | нет              | информация об отеле доставки авто, если данная опция поддерживается станцией |
+---------------+--------------------------------------------------------------------+------------------+------------------------------------------------------------------------------+

Элемент HotelInfo
'''''''''''''''''

Параметры отеля доставки (если данная опция поддерживается станцией получения авто).
- Необязательный элемент.
- Дочерних элементов нет.

Аттрибуты элемента ``HotelInfo``:

+------------------+---------+------------------+------------------------------+
| **Аттрибут**     | **Тип** | **Обязательный** | **Описание**                 |
+==================+=========+==================+==============================+
| ``hotelName``    | строка  | да               | Название отеля доставки авто |
+------------------+---------+------------------+------------------------------+
| ``hotelAddress`` | строка  | да               | Адрес отеля доставки авто    |
+------------------+---------+------------------+------------------------------+

Элемент DropOff
'''''''''''''''

Параметры места возврата авто.

- Обязательный элемент.
- Аттрибутов элемента нет.

Дочерние элементы:

+--------------------+---------+------------------+---------------------+
| **Элемент**        | **Тип** | **Обязательный** | **Описание**        |
+====================+=========+==================+=====================+
| ``DropOffStation`` | число   | да               | id станции возврата |
+--------------------+---------+------------------+---------------------+

Элемент Driver
''''''''''''''

Водитель авто.

- Обязательный элемент.
- Аттрибутов элемента нет.

Дочерние элементы:

+---------------+----------------+------------------+---------------------------------------+
| **Элемент**   | **Тип**        | **Обязательный** | **Описание**                          |
+===============+================+==================+=======================================+
| ``Title``     | Mr,Ms,Mrs,Chld | да               | обращение                             |
+---------------+----------------+------------------+---------------------------------------+
| ``FirstName`` | строка         | да               | имя водителя (латинскими буквами)     |
+---------------+----------------+------------------+---------------------------------------+
| ``LastName``  | строка         | да               | фамилия водителя (латинскими буквами) |
+---------------+----------------+------------------+---------------------------------------+
| ``BirthDate`` | строка         | да               | дата рождения водителя (YY-mm-dd)     |
+---------------+----------------+------------------+---------------------------------------+

Элемент Extras
''''''''''''''

Список выбранных дополнительных опций.

- Необязательный элемент.
- Аттрибутов элемента нет.

Дочерние элементы:

+-------------+-----------------------------------------------------------+------------------+--------------+
| **Элемент** | **Тип**                                                   | **Обязательный** | **Описание** |
+=============+===========================================================+==================+==============+
| ``Extra``   | id дополнительной опции, таких элементов может быть много | да               |              |
+-------------+-----------------------------------------------------------+------------------+--------------+

Элемент VoucherInfo
'''''''''''''''''''

Информация для ваучера.

- Необязательный элемент.
- Аттрибутов элемента нет.
- Дочерних элементов нет

Ответ, ModifyOrderResponse
--------------------------

Шаблон ответа такой же, как ответ на запрос информации о заказе (``OrderInfoResponse``).