
Список API
--------

| Тип API | **Тип содержания** | **Контекст** | **Тип запроса** | **Описание** | **Требуется подпись** |
| --------- | ---------------- | ------------------------------------------------ | ---------------- | ---------------------------------------------- | ---------------------- |
| Restful   | Market Data      | <a href="#1">api/v1/contract_contract_info </a>     | GET              | Get Contracts Information                      | No                     |
| Restful   | Market Data      | <a href="#2">api/v1/contract_index </a>             | GET              | Get contract Index Price Information           | No                     |
| Restful   | Market Data      | <a href="#3"> api/v1/contract_price_limit </a>      | GET              | Get Contract Price Limits                      | No                     |
| Restful   | Market Data      | <a href="#4"> api/v1/contract_open_interest</a>     | GET              | Get Contract Open Interest Information         | No                     |
| Restful   | Market Data      | <a href="#5"> /market/depth </a>                 | GET              | Get Market Depth                               | No                     |
| Restful   | Market Data      | <a href="#6">/market/history/kline  </a>         | GET              | Get K-Line Data                                | No                     |
| Restful   | Market Data      | <a href="#7"> /market/detail/merged </a>         | GET              | Get Market Data Overview                       | No                     |
| Restful   | Market Data      | <a href="#8"> /market/trade </a>                 | GET              | The Last Trade of a Contract                   | No                     |
| Restful   | Market Data      | <a href="#9">/market/history/trade  </a>         | GET              | Request a Batch of Trade Records of a Contract | No                     |
| Restful   | Account          | <a href="#101"> api/v1/contract_account_info </a>   | POST             | User’s Account Information                     | Yes                    |
| Restful   | Account          | <a href="#102">api/v1/contract_position_info  </a>  | POST             | User’s position Information                    | Yes                    |
| Restful   | Trade            | <a href="#103"> api/v1/contract_order </a>          | POST             | Place an Order                                 | Yes                    |
| Restful   | Trade            | <a href="#104">api/v1/contract_batchorder   </a>    | POST             | Place a Batch of Orders                        | Yes                    |
| Restful   | Trade            | <a href="#105">api/v1/contract_cancel </a>          | POST             | Cancel an Order                                | Yes                    |
| Restful   | Trade            | <a href="#106">api/v1/contract_cancelall  </a>      | POST             | Cancel All Orders                              | Yes                    |
| Restful   | User Order Info  | <a href="#107">api/v1/contract_order_info  </a>     | POST             | Get Information of an Order                    | Yes                    |
| Restful   | User Order Info  | <a href="#108"> api/v1/contract_order_detail  </a>  | POST             | Get Trade Details of an Order                  | Yes                    |
| Restful   | User Order Info  | <a href="#109"> api/v1/contract_openorders  </a>    | POST             | Get Current Orders                             | Yes                    |
| Restful   | User Order Info  | <a href="#110"> api/v1/contract_hisorders  </a>     | POST             | Get History Orders                             | Yes                    |


Проверка подлинности подписи
--------

#### <a name="199">Authentication Method</a>

Частный интерфейс пользователя (учетная запись, торговля и данные по ордерам пользователя), все интерфейсы, имеющие отношение к пользователю, должны пройти верификацию, чтобы проверить законность пользователя.
Метод аутентификации такой же, как и для наличных товаров. Подробности здесь:

<https://github.com/huobiapi/API_Docs/wiki/REST_authentication>


#### <a name="200">API Rate Limit Illustration</a>


Обратите внимание, что как для публичного интерфейса, так и для частного интерфейса установлены лимиты скорости. Подробности ниже::
* Как правило, лимит скорости API-ключа для частного интерфейса составляет не более 10 раз/сек для каждого UID (это ограничение скорости 10 раз/сек используется всеми контрактами альткоинов, выполненными в другую дату).
* Для публичного интерфейса, используемого для получения информации об индексе, ценовом пределе, расчете, выполнении, открытых позициях и т. д., лимит скорости составляет не более 20 раз/сек для каждого IP (это ограничение скорости публичного интерфейса 20 раз/сек используется всеми запросами от этого IP нерыночной информации, как указано выше).
* С точки зрения публичного интерфейса, используемого для получения данных графика свечей, последней записи о транзакциях и информации о совокупном рынке, таблице заявок и т. д., лимит скорости выглядит следующим образом:
  

(1) для Restful интерфейса: максимум 200 раз/сек для одного IP.

(2) для Websocket: ограничение скорости для запроса “req” составляет 50 раз за один промежуток времени. Ограничение скорости для запроса “sub” отсутствует, так как данные будут передаваться сервером добровольно.
* Если у Вас есть особые требования к лимиту скорости API, пожалуйста, отправьте заявку на dm_mm@huobi.com с темой “Заявка на повышение лимита скорости API”. В письме должна содержаться следующая информация:

 

(1) Пожалуйста, предоставьте Ваш UID.

 (2) Пожалуйста, опишите цель/причины Вашей заявки и ожидаемый рост объема торгов.

 (3) Укажите лимит скорости API, который Вы запрашиваете.

Как только заявка будет принята, мы обработаем ее и ответим Вам в ближайшее время. Спасибо за Ваше терпение.




Restful API
===========

Рыночные данные
--------

#### <a ame="1"> Get Contract Info  </a> 

URL api/v1/contract_contract_info


| **Имя параметра** | **Тип** | **Обязательно** | **Описание** |
| ------------------ | -------- | ------------- | --------------- |

| symbol             | string   | false         | "BTC","ETH"...  |
| contract_type | string   | false      | "this_week","next_week", "quarter" |
| contract_code | string   | false      | BTC180914|


**Примечание**：
Примечание: Если есть номер в строке кода контракта, запрос с Contract_Code. Если нет номера, запрос по Символу + Тип Контракта. Необходимо выбрать одно из условий запроса.


**Параметр возврата**

| **Имя параметра**             | **Обязательно** | **Тип** | **Описание**                               | **Диапазон значений **                                              |
| ------------------------------ | ------------- | -------- | --------------------------------------------- | ------------------------------------------------------------ |
| status                         | true          | string   | Request Processing Result                     | "ok" , "error"                                               |
| \<list\>(Attribute Name: data) |               |          |                                               |                                                              |
| symbol                         | true          | string   | Product Code                                  | "BTC","ETH"...                                               |
| contract_code                  | true          | string   | Contract Code                                 | "BTC180914" ...                                              |
| contract_type                  | true          | string   | Contract Type                                 | "this_week","next_week", "quarter"                           |
| contract_size                  | true          | decimal  | Contract Value (USD of one contract)          | 10, 100...                                                   |
| price_tick                     | true          | decimal  | Minimum Variation of Contract Price           | 0.001, 0.01...                                               |
| delivery_date                  | true          | string   | Contract Delivery Date                        | eg "20180720"                                                |
| create_date                    | true          | string   | Contract Listing Date                         | eg "20180706"                                                |
| contract_status                | true          | int      | Contract Status                               | 0: Delisting,1: Listing,2: Pending Listing,3: Suspension,4: Suspending of Listing,5: In Settlement,6: Delivering,7: Settlement Completed,8: Delivered,9: Suspended Listing |
| \</list\>                      |               |          |                                               |                                                              |
| ts                             | true          | long     | Time of Respond Generation，Unit：Millisecond |                                                              |
**Пример**
```
ПОЛУЧИТЬ https://api.hbdm.com/api/v1/contract_contract_info

# Ответ

{
  "status": "ok",
  "data": [
    {
      "symbol": "BTC",
      "contract_code": "BTC180914",
      "contract_type": "this_week",
      "contract_size": 100,
      "price_tick": 0.001,
      "delivery_date": "20180704",
      "create_date": "20180604",
      "contract_status": 1
     }
    ],
  "ts":158797866555
}

```
#### <a name="2">Get Contract Index Price Information  </a>

