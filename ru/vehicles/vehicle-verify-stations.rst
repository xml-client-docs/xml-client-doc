Верификации станций получения / возврата авто
#############################################

Описание XML схем верификации станций получения / возврата авто
===============================================================

XSD-схемы:

:download:`www/xsd/vehicle/VehicleVerifyStationsRequest.xsd <../../themes/hotelbook/static/xsd/vehicle/VehicleVerifyStationsRequest.xsd>`

:download:`www/xsd/vehicle/VehicleVerifyStationsResponse.xsd <../../themes/hotelbook/static/xsd/vehicle/VehicleVerifyStationsResponse.xsd>`

Запрос на верификацию станций получения / возврата, VehicleVerifyStationsRequest
--------------------------------------------------------------------------------

Запрос на верфикацию станций получения / возврата формируется по пути:
``/xml/vehicle_verify_stations``. И может проводиться только когда
известны id поискового запроса и результата поиска (для конкретного
авто).

В одном запросе можно указывать информацию только по одной паре станций
получения / возврата.

XML-схема запроса:

::

    <?xml version="1.0" encoding="utf-8"?>

    <VehicleVerifyStationsRequest>
      <SearchId>..</SearchId> - id поисковоо запроса 
      <ResultId>..</ResultId> - id результата поиска (для конкретного авто)
      <PickUp>        
          <Station>..</Station> - id станции получения авто
      </PickUp>
      <DropOff>        
          <Station>..</Station> - id станции возврата авто
      </DropOff>
    </VehicleVerifyStationsRequest>

Элемент VehicleVerifyStationsRequest
------------------------------------

Запрос на верификацию станций получения / возврата.

Сейчас в качестве рзультата на верификацию возвращается инфомация
непосредственно о верификации и дополнительная информация (напр.,
обслуживание отелей, станцией получения).

- Корневой элемент.
- Аттрибутов нет.

Дочерние элементы ``VehicleVerifyStationsRequest``:

+--------------+------------------+-------------------------------------------+--------------------------------------+
| **Элемент**  | **Обязательный** | **Описание**                              |                                      |
+==============+==================+===========================================+======================================+
| ``SearchId`` | да               | id поискового запроса                     |                                      |
+--------------+------------------+-------------------------------------------+--------------------------------------+
| ``ResultId`` | да               | id результата поиска для конкретного авто |                                      |
+--------------+------------------+-------------------------------------------+--------------------------------------+
| ``PickUp``   | да               | данные получения авто                     |                                      |
+--------------+------------------+-------------------------------------------+--------------------------------------+
| ``DropOff``  | да               | данные возврата авто                      |                                      |
+--------------+------------------+-------------------------------------------+--------------------------------------+
|              | **Элемент**      | **Обязательный**                          | **Описание**                         |
+--------------+------------------+-------------------------------------------+--------------------------------------+
|              | ``Station``      | да                                        | id станции получения / возврата авто |
+--------------+------------------+-------------------------------------------+--------------------------------------+

Элемент SearchId
----------------

В элементе указывается id поискового запроса.

- Обязательный элемент.
- Аттрибуты: нет.
- Дочерние элементы: нет.

Элемент ResultId
----------------

В элементе указывается id езультата поиска для конкретного авто.

- Обязательный элемент.
- Аттрибуты: нет.
- Дочерние элементы: нет.

Элемент PickUp
^^^^^^^^^^^^^^

В элементе указываются параметры получения авто (id станции получения).

- Обязательный элемент.
- Аттрибуты: нет.
- Дочерние элементы:

+---------------+--------------------+-----------------------------+
| **Элемент**   | **Обязательный**   | **Описание**                |
+---------------+--------------------+-----------------------------+
| ``Station``   | да                 | id станции получения авто   |
+---------------+--------------------+-----------------------------+

Элемент DropOff
^^^^^^^^^^^^^^^

В элементе указываются параметры возврата авто (id станции возврата).

- Обязательный элемент.
- Аттрибуты: нет.
- Дочерние элементы: те же, что и в элементе PickUp

Ответ на верификацию станций получения / возврата, VehicleVerifyStationsResponse
-------------------------------------------------------------------------------

XML-схема ответа:

::

    <?xml version="1.0" encoding="utf-8"?>
    <VehicleVerifyStationsResponse>
      <VehicleVerifyStationsRequest>... исходный запрос ...</VehicleVerifyStationsRequest>
      [<Errors>
        <Error code="..." description="..."> - ошибки
      </Errors>]
      <VehicleVerifyStations>        
          <Verify>true|false</Verify>          
              <AdditionalInfo>   
                    <Detail>      
                            <Title>..</Title>
                            <Value>..</Value>
                    </Detail>
              </AdditionalInfo>
      </VehicleVerifyStations>  
    </VehicleStationsInfoResponse>

Элемент VehicleVerifyStationsResponse
-------------------------------------

Ответ, сформированный сервером на получение информации о верификации
станций получения / возврата авто **VehicleVerifyStationsRequest**.

- Корневой элемент.
- Аттрибут: нет.
- Дочерние элементы ``VehicleVerifyStationsResponse``:

