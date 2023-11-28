# Сущности

## Покупатель

### Создание покупателя

Запрос на создание нового покупателя.

#### Атрибуты сущности
+ **retailStore** `object` `Необходимое`
    + **meta** `object` `Необходимое`
        + **href** `string`  - Идентификатор точки продаж `Необходимое`
        + **id** `string` - Идентификатор точки продаж `Необходимое`
    + **name** `string` - Название точки продаж
+ **meta** `object` `Необходимое`
    + **href** `string` - Идентификатор покупателя `Необходимое`
    + **id** `string` - Идентификатор покупателя `Необходимое`
+ **name**`string` - ФИО покупателя 
+ **discountCardNumber** `string` - Номер дисконтной карты
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

+ **syncId** `string` - Уникальный идентификатор, присвоенный покупателю при создании через Кассу МойСклад
+ **statusCheck** `enum[string]` - Статус верификации контрагента через код подтверждения
  + Members
    + UNCHECKED - Верификация контрагента по коду подтверждения не была произведена
    + CHECKED - Верификация контрагента по коду подтверждения была произведена
    + IGNORE - Верификация контрагента по коду подтверждения была проигнорирована, такой контрагент в любом случае попадает в базу данным МоегоСклада.

> **`POST`** 
> /counterparty

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
  "meta": {
    "href": "https://api.moysklad.ru/api/remap/1.2/entity/counterparty/276a6f50-7ffd-11e6-8a84-bae50000005",
    "id": "276a6f50-7ffd-11e6-8a84-bae50000005"
  },
  "name": "Иванов Иван Иванович",
  "discountCardNumber": "MTIzNDU2Nzg5MA",
  "phone": "+7 555 123 4568",
  "email": "email@example.com",
  "syncId": "6ebefb74-f6e3-4ef1-b155-5232a2ae396a",
  "legalFirstName": "Иванов",
  "legalMiddleName": "Иван",
  "legalLastName": "Иванович",
  "birthDate": "2023-07-14 00:00:00",
  "sex": "MALE",
  "statusCheck": "CHECKED"
}
```

> **Response**  
> 201

### Поиск покупателя 

Запрос на поиск существующего покупателя.

#### Параметры
| Параметр | Описание   |
|---|---|
| search | `string` *Example: 9039993344* Строка с поисковым запросом |

#### Атрибуты сущности
+ **rows** `array` - Список покупателей
    + Покупатель `object`
        + **id** `string` - Уникальный идентификатор покупателя в системе лояльности в формате GUID `Необходимое`
        + **msId** `string` - Уникальный идентификатор покупателя в системе МойСклад в формате GUID
        + **name** `string` - ФИО покупателя `Необходимое`
        + **discountCardNumber** `string` - Номер дисконтной карты 
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

> **`GET`** 
> /counterparty?search=9039993344

> **Request**

> Headers

```
Content-Type:application/json
Lognex-Discount-API-Auth-Token:Токен авторизации
```

> **Response**  
> 200 (application/json)

```json
{
  "rows": [
    {
      "id": "2b5eb22f-139e-11e6-9464-e4de00000073",
      "msId": "276a6f50-7ffd-11e6-8a84-bae50000005",
      "name": "Иванов Иван Иванович",
      "discountCardNumber": "MTIzNDU2Nzg5MA",
      "phone": "+7 555 123 4567",
      "email": "email@example.com",
      "legalFirstName":"Иванов",
      "legalMiddleName":"Иванович",
      "legalLastName":"Иванов",
      "birthDate": "2023-07-14 00:00:00",
      "sex": "MALE"
    }
  ]
}
```

### Получение баланса баллов покупателя 

Запрос на получение баланса покупателя. Поиск и идентификация покупателя идет по идентификатору покупателя `id` из метаданных.
Прочие реквизиты несут информационный характер и могут не предаваться. Передача нескольких покупателей в ответе **не допускается**.


#### Атрибуты сущности   

+ **retailStore** `object` `Необходимое`
    + **meta** `object` `Необходимое`
        + **href**  `string` - Идентификатор точки продаж `Необходимое`
        + **id** `string` - Идентификатор точки продаж `Необходимое`
    + **name** `string` - Магазин №1 - Название точки продаж
+ **meta** `object` `Необходимое`
    + **href** `string` - Идентификатор покупателя `Необходимое`
    + **id** `string` - Идентификатор покупателя `Необходимое`
+ **name** `string` - ФИО покупателя 
+ **discountCardNumber** `string` - Номер скидочной карты/счета
+ **phone** `string` - Номер телефона в произвольном формате
+ **email** `string` -  Почтовый адрес  
+ **legalFirstName** `string` - Имя контрагента
+ **legalMiddleName** `string` - Отчество контрагента
+ **legalLastName** `string` - Фамилия контрагента
+ **birthDate** `date` - Дата рождения контрагента
+ **sex** `enum[string]` - Пол контрагента (Мужской - MALE, женский - FEMALE)
    + Members 
        + MALE
        + FEMALE

#### Атрибуты ответа  
+ **bonusProgram** `object` - Блок информации по баллам 
    + **agentBonusBalance** `number` - Баланс баллов покупателя до продажи (текущий баланс)`Необходимое`

> **`POST`** 
> /counterparty/detail

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
  "meta": {
    "href": "https://api.moysklad.ru/api/remap/1.2/entity/counterparty/276a6f50-7ffd-11e6-8a84-bae50000005",
    "id": "276a6f50-7ffd-11e6-8a84-bae50000005"
  },
  "name": "Иванов Иван Иванович",
  "discountCardNumber": "MTIzNDU2Nzg5MA",
  "phone": "+7 555 123 4567",
  "email": "email@example.com",
  "legalFirstName":"Иванов",
  "legalMiddleName":"Иванович",
  "legalLastName":"Иванов",
  "birthDate": "2023-07-14 00:00:00",
  "sex": "MALE"
}
```
> **Response**  
> 200 (application/json)