URL  api/v1/contract_index

**Параметр запроса**

| **Parameter Name** | **Parameter Type** | **Mandatory** | **Desc**       |
| ------------------ | ------------------ | ------------- | -------------- |
| symbol             | string             | true          | "BTC","ETH"... |

**Параметр возврата**


| **Имя параметра**             | **Обязательно** | **Тип** | **Описание**                                      | **Диапазон значений** |
| ------------------------------ | ------------- | -------- | --------------------------------------------- | --------------- |
| status                         | true          | string   | Request Processing Result                     | "ok" , "error"  |
| \<list\>(Attribute Name: data) |               |          |                                               |                 |
| symbol                         | true          | string   | symbol                                        | "BTC","ETH"...  |
| index_price                    | true          | decimal  | Index Price                                   |                 |
| \</list\>                      |               |          |                                               |                 |
| ts                             | true          | long     | Time of Respond Generation，Unit：Millisecond |                 |

**Пример**

```
ПОЛУЧИТЬ https://api.hbdm.com/api/v1/contract_index?symbol=BTC

# Ответ
{
  "status":"ok",
  "data": [
     {
       "symbol": "BTC",
       "index_price":471.0817
      }
    ],
  "ts": 1490759594752
}
```
#### <a name="3">Contract Price Limitation</a>

URL api/v1/contract_price_limit

**Параметр запроса**

| **Имя параметра** | **Тип параметра** | **Обязательно** | **Описание**                                          |
| ------------------ | ------------------ | ------------- | ------------------------------------------------- |
| symbol             | string             | false         | "BTC","ETH"...                                    |
| contract_type      | string             | false         | Contract Type ("this_week","next_week","quarter") |
| contract_code      | string             | false         | BTC180914  ...                                    |

**Примечание**：
Примечание: Если есть номер в строке кода контракта, запрос с Contract_Code. Если нет номера, запрос по Символу + Тип Контракта. Необходимо выбрать одно из условий запроса.


**Параметр возврата**

| **Имя параметра**             | **Обязательно** | **Тип** | **Описание**                                      | **Диапазон значений**                   |
| ------------------------------ | ------------- | -------- | --------------------------------------------- | --------------------------------- |
| status                         | true          | string   | Request Processing Result                     | "ok" ,"error"                     |
| \<list\>(Attribute Name: data) |               |          |                                               |                                   |
| symbol                         | true          | string   | Variety code                                  | "BTC","ETH" ...                   |
| high_limit                     | true          | decimal  | Highest Buying Price                          |                                   |
| low_limit                      | true          | decimal  | Lowest Selling Price                          |                                   |
| contract_code                  | true          | string   | Contract Code                                 | eg "BTC180914"  ...               |
| contract_type                  | true          | string   | Contract Type                                 | "this_week","next_week","quarter" |
| \<list\>                       |               |          |                                               |                                   |
| ts                             | true          | long     | Time of Respond Generation, Unit: Millisecond |                                   |

**Пример**
```

ПОЛУЧИТЬ https://api.hbdm.com/api/v1/contract_price_limit?symbol=BTC&contract_type=this_week

# Ответить

{
  "status":"ok",
  "data": 
    {
      "symbol":"BTC",
      "high_limit":443.07,
      "low_limit":417.09,
      "contract_code":"BTC180914",
      "contract_type":"this_week"
     },
  "ts": 1490759594752
}
```
#### <a name="4">Get Contract Open Interest Information </a>

URL api/v1/contract_open_interest

**Параметр запроса**

| **Имя параметра** | **Тип параметра** | **Обязательно** | **Описание**                                          |
| ------------------ | ------------------ | ------------- | ------------------------------------------------- |
| symbol             | string             | false         | "BTC","ETH"...                                    |
| contract_type      | string             | false         | Contract Type ("this_week","next_week","quarter") |
| contract_code      | string             | false         | BTC180914                                         |
**Параметр возврата**


| **Имя параметра**             | **Обязательно** | **Тип** | **Описание**                                      | **Диапазон значений**                   |
| ------------------------------ | ------------- | -------- | --------------------------------------------- | --------------------------------- |
| status                         | true          | string   | Request Processing Result                     | "ok" , "error"                    |
| \<list\>(Attribute Name: data) |               |          |                                               |                                   |
| symbol                         | true          | string   | Variety code                                  | "BTC", "ETH" ...                  |
| contract_type                  | true          | string   | Contract Type                                 | "this_week","next_week","quarter" |
| volume                         | true          | decimal  | Position quantity(amount)                     |                                   |
| amount                         | true          | decimal  | Position quantity(Currency)                   |                                   |
| contract_code                  | true          | string   | Contract Code                                 | eg "BTC180914"   ...              |
| \</list\>                      |               |          |                                               |                                   |
| ts                             | true          | long     | Time of Respond Generation, Unit: Millisecond |                                   |

**Пример**

```
ПОЛУЧИТЬ https://api.hbdm.com/api/v1/contract_open_interest?symbol=BTC&contract_type=this_week

# Ответ

{
  "status":"ok",
  "data":
    {
      "symbol":"BTC",
      "contract_type": "this_week",
      "volume":123,
      "amount":106,
      "contract_code": "BTC180914"
     },
  "ts": 1490759594752
}
```
#### <a name="5">Get Market Depth</a>

URL /рынок/глубина


**Параметр запроса**


| **Имя параметра** | **Тип параметра** | **Обязательно** | **Описание**                                                     |
| ------------------ | ------------------ | ------------- | ------------------------------------------------------------ |
| symbol             | string             | true          | e.g. "BTC_CQ" represents BTC “This Week”，"BTC_CQ" represents BTC “Next Week”，"BTC_CQ" represents BTC “Quarter” |
| type               | string             | true          | step0, step1, step2, step3, step4, step5（merged deep data 0-5）；when step is 0，deep data not merged |

**Параметр возврата**

