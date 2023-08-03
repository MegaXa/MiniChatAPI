# MiniChat API

**Текущая версия: 0.11.X**
**Последнее обновление: 18.03.23**

Для подключения к серверу чата следует использовать websocket соединение по адресу: ws://localhost:4848/Chat

Порт по умолчанию: 4848, но зависит от настройки в MiniChat.


#### **Общий тип JSON сообщения:**
```
{
  "Type": "EventType", // Тип события.
  "Data": {Object} // Полезные данные.
}
```

#### **Типы событий (EventType):**

* Unknown - По умолчанию, не используется.
* Message - Обычное сообщение.
* Live - Событие на сервисе (Отслеживание, подписка, подарок, рейд, хотс и т.д.).
* DeleteMessage - Удаление сообщения.
* UserBan - Бан пользователя.
* UserMute - Временная блокировка пользователя.
* SettingsTheme - Настройки темы.
* Await - Ожидание подключения к чату, если чат не перманентный.
* Connect - Подключение к сервису и информация о канале.
* State - Информация о чате сервиса. (Роли в чате, доступные методы для вызова).
* Reconnect - Переподключение к чату сервиса.
* Disconnect - Отключение от сервиса.
* NotFound - Не найден пользователь для подключения.
* UnknownError - Неизвестная ошибка.
* Speak -  Синтез речи.
* Avatar - Аватар.


#### **Обычное сообщение (Message):**

```
{
  "Service": "Service",
  "GUID": "4da6dd37-158c-4c17-bf8c-2277d568417d",
  "Date": "1973-01-01T00:00:00.000+00:00",
  "UserName": "MegaXa",
  "UserID": "0",
  "Color": "#323232",
  "Badges": [
    {
      "Text": "Новый спонсор",
      "Image": {
        "Default": "https://megaxa.ru/badge.png",
        "Large": "https://megaxa.ru/badge2X.png"
      }
    }
  ],
  "MessageKit": [
    {
      "Type": "MessageKitType",
      "Data": {
        "Text": ":200IQ:",
        "URL": "https://megaxa.ru/",
        "Image": {
          "Default": "https://megaxa.ru/emoticon.png",
          "Large": "https://megaxa.ru/emoticon2X.png"
        }
      }
    }
  ],
  "Avatar": {
    "Default": "https://megaxa.ru/avatar.png",
    "Large": "https://megaxa.ru/avatar2X.png"
  },
  "Roles": [
    "Owner",
    "Subscriber"
  ],
  "Reply": false,
  "Meta": {
    "Me": false,
    "Login": "megaxa",
    "Highlighted": false
  }
}
```

#### **Список сервисов (Service):**

* Unknown - По умолчанию.
* MiniChat
* Twitch
* YouTube
* GoodGame
* DonationAlerts
* VK
* DonatePay
* WASD
* Steam
* Facebook
* OK
* Trovo
* Peka2
* DLive
* YouNow
* Tango
* Rutube
* Telegram
* VKPlay
* Boosty
* QIWIDonate
* DonateStream

#### **Список типов для конструктора сообщения (MessageKitType):**

* Unknown - По умолчанию.
* Text - Текст.
* Emoticon - Смайлик.
* URL - Ссылка.
* Image - Изображение.
* Sticker - Стикер.

#### **Типы “Live”событий (LiveType):**

* Follow
* UnFollow
* Subscription
* GiftSubscription
* Donation
* Reward
* Support
* Host
* Raid
* Winner

#### **Типы валют для  “Live”событий типа “Reward” или “Support” (CurrencyType):**

* ChannelPoints - “Баллы канала (Twitch)”.
* Mana - “Мана (Trovo)”.
* Lemon - “Лимоны (DLive)”.
* Bits - “Bits (Twitch)”.
* Elixir  - “Эликсир (Trovo)”.
* Diamond - “Алмазы (Bigo)”.
* OK - “OK (Одноклассники)”.


#### **Удаление сообщения (DeleteMessage):**

