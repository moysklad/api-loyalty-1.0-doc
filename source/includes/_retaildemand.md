## Продажа 

### Расчет скидок для продажи 

Запрос на пересчет скидок для операции продажи. В запросе передается продажа без применения скидок. В ответе ожидается продажа со всеми примененными скидками. В случае округления суммы чека, допускается разбиение одной позии на две.

Если проишло разбиение позиции, то необходимо учитывать значение в поле sn (серийные номера). Правило следующее - количество серийных номеров изначальной позиции совпадает с количеством серийных номеров в позициях, получившихся в результате разбиения. Так же, количество серийных номеров должно быть равно количеству товара (поле quantity).

После расчета скидок, приложение уже никак не меняет состав чека и не применяет другие скидки.
     
#### Атрибуты сущности  
+ **retailStore** `object` `Необходимое`
    + **meta** `object` `Необходимое`
        + **href** `string` - Идентификатор точки продаж `Необходимое`
        + **id** `string` - Идентификатор точки продаж `Необходимое`
    + **name** `string` - Название точки продаж
+ **agent** `object` - Реквизиты покупателя в формате метаданных`Необходимое`
    + **meta** `object` `Необходимое`
        + **href** `string` - Идентификатор покупателя`Необходимое`
        + **id** `string` - Идентификатор покупателя`Необходимое`
    + **name** `string` - ФИО покупателя 
    + **discountCardNumber** `string` - Номер скидочной карты/счета
    + **phone** `string` - Номер телефона в произвольном формате 
    + **email** `string` - Почтовый адрес 
    + **legalFirstName** `string` - Имя контрагента
    + **legalMiddleName** `string` - Отчество контрагента
    + **legalLastName** `string` - Фамилия контрагента
    + **birthDate** `date` - Дата рождения контрагента
    + **sex** `enum[string]` - Пол контрагента (Мужской - MALE, женский - FEMALE)
        + Members 
            + MALE
            + FEMALE

