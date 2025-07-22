## Возврат

Запрос на фискализацию возврата продажи
В составе запроса может быть указана ссылка на документ продажи.

### Параметры запроса
+ **meta** `object` - Внешний уникальный идентификатор возврата продажи в формате метаданных `Необходимое`
    + **href** `string` - Ссылка на возврат продажи `Необходимое`
    + **id** `string` - Идентификатор возврата продажи `Необходимое`
+ **name** `string` - Номер возврата продажи `Необходимое`
+ **retailStore** `object` - Данные о точке продаж, на которой была совершена операция возврата продажи `Необходимое`
    + **meta** `object` `Необходимое`
        + **href** `string` - Ссылка на точку продаж `Необходимое`
        + **id** `string` - Идентификатор точки продаж `Необходимое`
+ **retailShift** `object` - Данные о смене `Необходимое`
    + **meta** `object` `Необходимое`
        + **href** `string` - Ссылка на смену `Необходимое`
        + **id** `string` - Идентификатор смены `Необходимое`
+ **moment** `date` - Дата возврата продажи в формате ГГГГ-ММ-ДД ЧЧ:ММ:СС `Необходимое`
+ **demand** `object` - Данные розничной продажи для возврата
    + **meta** `object` `Необходимое`
        + **href** `string` - Ссылка на продажу `Необходимое`
        + **id** `string` - Идентификатор продажи `Необходимое`
+ **payments** `object` - Информация о платежах `Необходимое`
    + **cashSum** `string` - Сумма оплаты наличными
    + **cardSum** `string` - Сумма оплаты картой
    + **qrSum** `string` - Сумма оплаты QR-кодом
+ **phone** `string` Номер телефона для отправки электронного чека
+ **email** `string` Адрес электронной почты для отправки электронного чека
+ **positions** `array` - Массив позиций документа
    + **assortment** `object` - Реквизиты позиции в формате метаданных`Необходимое`
        + **meta** `object` `Необходимое`
            + **href** `string` - Идентификатор товара/услуги `Необходимое`
            + **id** `string` - Идентификатор товара/услуги `Необходимое`
        + **name** `string` - Название товара `Необходимое`
        + **uom** `object` - Единица измерения
            + **name** `string` - Название единицы измерения `Необходимое`
            + **code** `string` - Код единицы измерения
        + **quantity** `number` - Количество товара в позиции `Необходимое`
        + **price** `string` - Цена товара `Необходимое`
        + **discount** `string` - Процент скидки
        + **pack** `object` - Упаковка товара
            + **name** `string` - Название `Необходимое`
            + **quantity** `number` Количество товара в упаковке - `Необходимое`
        + **vat** `number` - Ставка НДС
        + **vatEnabled** `boolean` - Включён ли НДС для позиции
        + **marks** `array` - Массив кодов маркировки
            + **cis** `string` - Код маркировки
+ **vatEnabled** `boolean` - Флаг, указывающий, что документ содержит НДС
+ **vatIncluded** `boolean` - Флаг, указывающий, включён ли НДС в цену
+ **customerOrder** `object` - Заказ покупателя в МС

> **`POST`**
> /1/retaisalesreturn

> **Request**

> Headers

```
Content-Type:application/json
X-Lognex-Galya-Signature: подпись
X-Lognex-Galya-Account-Id: идентификатор аккаунт-решение
```

> Body

```json
{
  "meta": {
    "href": "https://api.moysklad.ru/api/remap/1.0/entity/sale/saleId",
    "id": "saleId"
  },
  "name": "12345",
  "retailstore": {
    "meta": {
      "href": "https://api.moysklad.ru/api/remap/1.0/entity/retailstore/retailStoreId",
      "id": "retailStoreId"
    }
  },
  "retailShift": {
    "meta": {
      "href": "https://api.moysklad.ru/api/remap/1.2/entity/retailshift/2b5eb22f-139e-11e6-9464-e4de00000073",
      "id": "2b5eb22f-139e-11e6-9464-e4de00000073"
    }
  },
  "moment": "2024-11-20 14:30:00",
  "demand": {
    "meta": {
      "href": "https://api.moysklad.ru/api/remap/1.0/entity/retaildemand/retaildemandid/",
      "id": "e21d80cb-8344-43c6-8c47-bedf0b7b5822"
    }
  },
  "payments": {
    "cashSum": "1000",
    "cardSum": "500"
  },
  "phone": "+79051234567",
  "email": "example@example.com",
  "positions": [
    {
      "assortment": {
        "meta": {
          "href": "https://api.moysklad.ru/api/remap/1.0/entity/product/productId",
          "id": "productId"
        },
        "name": "Товар 1"
      },
      "uom": {
        "name": "шт",
        "code": "unit1"
      },
      "quantity": 2.0,
      "price": "500",
      "discount": "10",
      "pack": null,
      "vat": 18.0,
      "vatEnabled": true,
      "marks": ["markCode1", "markCode2"]
    }
  ],
  "vatEnabled": true,
  "vatIncluded": true,
  "customerOrder": {
    "meta": {
      "href": "https://api.moysklad.ru/api/remap/1.0/entity/customerorder/orderId",
      "id": "orderId"
    }
  }
}
```

### Параметры ответа
| Параметр        | Описание                                                                                        |
|-----------------|-------------------------------------------------------------------------------------------------|
| fnNumber        | `string` Номер ФН                                                                               |
| kktRegNumber    | `string` Регистрационный номер                                                                  |
| fiscalDocNumber | `string` Номер фискального документа                                                            |
| fiscalDocSign   | `string` Фискальный признак документа                                                           |
| receipt         | `string` Чек в формате base64                                                                   |
| time            | `date` Момент фискализации возврата продажи в формате ГГГГ-ММ-ДД ЧЧ:ММ:СС `2024-10-14 14:48:33` |

> **Response**   
> 200 (application/json)

> Headers

```
Content-Type:application/json
```

> Body

```json
{
    "fnNumber": "1234",
    "kktRegNumber": "5678",
    "fiscalDocSign": "9012",
    "fiscalDocNumber": "7890",
    "time": "2024-11-18 21:41:46"
}
```
