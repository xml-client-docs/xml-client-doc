Аннуляция Элемента Заказа
#########################

Описание XML схем аннуляции заказа
==================================

Запрос на аннуляцию элемента заказа сейчас формируется через URL (методом GET).

XSD-схема ответа с информацией о заказе:

:download:`www/xsd/order/CancellationOrderResponse.xsd <../../themes/hotelbook/static/xsd/order/CancellationOrderResponse.xsd>`

Запрос аннуляции заказа
-----------------------

В запросе нужно передать 2 параметра:

-  ``order_id`` – id заказа
-  ``item_id`` – id элемента заказа(трансфера), который будет аннулироваться

Оба параметра сейчас передаются через URL – вместе с учётными данными(``login``, ``password``, ``checksum``,..).
Запрос формируется по пути: ``/xml/cancellation_order``.

Если элемент заказа можно аннулировать – то он будет поставлен в очередь на аннуляцию (статус «Ожидает аннуляции»). *Это значит, что аннуляция не будет отправлена в работу!*
Для подтверждения аннуляции (отправки ее в работу) нужно выполнить ``/xml/confirm_order?order_id=...``, где ``order_id`` - номер аннулируемого заказа.

*Исключение:* после cancellation_order не нужно отправлять confirm_order, если заказ после создания не был подтвержден (не был отправлен в работу). Это можно проверить по статусу элемента заказа в ответе на первый запрос cancellation_order, там он сразу будет аннулирован.

Ответ на запрос об аннуляции элемента заказа, CancellationOrderResponse
-----------------------------------------------------------------------

| Формат ответа точно такой же, как и в ответа на запрос информации о заказе – ``OrderInfoResponse``.
| Для того, чтобы определить успешна ли постановка элемента заказа в очередь на аннуляцию – нужно проверить статус соответствующего элемента заказа.

В ответе могут прийти ошибки. См. страницу "Ошибки".