> Body

```json
{
  "bonusProgram": {
    "agentBonusBalance": 500
  }
}
```

### Подготовка к запросу кода подтверждения регистрации покупателя

Если для регистрации покупателя с атрибутом `"statusCheck": "UNCHECKED"` требуется провести подтверждение через код,
то необходимо в ответе на запрос вернуть ошибку:

> **Response**  
> 412 (application/json)

```json
{
  "errors": [
    {
      "error": "Необходимо подтверждение создания покупателя.",
      "code": 28001,
      "error_message": "Покупатель должен подтвердить свои данные через код."
    }
  ]
}
```

### Получение кода подтверждения регистрации покупателя

Метод предназначен для запроса кода у внешней бонусной программы с целью подтверждения регистрации покупателя.

#### Атрибуты сущности

+ **meta** `object` `Необходимое`
  + **href** `string` - Идентификатор покупателя `Необходимое`
+ **name** `string` - ФИО покупателя
+ **discountCardNumber** `string` - Номер скидочной карты/счета
+ **phone** `string` - Номер телефона в произвольном формате
+ **email** `string` -  Почтовый адрес
+ **legalFirstName** `string` - Имя контрагента
+ **legalMiddleName** `string` - Отчество контрагента
+ **legalLastName** `string` - Фамилия контрагента
+ **birthDate** `date` - Дата рождения контрагента
+ **sex** `enum[string]` - Пол контрагента (Мужской - MALE, женский - FEMALE)
  + Members
    + MALE
    + FEMALE

> **`POST`**
> /counterparty/verify

> **Request**

> Headers

```
Content-Type:application/json
Lognex-Discount-API-Auth-Token:Токен авторизации
```

> Body

```json
{
  "meta": {
    "href": "https://api.moysklad.ru/api/posap/1.0/entity/counterparty/syncid/276a6f50-7ffd-11e6-8a84-bae50000005"
  },
  "name":"Ромашкова Варвара Никитична",
  "discountCardNumber":"09716398",
  "phone":"+79011231122",
  "email":"romashkova@fmail.com",
  "legalFirstName":"Варвара",
  "legalMiddleName":"Никитична",
  "legalLastName":"Ромашкова",
  "birthDate":"1992-08-01 00:00:00.000",
  "sex":"FEMALE"
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
