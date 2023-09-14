# HTTP-services API (1.1.0.1)

## Оглавление

[Изменения](#изменения)

---

- [Доступность сервиса](#доступность-сервиса)

---

- [**Списки**](#списки)

- [Номенклатура клиента](#номенклатура-клиента)

---

## Изменения

Изменения в описании отменчены следующим образом (\*)

---

## Доступность сервиса

### Описание

Предназначен для проверки доступности сервиса.

Метод - **GET**

### Описание шаблона

**_URL_**:

```html
https://server.ru/mosDataToClient/ping
```

Тело ответа содержит _JSON_ с следующими параметрами:

| Параметры                             |           Тип            | Обязательный | Описание                          |
| ------------------------------------- | :----------------------: | :----------: | :-------------------------------- |
| [result](#result-доступность-сервиса) | Null, либо данные ответа |      Да      | Не заполняется при ошибке         |
| error                                 |          Строка          |      Да      | Строка описания ошибки            |
| errorCode                             |          Строка          |      Да      | Код ошибки в классификации API    |
| notice                                |          Строка          |      Да      | Текст с дополнительной информации |

#### **result (Доступность сервиса):**

| Параметры |  Тип   | Обязательный | Описание                                      |
| --------- | :----: | :----------: | :-------------------------------------------- |
| text      | Строка |      Да      | Возвращает "ok" при успешном соединении       |
| ver       | Строка |      Да      | Возвращает строковое представление версии API |

### Пример

**Ответ в формате _JSON_**:

```json
{
  "result": {
    "text": "ok",
    "ver": "1.1.0.1"
  },
  "error": null,
  "errorCode": null,
  "notice": null
}
```

---

## Списки

---

## Номенклатура клиента

### Описание

Предназначен для получения списка каналов продаж

Метод - **GET**

### Описание шаблона

**_URL_**:

```html
https://server.ru/mosDataToClient/product/forOrder?perID={perID}
```

где perID - идентификатор (строка (36)) личного кабинета

Тело ответа содержит _JSON_ с следующими параметрами:

| Параметры                              |     Тип      | Обязательный | Описание                          |
| -------------------------------------- | :----------: | :----------: | :-------------------------------- |
| [result](#result-номенклатура-клиента) | Null, Массив |      Да      | Не заполняется при ошибке         |
| error                                  | Null, Строка |      Да      | Строка описания ошибки            |
| errorCode                              | Null, Строка |      Да      | Код ошибки в классификации API    |
| notice                                 | Null, Строка |      Да      | Текст с дополнительной информации |

#### **result (Номенклатура клиента):**

| Параметры                                                |      Тип      | Обязательный | Описание                          |
| -------------------------------------------------------- | :-----------: | :----------: | :-------------------------------- |
| uID                                                      |  Строка(36)   |      Да      | Идентификатор номенклатуры (guid) |
| article                                                  |  Строка(25)   |      Да      | Артикул                           |
| code                                                     |  Строка(11)   |      Да      | Код                               |
| name                                                     | Строка (100)  |      Да      | Наименование                      |
| fullName                                                 | Строка (1000) |      Да      | Наименование полное               |
| groupName                                                | Строка (100)  |      Да      | Наименование группы               |
| description                                              | Строка (500)  |      Да      | Комментарий                       |
| [otherProperties](#otherproperties-номенклатура-клиента) |    Массив     |      Да      | Массив дополнительных свойств     |

#### **otherProperties (Номенклатура клиента):**

| Параметры |                        Тип                         | Обязательный | Описание                                                                                                                |
| --------- | :------------------------------------------------: | :----------: | :---------------------------------------------------------------------------------------------------------------------- |
| uID       |                     Строка(36)                     |      Да      | Идентификатор свойства (guid)                                                                                           |
| name      |                     Строка(25)                     |      Да      | Наименование свойства                                                                                                   |
| typeValue |                     Число (1)                      |      Да      | Тип значения: 0 - Строка, 1 - Число, 2 - Булево, 3 - Дата, 4 - Ссылочный тип в 1С, в ключе Value будет приходить Строка |
| value     | Строка, Число, Булево, Дата (строка в формате UTC) |      Да      | Значение                                                                                                                |

### Пример

**_URL_**:

```html
https://server.ru/mosDataToClient/product/forOrder?perID=c09c91e5-a53d-4e15-9ffe-13e54b734b6f
```

**Ответ в формате _JSON_**:

```json
{
  "result": [
    {
      "uID": "bd433688-4e62-11e9-80d1-0050569133d8",
      "article": "N093430",
      "code": "НФ-00020717",
      "name": "УПЛОТНЕНИЕ",
      "fullName": "УПЛОТНЕНИЕ",
      "groupName": "Запчасти DeWalt",
      "description": "",
      "otherProperties": []
    },
    {
      "uID": "a934b420-0be9-11ed-81a1-00155df43005",
      "article": "DW125DR-PL-PR50",
      "code": "НФ-00250627",
      "name": "Алмазная шлифовальная чашка. Размером  125MM DCUT (50шт)",
      "fullName": "Алмазная шлифовальная чашка. Размером  125MM DCUT (50шт)",
      "groupName": "Алмазные чашки",
      "description": "",
      "otherProperties": [
        {
          "uID": "3e758628-cd37-11ed-81ba-00155df43005",
          "name": "Посадочный диаметр, мм",
          "typeValue": 4,
          "value": "22.2"
        },
        {
          "uID": "4a962fc8-cd37-11ed-81ba-00155df43005",
          "name": "Тип",
          "typeValue": 4,
          "value": "двухрядная"
        }
      ]
    }
  ],
  "error": null,
  "errorCode": null,
  "notice": null
}
```

---