| **Имя параметра** | **Обязательно** | **Тип данных** | **Описание**                                                     | **Диапазон значений** |
| ------------------ | ------------- | ------------- | ------------------------------------------------------------ | --------------- |
| ch                 | true          | string        | Data belonged channel，Format： market.period                |                 |
| status             | true          | string        | Request Processing Result                                    | "ok" , "error"  |
| asks               | true          | object        | Selling, [price(hanging unit Price), vol(this price represent single contract)], According to the ascending order of Price |                 |
| bids               | true          | object        | Buying, [price(hanging unit price), vol(this price represent single contract)], According to the descending order of Price |                 |
| ts                 | true          | number        | Time of Respond Generation，Unit：Millisecond                |                 |
```
Пример отметки:

"tick": {
    "id": id сообщения.
    "ts": Время создания сообщения, единица: миллисекунда
    "bids": покупка, [цена(подвешенная цена за единицу), объем(эта цена представляет единственный контракт)], по убыванию цены
    "asks": Selling, [цена(подвешенная цена за единицу), объем(эта цена представляет единственный контракт)], по возрастанию цены
    }


```

**Пример**

```
ПОЛУЧИТЬ https://api.hbdm.com/market/depth?symbol=BTC_CQ&type=step5


# Ответ

{
  "ch":"market.BTC_CQ.depth.step5",
  "status":"ok",
    "tick":{
      "asks":[
        [6580,3000],
        [70000,100]
        ],
      "bids":[
        [10,3],
        [2,1]
        ],
      "ch":"market.BTC_CQ.depth.step5",
      "id":1536980854,
      "mrid":6903717,
      "ts":1536980854171,
      "version":1536980854
    },
  "ts":1536980854585
}
```
#### <a name="6">Get K-Line Data</a>

URL
/рынок/история/kline


**Параметр запроса**

| **Имя параметра** | **Обязательно** | **Тип** | **Описание**             | **Значение по умолчанию** | **Диапазон значений**                                              |
| ------------------ | ------------- | -------- | -------------------- | ----------- | ------------------------------------------------------------ |
| symbol             | true          | string   | Contract Name        |             | e.g. "BTC_CQ" represents BTC “This Week”，"BTC_CQ" represents BTC “Next Week”，"BTC_CQ" represents BTC “Quarter” |
| period             | true          | string   | K-Line Type          |             | 1min, 5min, 15min, 30min, 60min, 1hour,4hour,1day, 1mon      |
| size               | false         | integer  | Acquisition Quantity | 150         | [1,2000]                                                     |

**Параметр возврата**


| **Имя параметра** | **Обязательно** | **Тип данных ** | **Описание**                                      | **Диапозон значений** |
| ------------------ | ------------- | ------------- | --------------------------------------------- | --------------- |
| ch                 | true          | string        | Data belonged channel，Format： market.period |                 |
| data               | true          | object        | KLine Data                                    |                 |
| status             | true          | string        | Request Processing Result                     | "ok" , "error"  |
| ts                 | true          | number        | Time of Respond Generation, Unit: Millisecond |                 |

Пример данных:
```
"data": [
  {
        "id": K-Line id,
        "vol": Transaction Volume(amount),
        "count": transaction count
        "open": opening Price
        "close": Closing Price, when the K-line is the latest one，it means the latest price
        "low": Lowest price
        "high": highest price
        "amount": transaction volume(currency), sum(every transaction volume(amount)*every contract value/transaction price for this contract)
   }
]
```
**Пример**

```
ПОЛУЧИТЬ  https://api.hbdm.com/market/history/kline?period=1min&size=200&symbol=BTC_CQ


# Ответ

{
  "ch": "market.BTC_CQ.kline.1min",
  "data": [
    {
      "vol": 2446,
      "close": 5000,
      "count": 2446,
      "high": 5000,
      "id": 1529898120,
      "low": 5000,
      "open": 5000,
      "amount": 48.92
     },
    {
      "vol": 0,
      "close": 5000,
      "count": 0,
      "high": 5000,
      "id": 1529898780,
      "low": 5000,
      "open": 5000,
      "amount": 0
     }
   ],
  "status": "ok",
  "ts": 1529908345313
}


```
####  <a name="7">Get Market Data Overview</a>

URL
/рынок/детали/слияние


**Параметр запроса**


| **Имя параметра** | **Обязательно** | **Тип** | **Описание**      | **Значение по умолчанию** | **Диапазон значений**                                              |
| ------------------ | ------------- | -------- | ------------- | ----------- | ------------------------------------------------------------ |
| symbol             | true          | string   | Contract Name |             | e.g. "BTC_CQ" represents BTC “This Week”，"BTC_CQ" represents BTC “Next Week”，"BTC_CQ" represents BTC “Quarter” |

**Параметр возврата**

| **Имя параметра** | **Обязательно** | **Тип данных** | **Описание**                                                     | **Диапазон значений** |
| ------------------ | ------------- | ------------- | ------------------------------------------------------------ | --------------- |
| ch                 | true          | string        | Data belonged channel，format： market.$symbol.detail.merged |                 |
| status             | true          | string        | Request Processing Result                                    | "ok" , "error"  |
| tick               | true          | object        | K-Line Data                                                  |                 |
| ts                 | true          | number        | Time of Respond Generation, Unit: Millisecond                |                 |

Пример отметки
```
"tick": {
    "id": K-Line id,
    "vol": объем транзакций (контракт),
    "count": счетчик транзакций
    "open": цена открытия,
    "close": Цена закрытия, когда Kline последняя, цена - последняя 
        "low": Самая низкая цена
        "high": Самая высокая цена
        "amount": объем транзакций(валюта), сумма(объем каждой транзакции(количество)*значение каждого контракта/цена транзакции для этого котракта)
    "bid": [цена покупки (количество)],
    "ask": [цена продажи (количество)]


  }
```
**Пример**

```
ПОЛУЧИТЬ  https://api.hbdm.com/market/detail/merged?symbol=BTC_CQ 


# Ответ

{
  "ch": "market.BTC_CQ.detail.merged",
  "status": "ok",
  "tick": 
    {
      "vol":"13305",
      "ask": [5001, 2],
      "bid": [5000, 1],
      "close": "5000",
      "count": "13305",
      "high": "5000",
      "id": 1529387841,
      "low": "5000",
      "open": "5000",
      "ts": 1529387842137,
      "amount": "266.1"
     },
  "ts": 1529387842137
}
```
#### <a name="8">The Last Trade of a Contract</a>

URL /рынок/торговля
**Параметр запроса**

| **Имя параметра** | **Обязательно** | **Тип** | **Описание**      | **Значение по умолчанию** | **Диапазон значений**                                              |
| ------------------ | ------------- | -------- | ------------- | ----------- | ------------------------------------------------------------ |
| symbol             | true          | string   | Contract Name |             | e.g. "BTC_CQ" represents BTC “This Week”，"BTC_CQ" represents BTC “Next Week”，"BTC_CQ" represents BTC “Quarter” |

**Параметр возврата**