+ **positions** `array` - Перечень всех позиций чека
    + **assortment** `object` - Реквизиты позиции в формате метаданных`Необходимое`
        + **meta** `object```Необходимое`
            + **href** `string` - Идентификатор товара/услуги `Необходимое`
            + **id** `string` - Идентификатор товара/услуги `Необходимое`
            + **idType** `string` - тип id. Одно из значений `[native, sync]` `Необходимое`
            + **type** `string` - Тип сущности `Необходимое`
    + **quantity** `number` - Количество в чеке (3 зн. после запятой) `Необходимое`
    + **price** `number` - Цена за единицу (2 зн. после запятой) `Необходимое`
    + **sn** `array` - Список серийных номеров в формате метаданных
          + **meta** `object` `Необходимое`
              + **href** `string` - Идентификатор серийного номера  `Необходимое`
              + **id** `string` - Идентификатор серийного номера `Необходимое`
          + **name** `string` - Серийный номер `string`
    + **pack** `object` - Упаковка
        + **id** `UUID` - Уникальный идентификатор упаковки `Необходимое`
        + **name** `string` - Название упаковки `Необходимое`
        + **quantity** `double` - Количество `Необходимое`
        + **barcode** `string` - Штрихкод
+ **bonusProgram** `object` - Блок информации по баллам `object` 
    + **transactionType** `enum[string]` - Тип операции с баллами (начисление - EARNING, списание - SPENDING) 
        + Default: EARNING
        + Members 
            + EARNING
            + SPENDING
+ **preferredBonusToSpend** `number` - Количество бонусных баллов, которые нужно списать

> **`POST`** 
> /retaildemand/recalc

> **Request**

> Headers

```
Content-Type:application/json
Lognex-Discount-API-Auth-Token:Токен авторизации
```

> Body

```json
{
  "retailStore": {
    "meta": {
      "href": "https://api.moysklad.ru/api/remap/1.2/entity/retailstore/2b5eb22f-139e-11e6-9464-e4de00000073",
      "id": "2b5eb22f-139e-11e6-9464-e4de00000073"
    },
    "name": "Магазин №1"
  },
  "agent": {
    "meta": {
      "href": "https://api.moysklad.ru/api/remap/1.2/entity/counterparty/276a6f50-7ffd-11e6-8a84-bae50000005",
      "id": "276a6f50-7ffd-11e6-8a84-bae50000005"
    },
    "name": "Иванов Иван Иванович",
    "discountCardNumber": "MTIzNDU2Nzg5MA",
    "phone": "+7 555 123 4567",
    "email": "email@example.com",
    "legalFirstName": "Иванов",
    "legalMiddleName": "Иван",
    "legalLastName": "Иванович",
    "sex": "MALE",
    "birthDate": "2023-07-14 00:00:00"
  },
  "positions": [
    {
      "assortment": {
        "meta": {
          "href": "https://api.moysklad.ru/api/remap/1.2/entity/product/9c56720c-e8a7-4fdc-aea4-7104f28207be",
          "id": "9c56720c-e8a7-4fdc-aea4-7104f28207be"
        }
      },
      "quantity": 123.456,
      "price": 123.45,
      "sn": [
        {
          "meta": {
            "href": "https://online.moysklad.ru/api/posap/1.0/entity/sn/2b5eb22f-139e-11e6-9464-e4de00000073",
            "id": "2b5eb22f-139e-11e6-9464-e4de00000073"
          },
          "name": "7895545"
        }
      ],
      "pack": {
        "id": "98f87a95-c0b6-11ee-0a80-06e1000360e2",
        "name": "Бутылка 1,5 л",
        "quantity": 1.5,
        "barcode": "2000000051420"
      }
    }
  ],
  "bonusProgram": {
    "transactionType": "EARNING"
  }
}
```

#### Атрибуты ответа  
+ **agent** `object` - Реквизиты покупателя в формате метаданных `Необходимое`
    + **meta** `object` `Необходимое`
        + **href**: `string` - Идентификатор покупателя `Необходимое`
        + **id**: `string` - Идентификатор покупателя `Необходимое`
    + **name**: `string` - ФИО покупателя
    + **discountCardNumber**: `string` - Номер скидочной карты/счета
    + **phone**: `string` - Номер телефона в произвольном формате
    + **email**: `string` - Почтовый адрес  
    + **legalFirstName** `string` - Имя контрагента
    + **legalMiddleName** `string` - Отчество контрагента
    + **legalLastName** `string` - Фамилия контрагента
    + **birthDate** `date` - Дата рождения контрагента
    + **sex** `enum[string]` - Пол контрагента (Мужской - MALE, женский - FEMALE)
        + Members 
            + MALE
            + FEMALE
+ **positions** `array` - Перечень всех позиций чека
    + **assortment** `object` - Реквизиты позиции в формате метаданных `Необходимое`
        + **meta** `object` `Необходимое`
            + **href**: `string` - Идентификатор товара/услуги `Необходимое`
            + **id**: `string` - Идентификатор товара/услуги `Необходимое`
    + **quantity**: `number` - Количество в чеке (3 зн. после запятой) `Необходимое`
    + **price**: `number` - Цена за единицу (2 зн. после запятой) `Необходимое`
    + **discountPercent**: `number` - Процент скидки (2 зн. после запятой). от 0 до 100 `Необходимое`
    + **discountedPrice**: `number` - Цена с учетом скидки (2 зн. после запятой) `Необходимое`
    + **sn** `array` - Коллекция уникальных идентификаторов серийных номеров в формате метаданных. Если массив не пуст, то количество товаров в позиции (quantity) должно быть равно количеству серийных номеров, переданных в значении атрибута
          + **meta** `object` `Необходимое`
              + **href**: `string` - Идентификатор серийного номера `Необходимое`
              + **id**: `string` - Идентификатор серийного номера `Необходимое`
          + **name**: `string` - Серийный номер
    + **pack** `object` - Упаковка
        + **id** `UUID` - Уникальный идентификатор упаковки `Необходимое`
        + **name** `string` - Название упаковки `Необходимое`
        + **quantity** `double` - Количество `Необходимое`
        + **barcode** `string` - Штрихкод
+ **bonusProgram** `object` - Блок информации по баллам
    + **transactionType**: `enum[string]` - Тип операции с баллами (начисление - EARNING, списание - SPENDING)
        + Default: EARNING
        + Members 
            + EARNING
            + SPENDING
    + **agentBonusBalance**: `number` - Баланс баллов покупателя до продажи.
    + **bonusValueToSpend**: `number` - Сколько будет списано баллов за продажу. В случае отсутствия/null поля **preferredBonusToSpend** стоит возвращать максимально доступную сумму для списания по этой продаже.
    + **bonusValueToEarn**: `number` - Сколько может быть начислено баллов за продажу.
    + **agentBonusBalanceAfter**: `number` - Баланс баллов покупателя после продажи.
    + **paidByBonusPoints**: `number` - Сумма оплаченная бонусами (2 знака после запятой).
    + **receiptExtraInfo**: `string` - Дополнительный текст для вывода в чеке, может содержать переносы строк.
+ **needVerification** `boolean` - Флаг, показывающий нужно ли запросить код для проверки личности контрагента.

> **Response**   
> 200 (application/json)

> Headers

```
Content-Type:application/json
```

> Body

```json
{
  "agent": {
    "meta": {
      "href": "https://api.moysklad.ru/api/remap/1.2/entity/counterparty/276a6f50-7ffd-11e6-8a84-bae50000005",
      "id": "276a6f50-7ffd-11e6-8a84-bae50000005"
    },
    "name": "Иванов Иван Иванович",
    "discountCardNumber": "MTIzNDU2Nzg5MA",
    "phone": "+7 555 123 4567",
    "email": "email@example.com",
    "legalFirstName": "Иванов",
    "legalMiddleName": "Иван",
    "legalLastName": "Иванович",
    "sex": "MALE",
    "birthDate": "2023-07-14 00:00:00"
  },
  "positions": [
    {
      "assortment": {
        "meta": {
          "href": "https://api.moysklad.ru/api/remap/1.2/entity/product/9c56720c-e8a7-4fdc-aea4-7104f28207be",
          "id": "9c56720c-e8a7-4fdc-aea4-7104f28207be"
        }
      },
      "quantity": 123.456,
      "price": 123.45,
      "discountPercent": 49.99,
      "discountedPrice": 62.95,
      "sn": [
        {
          "meta": {
            "href": "https://online.moysklad.ru/api/posap/1.0/entity/sn/2b5eb22f-139e-11e6-9464-e4de00000073",
            "id": "2b5eb22f-139e-11e6-9464-e4de00000073"
          },
          "name": "7895545"
        }
      ],
      "pack": {
        "id": "98f87a95-c0b6-11ee-0a80-06e1000360e2",
        "name": "Бутылка 1,5 л",
        "quantity": 1.5,
        "barcode": "2000000051420"
      }
    }
  ],
  "bonusProgram": {
    "transactionType": "EARNING",
    "agentBonusBalance": 500,
    "bonusValueToSpend": 0,
    "bonusValueToEarn": 150,
    "agentBonusBalanceAfter": 650,
    "paidByBonusPoints": 0,
    "receiptExtraInfo": "Спасибо за участие в нашей программе!"
  },
  "needVerification": false
}
```

### Запрос кода подтверждения списания баллов

Метод предназначен для запроса кода у внешней бонусной программы с целью подтверждения списания бонусов.

#### Атрибуты запроса

+ **retailStore** `object` `Необходимое`
    + **meta** `object` `Необходимое`
        + **href** `string` - Идентификатор точки продаж `Необходимое`
        + **id** `string` - Идентификатор точки продаж `Необходимое`
    + **name** `string` - Название точки продаж
+ **counterpartyId** `string` `Необходимое` - Идентификатор контрагента, необходимый для синхронизации.
+ **phone** `string` - Телефонный номер покупателя, указанный в карточке контрагента.

> **`POST`**
> /retaildemand/verify

> **Request**

> Headers

```
Content-Type:application/json
Lognex-Discount-API-Auth-Token:Токен авторизации
```

> Body

```json
{
  "retailStore": {
    "meta": {
      "href": "https://api.moysklad.ru/api/remap/1.2/entity/retailstore/2b5eb22f-139e-11e6-9464-e4de00000073",
      "id": "2b5eb22f-139e-11e6-9464-e4de00000073"
    },
    "name": "Магазин №1"
  },
  "counterpartyId": "75d9ba29-2c4a-4c1c-a3a8-8db00366ac04",
  "phone": "+79011231122"
} 
```

#### Атрибуты ответа
+ **verificationCode** `string` `Необходимое` - Код, отправленный покупателю.
+ **timeForRepeat** `integer` - Время в секундах, по прошествии которого, можно запросить код повторно.
+ **messageForCashier** `string` - Сообщение, которое необходимо отобразить кассиру (140 символов).

> **Response**   
> 200 (application/json)

> Headers

```
Content-Type:application/json
```

> Body

```json
{
  "verificationCode":"123456",
  "timeForRepeat": 60,
  "messageForCashier": "Код был отправлен на номер покупателя: +79011231122"
}
```

### Создание продажи 

Запрос на создание новой продажи. Если при продаже начислялись или списывались баллы, информация об этом указывается в секции `bonusProgram`

#### Атрибуты сущности  
  
+ **retailStore** `object` `Необходимое`
    + **meta** `object` `Необходимое`
        + **href** `string`- Идентификатор точки продаж `Необходимое`
        + **id**: `string` - Идентификатор точки продаж `Необходимое`
    + **name** `string` - Название точки продаж
+ **name** `string` - Номер продажи
+ **moment** `string` - Дата продажи
+ **meta** `object` - Реквизиты продажи в формате метаданных `Необходимое`
    + **href** `string` - Идентификатор продажи (URL) `Необходимое`
    + **id** `string` - Идентификатор продажи `Необходимое`
+ **agent** `object` - Реквизиты покупателя в формате метаданных
    + **meta** `object`
        + **href** `string` - Идентификатор покупателя `Необходимое`
        + **id** `string` - Идентификатор покупателя `Необходимое`
    + **name** `string` - ФИО покупателя
    + **discountCardNumber** `string` - Номер скидочной карты/счета
    + **phone** `string` - Номер телефона в произвольном формате
    + **email** `string` - Почтовый адрес
    + **legalFirstName** `string` - Имя контрагента
    + **legalMiddleName** `string` - Отчество контрагента
    + **legalLastName** `string` - Фамилия контрагента
    + **birthDate** `date` - Дата рождения контрагента
    + **sex** `enum[string]` - Пол контрагента (Мужской - MALE, женский - FEMALE)
        + Members 
            + MALE
            + FEMALE
+ **positions** `array` - Перечень всех позиций чека
    + **assortment** `object` - Реквизиты позиции в формате метаданных
        + **syncId** `string` - Уникальный идентификатор, присвоенный товару/услуге при создании через Кассу МойСклад или JSON API
        + **meta** `object`
            + **href** `string` - Идентификатор товара/услуги `Необходимое`
            + **id** `string` - Идентификатор товара/услуги `Необходимое`
    + **quantity** `number` - Количество в чеке (3 зн. после запятой)
    + **price** `number` - Цена за единицу (2 зн. после запятой)
    + **discountPercent** `number` - Процент скидки (2 зн. после запятой)
    + **discountedPrice** `number` - Цена с учетом скидки (2 зн. после запятой)
+ **bonusProgram** `object` - Блок информации по баллам
    + **bonusValueToSpend** `number` - Сколько может быть списано баллов за продажу
    + **bonusValueToEarn** `number` - Сколько может быть начислено баллов за продажу
+ **cashSum** `number` - Оплачено наличными (в рублях)
+ **noCashSum** `number` - Оплачено картой (в рублях)

> **`POST`** 
> /retaildemand

> **Request**

> Headers

```
Content-Type:application/json
Lognex-Discount-API-Auth-Token:Токен авторизации
```

> Body

```json
{
  "retailStore": {
    "meta": {
      "href": "https://api.moysklad.ru/api/remap/1.2/entity/retailstore/2b5eb22f-139e-11e6-9464-e4de00000073",
      "id": "2b5eb22f-139e-11e6-9464-e4de00000073"
    },
    "name": "Магазин №1"
  },
  "name": "00001",
  "moment": "2016-04-18 15:06:00",
  "meta": {
    "href": "",
    "id": ""
  },
  "agent": {
    "meta": {
      "href": "https://api.moysklad.ru/api/remap/1.2/entity/counterparty/276a6f50-7ffd-11e6-8a84-bae50000005",
      "id": "276a6f50-7ffd-11e6-8a84-bae50000005"
    },
    "name": "Иванов Иван Иванович",
    "discountCardNumber": "MTIzNDU2Nzg5MA",
    "phone": "+7 555 123 4567",
    "email": "email@example.com",
    "legalFirstName": "Иванов",
    "legalMiddleName": "Иван",
    "legalLastName": "Иванович",
    "sex": "MALE",
    "birthDate": "2023-07-14 00:00:00"
  },
  "positions": [
    {
      "assortment": {
        "syncId": "f085d67e-6eae-11e6-8a84-bc520403352a",
        "meta": {
          "href": "https://api.moysklad.ru/api/remap/1.2/entity/product/9c56720c-e8a7-4fdc-aea4-7104f28207be",
          "id": "9c56720c-e8a7-4fdc-aea4-7104f28207be"
        }
      },
      "quantity": 123.456,
      "price": 123.45,
      "discountPercent": 49.99,
      "discountedPrice": 62.95
    }
  ],
  "bonusProgram": {
    "bonusValueToSpend": 0,
    "bonusValueToEarn": 150
  },
  "cashSum": 62.95,
  "noCashSum": 283.1
} 
```


> **Response**  
> 201
