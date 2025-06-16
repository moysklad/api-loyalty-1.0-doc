## Подарочный сертификат

### Поиск подарочного сертификата

Запрос на получение данных подарочного сертификата по номеру.

#### Параметры
| Параметр      | Описание                                                                                          |
|---------------|---------------------------------------------------------------------------------------------------|
| name          | `string` *Example: 123456* Номер сертификата                                                      |
| retailStoreId | `string` *Example: 2b5eb22f-139e-11e6-9464-e4de00000073* Идентификатор точки продаж `Необходимое` |

> **`GET`**
> /giftcard?name=123456&retailStoreId=2b5eb22f-139e-11e6-9464-e4de00000073

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
  "name": "123456",
  "id": "276a6f50-7ffd-11e6-8a84-bae50000005",
  "status": "CAN_BE_USED",
  "expireDate": "2025-07-14 00:00:00",
  "currentBalance": "1000",
  "initialBalance": "1000"
}
```