```
{
  "Type": "DeleteMessage",
  "Data": {
    "GUID": "00000000-0000-0000-0000-000000000000"
  }
}
```

#### **Запрос на получение настроек виджета (WidgetProperties):**

```
{
  "Type": "WidgetProperties",
  "Data": {
    "Type": "Chat",
    "FolderName": "Dev",
    "ID": 0
  }
}
```

#### **Запрос на отправку сообщения (Message):**

```
{
  "Type": "Message",
  "Data": {
    "Service": "Service",
    "Message": "Сообщение для отправки.",
    "Hide": false
  }
}
```

#### **Запрос на отправку сообщения в MiniChat (Message):**

```
{
  "Type": "Message",
  "Data": {
    "Service": "MiniChat",
    "UserName": "MegaXa",
    "Message": "Тест."
  }
}
```

#### **Запрос на удаление сообщения (DeleteMessage):**

```
{
  "Type": "DeleteMessage",
  "Data": {
    "Service": "Service",
    "GUID": "00000000-0000-0000-0000-000000000000"
  }
}
```

#### **Запрос на синтез речи (Speak):**

Актуальный список голосов можно получить из соответствующего виджета.

VoiceArray = [ 'Maxim', 'Tatyana', 'Alice', 'Marusia', 'Svetlana', 'Dmitry', 'Ermilov', 'Zahar', 'Jane', 'Alyss', 'Omazh', 'Oksana' ]

```
{
  "Type": "Speak",
  "Data": {
    "GUID": "00000000-0000-0000-0000-000000000000",
    "Message": "Тест озвучки",
    "Voice": "Голос",
    "Pitch": "0"
  }
}
```

**Пример**:

```
{"Type":"Speak","Data":{"Voice":"Alice","Message":"1% 2% 3% 4% 5% 6% 7% 8% 9% 10%"}}
```

#### **Запрос на получение истории (History):**

```
{
  "Type": "History",
  "Data": {
    "Type": "Live",
    "Limit": 100,
    "Filter": {
      "Follow": false
    }
  }
}
```

**Пример**:

```
{"Type":"History","Data":{"Type":"Live","Limit":10,"Filter": {"Follow": false,"UnFollow": false}}}
```

#### **REST API:**

Принимаются POST запросы на адрес [http://localhost:4848/api](http://localhost:4848/api)

Формат как в случае с WebSockets.
В данный момент поддерживаются: Message, DeleteMessage, UserBan, UserUnban, Speak (Речь будет отправлена в первый виджет синтеза речи).

#### **PubSub:**

Используется для взаимодействия плагинов друг с другом.
Для подключения к серверу PubSub следует использовать WebSocket соединение по адресу: ws://localhost:4848/PubSub

#### **Типы событий (PubSubType):**

* Unknown - По умолчанию, зарезервирован.
* Subscribe - Подписаться на события.
* UnSubscribe - Отписаться от событий.
* Echo - Эхо (Вернуть запрос в клиент).
* Ping - Пинг.

При указании другого типа события данные будут отправлены всем подписавшимся клиентам на данное событие, например:

```
{"Type":"SoundPlay","Data":{"Play":"test.mp3"}}
```

#### **Подписаться на события (Subscribe):**

```
{
  "Type": "Subscribe",
  "Data": {
    "Events": [
      "SoundPlay",
      "SoundPause"
    ]
  }
}
```

#### **Отписаться от событий (UnSubscribe):**

```
{
  "Type": "UnSubscribe",
  "Data": {
    "Events": [
      "SoundPause"
    ]
  }
}
```

#### **Ответ на событие Subscribe, UnSubscribe:**

При успешном запросе вернется список с текущими подписками:

```
{"Type":"Subscribed","Data":{"Events":["SoundPlay","SoundPause"]}}
```

#### **Вернуть данные в клиент (Echo):**

```
{
  "Type": "Echo",
  "Data": {
    "Test": "Kappa"
  }
}
```

#### **Пинг сервера (Ping):**

```
{
  "Type": "Ping"
}
```