| **Имя параметра** | **Обязательно** | **Тип** | **Описание**                                                    | **Значение по умолчанию** | **Диапазон значений** |
| ------------------ | ------------- | -------- | ----------------------------------------------------------- | ----------- | --------------- |
| ch                 | true          | string   | Data belonged channel，Format： market.$symbol.trade.detail |             |                 |
| status             | true          | string   |                                                             |             | "ok","error"    |
| tick               | true          | object   | Trade Data                                                  |             |                 |
| ts                 | true          | number   | Sending time                                                |             |                 |

Пример отметки:
```
"tick": {

  "id": id сообщения,
  "ts": Время последней транзакции,
  "data": [
    {
      "id": id транзакции,
      "price": цена транзакции,
      "amount": количество транзакций,
      "direction": направление активных транзакций      
"ts": время транзакций


    }
  ]
}
```

**Пример**

```
ПОЛУЧИТЬ  https://api.hbdm.com/market/trade?symbol=BTC_CQ


# Ответ

{
  "ch": "market.BTC_CQ.trade.detail",
  "status": "ok",
  "tick": {
    "data": [
      {
        "amount": "1",
        "direction": "sell",
        "id": 6010881529486944176,
        "price": "5000",
        "ts": 1529386945343
       }
     ],
    "id": 1529388202797,
    "ts": 1529388202797
    },
  "ts": 1529388202797
}
```
#### <a name="9">Request a Batch of Trade Records of a Contract</a>

URL /рынок/история/торговля


**Параметр запроса**

| **Имя параметра** | **Обязательство** | **Тип данных** | **Описание**                              | **Значение по умолчанию** | **Диапазон значений**                                              |
| ------------------ | ------------- | ------------- | ------------------------------------- | ----------- | ------------------------------------------------------------ |
| symbol             | true          | string        | Contract Name                         |             | e.g. "BTC_CQ" represents BTC “This Week”，"BTC_CQ" represents BTC “Next Week”，"BTC_CQ" represents BTC “Quarter” |
| size               | false         | number        | Number of Trading Records Acquisition | 1           | [1, 2000]                                                    |

**Параметр возврата**

| **Имя параметра** | **Обязательно** | **Тип данных** | **Описание**                                                    | **Диапазон значений** |
| ------------------ | ------------- | ------------- | ----------------------------------------------------------- | --------------- |
| ch                 | true          | string        | Data belonged channel，Format： market.$symbol.trade.detail |                 |
| data               | true          | object        | Trade Data                                                  |                 |
| status             | true          | string        |                                                             | "ok"，"error"   |
| ts                 | true          | number        | Time of Respond Generation, Unit: Millisecond               |                 |

Пример данных:
```
"data": {

  "id": id сообщения,
  "ts": Время последней транзакции,
  "data": [
    {
      "id": id транзакции,
      "price": цена транзакции,
      "amount": транзакция (количество),
      "direction": направление активных транзакций
      "ts": время транзакций

      }
}
```


**Пример**

```
ПОЛУЧИТЬ  https://api.hbdm.com/market/history/trade?symbol=BTC_CQ&size=100 


# Ответ

{
  "ch": "market.BTC_CQ.trade.detail",
  "status": "ok",
  "ts": 1529388050915,
  "data": [
    {
      "id": 601088,
      "ts": 1529386945343,
      "data": [
        {
         "amount": 1,
         "direction": "sell",
         "id": 6010881529486944176,
         "price": 5000,
         "ts": 1529386945343
         }
       ]
    }
   ]
}

```

Интерфейс учетной записи
--------

#### <a name="101">User’s Account Information</a>

URL  api/v1/contract_account_info 

**Параметр запроса**

| **Имя параметра** | **Обязательно** | **Тип** | **Описание**     | **Значение по умолчанию** | **Диапазон значений**                                         |
| ------------------ | ------------- | -------- | ------------ | ----------- | ------------------------------------------------------- |
| symbol             | false         | string   | Variety code |             | "BTC","ETH"...if default, return to all types defaulted |

**Параметр возврата**

| **Имя параметра** | **Обязательно** | **Тип** | **Описание**     | **Диапазон значений**                                      |
| ------------------------------ | ------------- | -------- | --------------------------------------------- | --------------- |
| status                         | true          | string   | Request Processing Result                     | "ok" , "error"  |
| \<list\>(Attribute Name: data) |               |          |                                               |                 |
| symbol                         | true          | string   | Variety code                                  | "BTC","ETH"...  |
| margin_balance                 | true          | decimal  | Account rights                                |                 |
| margin_position                | true          | decimal  | Position Margin                               |                 |
| margin_frozen                  | true          | decimal  | Freeze margin                                 |                 |
| margin_available               | true          | decimal  | Available margin                              |                 |
| profit_real                    | true          | decimal  | Realized profit                               |                 |
| profit_unreal                  | true          | decimal  | Unrealized profit                             |                 |
| risk_rate                      | true          | decimal  | risk rate                                     |                 |
| liquidation_price              | true          | decimal  | Estimated liquidation price                   |                 |
| withdraw_available             | true          | decimal  | Available withdrawal                          |                 |
| lever_rate                     | true          | decimal  | Leverage Rate                                 |                 |
| \</list\>                      |               |          |                                               |                 |
| ts                             | number        | long     | Time of Respond Generation, Unit: Millisecond |                 |

**Пример**

```
ОТПРАВИТЬ https://api.hbdm.com/api/v1/contract_account_info    


# Ответ

{
  "status": "ok",
  "data": [
    {
      "symbol": "BTC",
      "margin_balance": 1,
      "margin_position": 0,
      "margin_frozen": 3.33,
      "margin_available": 0.34,
      "profit_real": 3.45,
      "profit_unreal": 7.45,
      "withdraw_available":4.0989898,
      "risk_rate": 100,
      "liquidation_price": 100
     },
    {
      "symbol": "ETH",
      "margin_balance": 1,
      "margin_position": 0,
      "margin_frozen": 3.33,
      "margin_available": 0.34,
      "profit_real": 3.45,
      "profit_unreal": 7.45,
      "withdraw_available":4.7389859,
      "risk_rate": 100,
      "liquidation_price": 100
     }
   ],
  "ts":158797866555
}

```
#### <a name="102">User’s position Information </a>

URL api/v1/contract_position_info

**Параметр запроса**


| **Имя параметра** | **Обязательно** | **Тип** | **Описание**     | **Значение по умолчению** | **Диапазон значений**                                         |
| ------------------ | ------------- | -------- | ------------ | ----------- | ------------------------------------------------------- |
| symbol             | false         | string   | Variety code |             | "BTC","ETH"...if default, return to all types defaulted |

**Параметр возврата**

| **Имя параметра** | **Обязательно** | **Тип** | **Описание**     | **Диапазон значений**                                         |

