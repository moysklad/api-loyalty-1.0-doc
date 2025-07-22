## Внесение средств

Запрос на фискализацию внесения денежных средств в кассу

### Параметры запроса
+ **meta** `object` - Внешний уникальный идентификатор внесения в формате метаданных `Необходимое`
    + **href** `string` - Ссылка на внесение `Необходимое`
    + **id** `string` - Идентификатор внесения `Необходимое`
+ **retailShift** `object` - Данные о смене `Необходимое`
    + **meta** `object` `Необходимое`
        + **href** `string` - Ссылка на смену `Необходимое`
        + **id** `string` - Идентификатор смены `Необходимое`
+ **retailStore** `object` - Данные о точке продаж, на которой была совершена операция внесения `Необходимое`
    + **meta** `object` `Необходимое`
        + **href** `string` - Ссылка на точку продаж `Необходимое`
        + **id** `string` - Идентификатор точки продаж `Необходимое`
+ **name** `string` - Номер внесения `Необходимое`
+ **moment** `date` - Дата внесения денег в формате ГГГГ-ММ-ДД ЧЧ:ММ:СС `Необходимое`
+ **cashier** `object` `Необходимое` - Данные кассира
    + **meta** `object` `Необходимое`
        + **href** `string` - Ссылка на кассира `Необходимое`
        + **id** `string` - Идентификатор кассира `Необходимое`
    + **firstName** - Имя
    + **middleName** - Фамилия
    + **lastName** - Отчество
+ **sum** `string` - Сумма внесения денег, умноженная на 100 `Необходимое`


> **`POST`**
> /1/retaildrawercashin

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
    "href": "https://api.moysklad.ru/api/remap/1.2/entity/retaildrawercashin/675b943f-a25b-433c-90e0-5c84c7b0c307",
    "id": "675b943f-a25b-433c-90e0-5c84c7b0c307"
  },
  "retailShift": {
    "meta": {
      "href": "https://api.moysklad.ru/api/remap/1.2/entity/retailshift/2b5eb22f-139e-11e6-9464-e4de00000073",
      "id": "2b5eb22f-139e-11e6-9464-e4de00000073"
    }
  },
  "cashier": {
    "meta": {
      "href": "https://online.moysklad.ru/api/remap/1.2/entity/employee/a4f36276-7b5a-11e6-8a84-bae500000004",
      "id": "a4f36276-7b5a-11e6-8a84-bae500000004"
    },
    "firstName": "Иван",
    "middleName": "Иванович",
    "lastName": "Иванов"
  },
  "name": "0001",
  "retailstore": {
    "meta": {
      "href": "https://api.moysklad.ru/api/remap/1.2/entity/retilstore/e827ea09-1447-41b6-8118-13cf438e9145",
      "id": "e827ea09-1447-41b6-8118-13cf438e9145"
    }
  },
  "moment": "2024-11-18 21:41:46",
  "sum": "340"
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
| time            | `date` Момент фискализации внесения средств в формате ГГГГ-ММ-ДД ЧЧ:ММ:СС `2024-10-14 14:48:33` |

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
