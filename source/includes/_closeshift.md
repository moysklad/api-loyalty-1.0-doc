## Закрытие смены

Запрос на фискализацию закрытия смены

### Параметры запроса
+ **retailShift** `object` - данные о смене `Необходимое`
  + **meta** `object` `Необходимое`
    + **href** `string` - Ссылка на смену `Необходимое`
    + **id** `string` - Идентификатор смены `Необходимое`
+ **name** `string` - номер смены `Необходимое`
+ **retailStore** `object` `Необходимое` - данные о точке продаж, на которой была открыта смена
  + **meta** `object` `Необходимое`
    + **href** `string` - Ссылка на точку продаж `Необходимое`
    + **id** `string` - Идентификатор точки продаж `Необходимое`
+ **cashier** `object` `Необходимое` - данные кассира
  + **meta** `object` `Необходимое`
    + **href** `string` - Ссылка на кассира `Необходимое`
    + **id** `string` - Идентификатор кассира `Необходимое`
  + **firstName** - Имя
  + **middleName** - Фамилия
  + **lastName** - Отчество
+ **closeMoment** `date` - дата закрытия смены в формате ГГГГ-ММ-ДД ЧЧ:ММ:СС `Необходимое`


> **`PUT`**
> /1/closeshift

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
  "retailShift": {
    "meta": {
      "href": "https://api.moysklad.ru/api/remap/1.2/entity/retailshift/2b5eb22f-139e-11e6-9464-e4de00000073",
      "id": "2b5eb22f-139e-11e6-9464-e4de00000073"
    }
  },
  "name": "0001",
  "retailstore": {
    "meta": {
      "href": "https://api.moysklad.ru/api/remap/1.2/entity/retailstore/e827ea09-1447-41b6-8118-13cf438e9145",
      "id": "e827ea09-1447-41b6-8118-13cf438e9145"
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
  "closeMoment": "2024-11-18 21:41:46"
}
```

### Параметры ответа
| Параметр        | Описание                                                                             |
|-----------------|--------------------------------------------------------------------------------------|
| fnNumber        | `string` Номер ФН                                                                    |
| kktRegNumber    | `string` Регистрационный номер                                                       |
| fiscalDocNumber | `string` Номер фискального документа                                                 |
| fiscalDocSign   | `string` Фискальный признак документа                                                |
| receipt         | `string` Чек в формате base64                                                        |
| shiftNumber     | `string` Номер смены                                                                 |
| time            | `date` Момент фискализации смены в формате ГГГГ-ММ-ДД ЧЧ:ММ:СС `2024-10-14 14:48:33` |
| chequesTotal    | `integer` количество чеков за смену                                                  |
| fiscalDocsTotal | `integer` количество фискальных документов за смену                                  |

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
  "shiftNumber": "3456",
  "fiscalDocNumber": "7890",
  "time": "2024-11-18 21:41:46",
  "chequesTotal": 10,
  "fiscalDocsTotal": 8
}
```