| ------------------------------ | ------------- | -------- | --------------------------------------------- | ----------------------------------- |
| status                         | true          | string   | Request Processing Result                     | "ok" , "error"                      |
| \<list\>(Attribute Name: data) |               |          |                                               |                                     |
| symbol                         | true          | string   | Variety code                                  | "BTC","ETH"...                      |
| contract_code                  | true          | string   | Contract Code                                 | "BTC180914" ...                     |
| contract_type                  | true          | string   | Contract Type                                 | "this_week", "next_week", "quarter" |
| volume                         | true          | decimal  | Position quantity                             |                                     |
| available                      | true          | decimal  | Available position can be closed              |                                     |
| frozen                         | true          | decimal  | frozen                                        |                                     |
| cost_open                      | true          | decimal  | Opening average price                         |                                     |
| cost_hold                      | true          | decimal  | Average price of position                     |                                     |
| profit_unreal                  | true          | decimal  | Unrealized profit and loss                    |                                     |
| profit_rate                    | true          | decimal  | Profit rate                                   |                                     |
| profit                         | true          | decimal  | profit                                        |                                     |
| position_margin                | true          | decimal  | Position margin                               |                                     |
| lever_rate                     | true          | int      | Leverage rate                                 |                                     |
| direction                      | true          | string   | Transaction direction                         |                                     |
| \</list\>                      |               |          |                                               |                                     |
| ts                             | true          | long     | Time of Respond Generation, Unit: Millisecond |                                     |

**Пример**

```
ОТПРАВИТЬ  https://api.hbdm.com/api/v1/contract_position_info 


# Ответ

{
  "status": "ok",
  "data": [
    {
      "symbol": "BTC",
      "contract_code": "BTC180914",
      "contract_type": "this_week",
      "volume": 1,
      "available": 0,
      "frozen": 0.3,
      "cost_open": 422.78,
      "cost_hold": 422.78,
      "profit_unreal": 0.00007096,
      "profit_rate": 0.07,
      "profit": 0.97,
      "position_margin": 3.4,
      "lever_rate": 10,
      "direction":"buy"
     }
    ],
 "ts": 158797866555
}
```


Торговый интерфейс
--------

#### <a name="103"> Place an Order </a>

URL api/v1/contract_order

**Параметр запроса**


| **Имя параметра** | **Тип параметра** | **Обязательно** | **Описание**     | 