+----------------------------------+--------------------+-----------------------------------------+--------------------------------------------------+------------------------+---------------------------------------+
| **Элемент**                      | **Обязательный**   | **Описание**                            |                                                  |                        |                                       |
+==================================+====================+=========================================+==================================================+========================+=======================================+
| ``VehicleVerifyStationsRequest`` | нет                | Исходный запрос,                        |                                                  |                        |                                       |
|                                  |                    | см. выше – VehicleVerifyStationsRequest |                                                  |                        |                                       |
+----------------------------------+--------------------+-----------------------------------------+--------------------------------------------------+------------------------+---------------------------------------+
| ``Errors``                       | нет                | Список ошибок, если есть                |                                                  |                        |                                       |
+----------------------------------+--------------------+-----------------------------------------+--------------------------------------------------+------------------------+---------------------------------------+
|                                  | **Элемент**        | **Обязательный**                        | **Описание**                                     |                        |                                       |
+----------------------------------+--------------------+-----------------------------------------+--------------------------------------------------+------------------------+---------------------------------------+
|                                  | ``Error``          | да                                      | Описание ошибки (и код), ошибок может быть много |                        |                                       |
+----------------------------------+--------------------+-----------------------------------------+--------------------------------------------------+------------------------+---------------------------------------+
| ``VehicleVerifyStations``        | нет                | Данные о верификации станций            |                                                  |                        |                                       |
+----------------------------------+--------------------+-----------------------------------------+--------------------------------------------------+------------------------+---------------------------------------+
|                                  | **Элемент**        | **Обязательный**                        | **Описание**                                     |                        |                                       |
+----------------------------------+--------------------+-----------------------------------------+--------------------------------------------------+------------------------+---------------------------------------+
|                                  | ``Verify``         | да                                      | true false информация о верификации              |                        |                                       |
+----------------------------------+--------------------+-----------------------------------------+--------------------------------------------------+------------------------+---------------------------------------+
|                                  | ``AdditionalInfo`` | нет                                     | Доп. информация (напр., доступность опции:       |                        |                                       |
|                                  |                    |                                         | "Доставка в отель" на станции получения)         |                        |                                       |
+----------------------------------+--------------------+-----------------------------------------+--------------------------------------------------+------------------------+---------------------------------------+
|                                  |                    | **Элемент**                             | **Обязательный**                                 | **Описание**           |                                       |
+----------------------------------+--------------------+-----------------------------------------+--------------------------------------------------+------------------------+---------------------------------------+
|                                  |                    | ``Detail``                              | нет                                              | детали доп. информации |                                       |
+----------------------------------+--------------------+-----------------------------------------+--------------------------------------------------+------------------------+---------------------------------------+
|                                  |                    |                                         | **Элемент**                                      | **Обязательный**       | **Описание**                          |
+----------------------------------+--------------------+-----------------------------------------+--------------------------------------------------+------------------------+---------------------------------------+
|                                  |                    |                                         | ``Title``                                        | да                     | наименование элемента доп. информации |
+----------------------------------+--------------------+-----------------------------------------+--------------------------------------------------+------------------------+---------------------------------------+
|                                  |                    |                                         | ``Value``                                        | да                     | значение эл. доп. информации          |
+----------------------------------+--------------------+-----------------------------------------+--------------------------------------------------+------------------------+---------------------------------------+

Элемент VehicleVerifyStationsRequest
------------------------------------

Исходный XML-запрос, который передал пользователь.

- Необязательный элемент. (Отстутствует если в синтаксисе исходного XML были ошибки)
- Описание схемы элемента см. выше (``VehicleVerifyStationsRequest``)

Элемент Errors
--------------

Смотри страницу :doc:`Ошибки <../errors>`


Элемент VehicleVerifyStations
-----------------------------

Информация о верификации станци получения / возврата авто.

- Необязательный элемент. Отсутствует, если есть ошибки.
- Аттрибуты: нет.

Дочерние элементы:

+--------------------+------------------+-------------------------------------------------------------------------------------+--------------------------+
| **Элемент**        | **Обязательный** | **Описание**                                                                        |                          |
+====================+==================+=====================================================================================+==========================+
| ``Verify``         | да               | true,false                                                                          | информация о верификации |
+--------------------+------------------+-------------------------------------------------------------------------------------+--------------------------+
| ``AdditionalInfo`` | нет              | Доп. информация (напр., доступность опции: "Доставка в отель" на станции получения) |                          |
+--------------------+------------------+-------------------------------------------------------------------------------------+--------------------------+

Элемент Verify
--------------

Информация, непосредственно о верификации станций (true \| false).

- Обязательный элемент.
- Аттрибуты: нет.
- Дочерние элементы: нет

Элемент AdditionalInfo
----------------------

Дополнительная информация о станциях получения / возврата (сейчас
только, информация о доставки авто в отель).

- Необязательный элемент.
- Аттрибуты: нет.

Дочерние элементы:

+-------------+------------------+------------------------+---------------------------------------+
| **Элемент** | **Обязательный** | **Описание**           |                                       |
+=============+==================+========================+=======================================+
| ``Detail``  | нет              | детали доп. информации |                                       |
+-------------+------------------+------------------------+---------------------------------------+
|             | **Элемент**      | **Обязательный**       | **Описание**                          |
+-------------+------------------+------------------------+---------------------------------------+
|             | ``Title``        | да                     | наименование элемента доп. информации |
+-------------+------------------+------------------------+---------------------------------------+
|             | ``Value``        | да                     | значение эл. доп. информации          |
+-------------+------------------+------------------------+---------------------------------------+