| ------------------ | ------------------ | ------------- | ------------------------------------------------------------ |
| symbol             | string             | false         | "BTC","ETH"...                                               |
| contract_type      | string             | false         | Contract Type ("this_week": "next_week": "quarter":)         |
| contract_code      | string             | false         | BTC180914                                                    |
| client_order_id    | long               | false         | Clients fill and maintain themselves, and this time must be greater than last time |
| price              | decimal            | true          | Price                                                        |
| volume             | long               | true          | Numbers of orders (amount)                                   |
| direction          | string             | true          | Transaction direction                                        |
| offset             | string             | true          | "open", "close"                                              |
| lever_rate         | int                | true          | Leverage rate [if“Open”is multiple orders in 10 rate, there will be not multiple orders in 20 rate |
| order_price_type   | string             | true          | "limit", "opponent"                                          |

**Примечание**：
Примечание: Если есть номер в строке кода контракта, запрос с Contract_Code. Если нет номера, запрос по Символу + Тип Контракта. 


**Параметр возврата**


| **Имя параметра** | **Обязательно** | **Тип** | **Описание**                                                     | **Диапазон значений** |

| ------------------ | ------------- | -------- | ------------------------------------------------------------ | --------------- |
| status             | true          | string   | Request Processing Result                                    | "ok" , "error"  |
| order_id           | true          | long     | Order ID                                                     |                 |
| client_order_id    | true          | long     | the client ID that is filled in when the order is placed, if it’s not filled, it won’t be returned |                 |
| ts                 | true          | long     | Time of Respond Generation, Unit: Millisecond                |                 |

**Пример**

```
ОТПРАВИТЬ  https://api.hbdm.com/api/v1/contract_order 


# Отправить

{
  "status": "ok",
  "order_id": 986,
  "client_order_id": 9086,
  "ts": 158797866555
}
```
#### <a name="104"> Place a Batch of Orders</a>

URL /v1/contract_batchorder
**Параметр запроса**


| **Имя параметра**                    | **Тип параметра** | **Обязательно** | **Описание**                                                     |

| ------------------------------------- | ------------------ | ------------- | ------------------------------------------------------------ |
| \<list\>(Attribute Name: orders_data) |                    |               |                                                              |
| symbol                                | string             | false         | "BTC","ETH"...                                               |
| contract_type                         | string             | false         | Contract Type: "this_week": "next_week": "quarter":          |
| contract_code                         | string             | false         | BTC180914                                                    |
| client_order_id                       | long               | true          | Clients fill and maintain themselves, and this time must be greater than last time |
| price                                 | decimal            | true          | Price                                                        |
| volume                                | long               | true          | Numbers of orders (amount)                                   |
| direction                             | string             | true          | Transaction direction                                        |
| offset                                | string             | true          | "open": "close"                                              |
| lever_rate                            | int                | true          | Leverage rate [if“Open”is multiple orders in 10 rate, there will be not multiple orders in 20 rate |
| order_price_type                      | string             | true          | "limit":   "opponent"                                        |
| \</list\>                             |                    |               |                                                              |

**Примечание**: Если есть номер в строке кода контракта, запрос с Contract_Code. Если нет номера, запрос по Символу + Тип Контракта

**Параметр возврата**


| **Имя параметра**                | **Обязательно** | **Тип** | **Описание**                                                     | **Диапазон цен** |

| --------------------------------- | ------------- | -------- | ------------------------------------------------------------ | --------------- |
| status                            | true          | string   | Request Processing Result                                    | "ok" , "error"  |
| \<list\>(Attribute Name: errors)  |               |          |                                                              |                 |
| index                             | true          | int      | order Index                                                  |                 |
| err_code                          | true          | int      | Error code                                                   |                 |
| err_msg                           | true          | string   | Error information                                            |                 |
| \</list\>                         |               |          |                                                              |                 |
| \<list\>(Attribute Name: success) |               |          |                                                              |                 |
| index                             | true          | int      | order Index                                                  |                 |
| order_id                          | true          | long     | Order ID                                                     |                 |
| client_order_id                   | true          | long     | the client ID that is filled in when the order is placed, if it’s not filled, it won’t be returned |                 |
| \</list\>                         |               |          |                                                              |                 |
| ts                                | true          | long     | Time of Respond Generation, Unit: Millisecond                |                 |

**Пример**

```
ОТПРАВИТЬ  https://api.hbdm.com/api/v1/contract_batchorder 


# Ответ

{
  "status": "ok",
  "data": {
    "errors":[
      {
        "index":0,
        "err_code": 200417,
        "err_msg": "invalid symbol"
       },
      {
        "index":3,
        "err_code": 200415,
        "err_msg": "invalid symbol"
       }
     ],
    "success":[
      {
        "index":1,
        "order_id":161256,
        "client_order_id":1344567
       },
      {
        "index":2,
        "order_id":161257,
        "client_order_id":1344569
       }
     ]
   },
  "ts": 1490759594752
}
```
#### <a name="105">Cancel an Order </a>

URL api/v1/contract_cancel

**Параметр запроса**


| **Parameter Name** | **Mandatory** | **Type** | **Desc**                                                     |
| ------------------ | ------------- | -------- | ------------------------------------------------------------ |
| order_id           | false         | string   | Order ID（different IDs are separated by ",", maximum 50 orders can be withdrew at one time） |
| client_order_id    | false         | string   | Client order ID (different IDs are separated by ",", maximum 50 orders can be withdrew at one time) |
| symbol             | true          | string   | "BTC","ETH"...                                               |

**Примечание**：
Как order_id, так и client_order_id могут быть использованы для вывода ордера, нужен один из них. Если установлены оба по умолчанию будет order_id.

**Параметр возврата**

| **Имя параметра**               | **Обязательно** | **Тип** | **Описание**                                                  | **Диапазон значений** |
| -------------------------------- | ------------- | -------- | --------------------------------------------------------- | --------------- |
| status                           | true          | string   | Request Processing Result                                 | "ok" , "error"  |
| \<list\>(Attribute Name: errors) |               |          |                                                           |                 |
| order_id                         | true          | string   | Order ID                                                  |                 |
| err_code                         | true          | int      | Error code                                                |                 |
| err_msg                          | true          | string   | Error information                                         |                 |
| \</list\>                        |               |          |                                                           |                 |
| successes                        | true          | string   | Successfully withdrew list of order_id or client_order_id |                 |
| ts                               | true          | long     | Time of Respond Generation, Unit: Millisecond             |                 |

**Пример**

```
ОТПРАВИТЬ  https://api.hbdm.com.com/api/v1/contract_cancel 


# Ответ

# результат многократных выводов ордера (успешно выведенный order ID, ошибка вывода order ID)
{
  "status": "ok",
  "errors":[
    {
      "order_id":161251,
      "err_code": "1002",
      "err_msg": "order doesn’t exist"
     },
    {
      "order_id":161253,
      "err_code": "1002",
      "err_msg": "order doesn’t exist"
     }
   ],
  "success":["161256","1344567"],
  "ts": 1490759594752
}
```
#### <a name="106">Cancel All Orders </a>

URL api/v1/contract_cancelall

**Параметр запроса**


| **Parameter Name** | **Mandatory** | **Type** | **Desc**                        |
| ------------------ | ------------- | -------- | ------------------------------- |
| symbol             | true          | string   | Variety code，eg "BTC","ETH"... |

**Параметр возврата**


| **Parameter Name**               | **Mandatory** | **Type** | **Desc**                                      | **Value Range** |
| -------------------------------- | ------------- | -------- | --------------------------------------------- | --------------- |
| status                           | true          | string   | Request Processing Result                     | "ok" , "error"  |
| successes                        | true          | string   | Successful order                              |                 |
| \<list\>(Attribute Name: errors) |               |          |                                               |                 |
| order_id                         | true          | String   | Order ID                                      |                 |
| err_code                         | true          | int      | failed order error messageError code          |                 |
| err_msg                          | true          | int      | failed order information                      |                 |
| \</list\>                        |               |          |                                               |                 |
| successes                        | true          | string   | Successful order                              |                 |
| ts                               | true          | long     | Time of Respond Generation, Unit: Millisecond |                 |

**Пример**

```
ОТПРАВИТЬ  https://api.hbdm.com.com/api/v1/contract_cancel        
 

# Отправить

{
 "symbol": "BTC"
}


# Ответ
# результат многократных выводов ордера (успешно выведенный order ID, ошибка вывода order ID)

{
  "status": "ok",
  "data": {
    "errors":[
      {
        "order_id":"161251",
        "err_code": 200417,
        "err_msg": "invalid symbol"
       },
      {
        "order_id":161253,
        "err_code": 200415,
        "err_msg": "invalid symbol"
       }
      ],
    "successes":[161256,1344567]
   },
  "ts": 1490759594752
}
Error：
{
  "status": "error",
  "err_code": 20012,
  "err_msg": "invalid symbol",
  "ts": 1490759594752
}
```
#### <a name="107">Get Information of an Order </a>

URL api/v1/contract_order_info

**Параметр запроса**


| **Имя параметра** | **Обязательно** | **Тип** | **Описание**                                                     |
| ------------------ | ------------- | -------- | ------------------------------------------------------------ |
| order_id           | false         | string   | Order ID（different IDs are separated by ",", maximum 20 orders can be withdrew at one time） |
| client_order_id    | false         | string   | Client order ID Order ID（different IDs are separated by ",", maximum 20 orders can be withdrew at one time) |
| symbol             | true          | string   | "BTC","ETH"...                                               |

**Примечание**：Как order_id, так и client_order_id могут быть использованы для вывода ордера, нужен один из них. Если установлены оба по умолчанию будет order_id.


**Параметр возврата**

| **Имя параметра** | **Обязательно** | **Тип** | **Описание**                                                     | **Диапазон значений**                     |
| ------------------------------ | ------------- | -------- | ------------------------------------------------------------ | ----------------------------------- |
| status                         | true          | string   | Request Processing Result                                    | "ok" , "error"                      |
| \<list\>(Attribute Name: data) |               |          |                                                              |                                     |
| symbol                         | true          | string   | Variety code                                                 |                                     |
| contract_type                  | true          | string   | Contract Type                                                | "this_week", "next_week", "quarter" |
| contract_code                  | true          | string   | Contract Code                                                | "BTC180914" ...                     |
| volume                         | true          | decimal  | Numbers of order                                             |                                     |
| price                          | true          | decimal  | Price committed                                              |                                     |
| order_price_type               | true          | string   | Order price type [limited price，opponent price，market price] |                                     |
| direction                      | true          | string   | Transaction direction                                        |                                     |
| offset                         | true          | string   | "open": "close"                                              |                                     |
| lever_rate                     | true          | int      | Leverage rate                                                | 1\\5\\10\\20                        |
| order_id                       | true          | long     | Order ID                                                     |                                     |
| client_order_id                | true          | long     | Client order ID                                              |                                     |
| created_at                     | true          | long     | Transaction time                                             |                                     |
| trade_volume                   | true          | decimal  | Transaction quantity                                         |                                     |
| trade_turnover                 | true          | decimal  | Transaction aggregate amount                                 |                                     |
| fee                            | true          | decimal  | Servicefee                                                   |                                     |
| trade_avg_price                | true          | decimal  | Transaction average price                                    |                                     |
| margin_frozen                  | true          | decimal  | Freeze margin                                                |                                     |
| profit                         | true          | decimal  | profit                                                       |                                     |
| status                         | true          | int      | Order status (1ready to submit 2ordered 3submitted 4partially transacted 5partially withdrew 6all transacted 7withdrew 11withdrawing) |                                     |
| order_source                   | true          | string   | Order source（1:system order、2:web page order、3:API order、4:APP order 5liquidation source、6delivery source） |                                     |
| \</list\>                      |               |          |                                                              |                                     |
| ts                             | true          | long     | Timestamp                                                    |                                     |

**Пример**

```
ОТПРАВИТЬ  https://api.hbdm.com.com/api/v1/contract_order_info 


# Ответ

{
  "status": "ok",
  "data":[
    {
      "symbol": "BTC",
      "contract_type": "this_week",
      "contract_code": "BTC180914",
      "volume": 111,
      "price": 1111,
      "order_price_type": "limit",
      "direction": "buy",
      "offset": "open",
      "lever_rate": 10,
      "order_id": 106837,
      "client_order_id": 10683,
      "order_source": "web",
      "created_at": 1408076414000,
      "trade_volume": 1,
      "trade_turnover": 1200,
      "fee": 0,
      "trade_avg_price": 10,
      "margin_frozen": 10,
      "profit ": 10,
      "status": 0
     },
    {
      "symbol": "ETH",
      "contract_type": "this_week",
      "contract_code": "ETH180921",
      "volume": 111,
      "price": 1111,
      "order_price_type": "limit",
      "direction": "buy",
      "offset": "open",
      "lever_rate": 10,
      "order_id": 106837,
      "client_order_id": 10683,
      "order_source": "web",
      "created_at": 1408076414000,
      "trade_volume": 1,
      "trade_turnover": 1200,
      "fee": 0,
      "trade_avg_price": 10,
      "margin_frozen": 10,
      "profit ": 10,
      "status": 0
     }
    ],
  "ts": 1490759594752
}
```
#### <a name="108">Order details acquisition </a>

URL api/v1/contract_order_detail

**Параметр запроса**


| **Имя параметра** | **Обязательно** | **Тип** | **Описание**                      |
| ------------------ | ------------- | -------- | ----------------------------- |
| symbol             | true          | string   | "BTC","ETH"...                |
| order_id           | true          | long     | Order ID                      |
| createAt           | true          | long     | Timestamp                     |
| page_index         | false         | int      | Page number, default 1st page |
| page_size          | false         | int      | Default 20，no more than 50   |

**Параметр возврата**


| **Имя параметра**                | **Обязательно** | **Тип** | **Описание**                                                     | **Диапазон значений**                   |
| --------------------------------- | ------------- | -------- | ------------------------------------------------------------ | --------------------------------- |
| status                            | true          | string   | Request Processing Result                                    | "ok" , "error"                    |
| \<object\> (Attribute Name: data) |               |          |                                                              |                                   |
| symbol                            | true          | string   | Variety code                                                 |                                   |
| contract_type                     | true          | string   | Contract Type                                                | "this_week","next_week","quarter" |
| contract_code                     | true          | string   | Contract Code                                                | "BTC180914" ...                   |
| lever_rate                        | true          | int      | Leverage Rate                                                | 1\\5\\10\\20                      |
| direction                         | true          | string   | Transaction direction                                        |                                   |
| offset                            | true          | string   | "open": "close"                                              |                                   |
| volume                            | true          | decimal  | Number of Order                                              |                                   |
| price                             | true          | decimal  | Price committed                                              |                                   |
| created_at                        | true          | long     | Transaction time                                             |                                   |
| order_source                      | true          | string   | Order Source                                                 |                                   |
| order_price_type                  | true          | string   | Order price type [limited price，opponent price，market price] |                                   |
| margin_frozen                     | true          | decimal  | Freeze margin                                                |                                   |
| profit                            | true          | decimal  | profit                                                       |                                   |
| total_page                        | true          | int      | Page in total                                                |                                   |
| current_page                      | true          | int      | Current Page                                                 |                                   |
| total_size                        | true          | int      | Total Size                                                   |                                   |
| \<list\> (Attribute Name: trades) |               |          |                                                              |                                   |
| trade_id                          | true          | long     | Match Result id                                              |                                   |
| trade_price                       | true          | decimal  | Match Price                                                  |                                   |
| trade_volume                      | true          | decimal  | Transaction quantity                                         |                                   |
| trade_turnover                    | true          | decimal  | Transaction price                                            |                                   |
| trade_fee                         | true          | decimal  | Transaction Service fee                                      |                                   |
| created_at                        | true          | long     | Creation time                                                |                                   |
| \</list\>                         |               |          |                                                              |                                   |
| \</object \>                      |               |          |                                                              |                                   |
| ts                                | true          | long     | Timestamp                                                    |                                   |

**Пример**

```
ОТПРАВИТЬ  https://api.hbdm.com/api/v1/contract_order_detail 


# Ответ

{
  "status": "ok",
  "data":{
    "symbol": "BTC",
    "contract_type": "this_week",
    "contract_code": "BTC180914",
    "volume": 111,
    "price": 1111,
    "order_price_type": "limit",
    "direction": "buy",
    "offset": "open",
    "status": 1,
    "lever_rate": 10,
    "trade_avg_price": 10,
    "margin_frozen": 10,
    "profit": 10,
    "order_id": 106837,
    "order_source": "web",
    "created_at": 1408076414000,
    "trades":[
      {
        "trade_id":112,
        "trade_volume":1,
        "trade_price":123.4555,
        "trade_fee":0.234,
        "trade_turnover":34.123,
        "created_at": 1490759594752
       }
      ],
    "total_page":15,
    "total_size":3,
    "current_page":3
    },
  "ts": 1490759594752
}
Error:
{
 "status":"error",
 "err_code":20029,
 "err_msg": "invalid symbol",
 "ts": 1490759594752
}
```
#### <a name="109">Current unfilled commission acquisition </a>

URL  api/v1/contract_openorders

**Параметр запроса**


| **Имя параметра** | **Обязательно** | **Тип** | **Описание**                    | **Значение по умолчанию** | **Диапазон значений** |
| ------------------ | ------------- | -------- | --------------------------- | ----------- | --------------- |
| symbol             | false         | string   | Variety code                |             | "BTC","ETH"...  |
| page_index         | false         | int      | Page, default 1st page      | 1           |                 |
| page_size          | false         | int      | Default 20，no more than 50 | 20          |                 |

**Параметр возврата**


| **Имя параметра**             | **Обязательно** | **Тип** | **Описание**                                                     | **Диапазон значений**                   |
| ------------------------------ | ------------- | -------- | ------------------------------------------------------------ | --------------------------------- |
| status                         | true          | string   | Request Processing Result                                    |                                   |
| \<list\>(Attribute Name: data) |               |          |                                                              |                                   |
| symbol                         | true          | string   | Variety code                                                 |                                   |
| contract_type                  | true          | string   | Contract Type                                                | "this_week","next_week","quarter" |
| contract_code                  | true          | string   | Contract Code                                                | "BTC180914" ...                   |
| volume                         | true          | decimal  | Number of Order                                              |                                   |
| price                          | true          | decimal  | Price committed                                              |                                   |
| order_price_type               | true          | string   | Order price type [limited price，opponent price，market price] |                                   |
| direction                      | true          | string   | Transaction direction                                        |                                   |
| offset                         | true          | string   | "open": "close"                                              |                                   |
| lever_rate                     | true          | int      | Leverage Rate                                                | 1\\5\\10\\20                      |
| order_id                       | true          | long     | Order ID                                                     |                                   |
| client_order_id                | true          | long     | Client order ID                                              |                                   |
| created_at                     | true          | long     | Order Creation time                                          |                                   |
| trade_volume                   | true          | decimal  | Transaction quantity                                         |                                   |
| trade_turnover                 | true          | decimal  | Transaction aggregate amount                                 |                                   |
| fee                            | true          | decimal  | Servicefee                                                   |                                   |
| trade_avg_price                | true          | decimal  | Transaction average price                                    |                                   |
| margin_frozen                  | true          | decimal  | Freeze margin                                                |                                   |
| profit                         | true          | decimal  | profit                                                       |                                   |
| status                         | true          | int      | Order status (3didn’t transact 4partially transacted 5partially withdrew 6all transacted 7withdrew) |                                   |
| order_source                   | true          | string   | Order Source                                                 |                                   |
| \</list\>                      |               |          |                                                              |                                   |
| total_page                     | true          | int      | Total Pages                                                  |                                   |
| current_page                   | true          | int      | Current Page                                                 |                                   |
| total_size                     | true          | int      | Total Size                                                   |                                   |
| ts                             | true          | long     | Timestamp                                                    |                                   |

**Пример**

```
ОТПРАВИТЬ https://www.hbdm.com/api/v1/contract_openorders

# Ответ

{
  "status": "ok",
  "data":{
    "orders":[
      {
         "symbol": "BTC",
         "contract_type": "this_week",
         "contract_code": "BTC180914",
         "volume": 111,
         "price": 1111,
         "order_price_type": "limit",
         "direction": "buy",
         "offset": "open",
         "lever_rate": 10,
         "order_id": 106837,
         "client_order_id": 10683,
         "order_source": "web",
         "created_at": 1408076414000,
         "trade_volume": 1,
         "trade_turnover": 1200,
         "fee": 0,
         "trade_avg_price": 10,
         "margin_frozen": 10,
         "status": 1
        }
       ],
    "total_page":15,
    "current_page":3,
    "total_size":3
   },
  "ts": 1490759594752
}
```
#### <a name="110">Get History Orders</a>

URL api/v1/contract_hisorders

**Параметр запроса**


| **Имя параметра** | **Обязательно** | **Тип** | **Описание**                    | **Значение по умолчанию** | **Диапазон значений**                                              |

| ------------------ | ------------- | -------- | --------------------------- | ----------- | ------------------------------------------------------------ |
| symbol             | true          | string   | Variety code                |             | "BTC","ETH"...                                               |
| trade_type         | true          | int      | Transaction type            |             | 0:all,1: buy long,2: sell short,3: buy short,4: sell  long,5: sell liquidation,6: buy liquidation,7:Delivery long,8: Delivery short |
| type               | true          | int      | Type                        |             | 1:All Orders,2:Order in Finished Status                      |
| status             | true          | int      | Order Status                |             | 0:all 3:unsettled, 4: partly transacted,5: partly transaction withdrawl,6: all transacted,7:withdrew |
| create_date        | true          | int      | Date                        |             | 7，90（7days or 90 days）                                    |
| page_index         | false         | int      | Page, default 1st page      | 1           |                                                              |
| page_size          | false         | int      | Default 20，no more than 50 | 20          |                                                              |

**Параметр возврата**


| **Имя параметра**               | **Обязательно** | **Тип** | **Описание**                                                     | **Диапазон значений**                   |
| -------------------------------- | ------------- | -------- | ------------------------------------------------------------ | --------------------------------- |
| status                           | true          | string   | Request Processing Result                                    |                                   |
| \<object\>(Attribute Name: data) |               |          |                                                              |                                   |
| \<list\>(Attribute Name: orders) |               |          |                                                              |                                   |
| order_id                         | true          | long     | Order ID                                                     |                                   |
| symbol                           | true          | string   | Variety code                                                 |                                   |
| contract_type                    | true          | string   | Contract Type                                                | "this_week","next_week","quarter" |
| contract_code                    | true          | string   | Contract Code                                                | "BTC180914" ...                   |
| lever_rate                       | true          | int      | Leverage Rate                                                | 1\\5\\10\\20                      |
| direction                        | true          | string   | Transaction direction                                        |                                   |
| offset                           | true          | string   | "open": "close"                                              |                                   |
| volume                           | true          | decimal  | Number of Order                                              |                                   |
| price                            | true          | decimal  | Price committed                                              |                                   |
| create_date                      | true          | long     | Creation time                                                |                                   |
| order_source                     | true          | string   | Order Source                                                 |                                   |
| order_price_type                 | true          | string   | Order price type [limited price，opponent price，market price] |                                   |
| margin_frozen                    | true          | decimal  | Freeze margin                                                |                                   |
| profit                           | true          | decimal  | profit                                                       |                                   |
| trade_volume                     | true          | decimal  | Transaction quantity                                         |                                   |
| trade_turnover                   | true          | decimal  | Transaction aggregate amount                                 |                                   |
| fee                              | true          | decimal  | Servicefee                                                   |                                   |
| trade_avg_price                  | true          | decimal  | Transaction average price                                    |                                   |
| status                           | true          | int      | Order Status                                                 |                                   |
| \</list\>                        |               |          |                                                              |                                   |
| \</object\>                      |               |          |                                                              |                                   |
| total_page                       | true          | int      | Total Pages                                                  |                                   |
| current_page                     | true          | int      | Current Page                                                 |                                   |
| total_size                       | true          | int      | Total Size                                                   |                                   |
| ts                               | true          | long     | Timestamp                                                    |                                   |

**Пример**

```
ОТПРАВИТЬ https://api.hbdm.com/api/v1/contract_hisorders 


# Ответ

{
  "status": "ok",
  "data":{
    "orders":[
      {
        "symbol": "BTC",
        "contract_type": "this_week",
        "contract_code": "BTC180914",
        "volume": 111,
        "price": 1111,
        "order_price_type": "limit",
        "direction": "buy",
        "offset": "open",
        "lever_rate": 10,
        "order_id": 106837,
        "client_order_id": 10683,
        "order_source": "web",
        "created_at": 1408076414000,
        "trade_volume": 1,
        "trade_turnover": 1200,
        "fee": 0,
        "trade_avg_price": 10,
        "margin_frozen": 10,
        "profit": 10,
        "status": 1
      }
     ],
    "total_page":15,
    "current_page":3,
    "total_size":3
    },
  "ts": 1490759594752
}
```