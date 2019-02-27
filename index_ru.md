Пожалуйста, войдите в huobi.pro, а затем посетите “Учетная запись – Управление API” для управления ключами API.
В huobi.pro поддерживаются все торговые пары.
Корневой URL-адрес: 

Global： api.huobi.pro

HBDM：api.hbdm.com

Критерии маркет-мейкера на Huobi Global
> 1. Вы должны обладать хорошей рыночной стратегией;
> 2. У вас должно быть не менее 20 BTC или эквивалентных активов, не включая бонусные возвраты на Вашем счете в Huobi Global;
> 3. Вам не будут доступны какие-либо бонусные карты, VIP или скидочные программы;
Процесс подачи заявки на позицию маркет-мейкера на Huobi Global
Если Вы соответствуете нашим критериям отбора и заинтересованы в участии в нашем маркет-мейкинг проекте, пожалуйста, напишите нам на MM_service@huobi.com, указав следующую информацию:
> 1. Идентификаторы пользователя (UIDs) (не связанные с какой-либо программой скидок в каких-либо учетных записях);
> 2. Скриншот торгового объема за последние 30 дней или VIP/корпоративного статуса с других бирж;
> 3. Краткая презентация своей стратегии маркет-мейкинга.
# WebSocket API(Market & Trade)

* [General](WS_General)
* [Reference](WS_Reference)
* Demo:[Python3](https://github.com/huobiapi/Websocket-Python3-demo)  [Node.js](https://github.com/huobiapi/WebSocket-Node.js-demo)  [PHP](https://github.com/huobiapi/WebSocket-PHP-demo) 
 [CSharp](https://github.com/huobiapi/WebSocket-CSharp-demo) 

# REST API(Рынок & Торговля)

* [Signing API Requests(Important)](Signing_API_Requests)
* [Request Process](Request_Process)
* [Reference](REST_Reference)
* Demo:[Python3](https://github.com/huobiapi/REST-Python3-demo) [Node.js](https://github.com/huobiapi/REST-Node.js-demo) [Java](https://github.com/huobiapi/REST-Java-demo) [C#](https://github.com/huobiapi/REST-CSharp-demo) [go](https://github.com/huobiapi/REST-GO-demo) [PHP](https://github.com/huobiapi/REST-PHP-demo) [C++](https://github.com/huobiapi/REST-Cpp-demo) [Objective-C](https://github.com/huobiapi/REST-ObjectiveC-demo) [QTC++](https://github.com/huobiapi/REST-QTCpp-demo) [Python2.7](https://github.com/huobiapi/REST-Python2.7-demo) [Ruby](https://github.com/huobiapi/REST-Ruby-demo) [易语言](https://github.com/huobiapi/REST-YiYuyan-demo)

# Использование SUB-UID API
* Ключ API суб-пользователей не может быть связан с IP-адресами, поэтому срок его действия истечет через 90 дней.
* Помимо всех API открытых рыночных данных, для субпользователей доступны следующие API, которые требуют подписи. Когда суб-пользователи попытаются получить доступ к другим API, отсутствующим в этом списке, система выдаст код ошибки 403.  

Метод запроса|Описание|
----------------|-----------------------|
[POST/v1/order/orders/place](https://github.com/huobiapi/API_Docs_en/wiki/REST_Reference#post-v1orderordersplace--make-an-order-in-huobipro)|	Выставить ордер |
[POST/v1/order/orders/{order-id}/submitcancel](https://github.com/huobiapi/API_Docs_en/wiki/REST_Reference#post-v1orderordersorder-idsubmitcancel--request-for-cancelling-an-order)	| Запросить отмену ордера |
[POST /v1/order/orders/batchcancel](https://github.com/huobiapi/API_Docs_en/wiki/REST_Reference#post-v1orderordersbatchcancel--batch-cancel)|	Запросить отмену нескольких ордеров, до 50 ордеров |
[POST /v1/order/orders/batchCancelOpenOrders](https://github.com/huobiapi/API_Docs_en/wiki/REST_Reference#post--v1orderbatchcancelopenorders--cancel-a-batch-of-orders-with-certain-criteria)	 | Запросить отмену нескольких ордеров, которые соответствуют определенным критериям, до 100 ордеров |
[GET /v1/account/accounts](https://github.com/huobiapi/API_Docs_en/wiki/REST_Reference#get-v1accountaccounts-get-all-the-accounts-pro-and-hadax-share-the-same-account-id)	| Получить статус учетной записи|
[GET /v1/account/accounts/{account-id}/balance](https://github.com/huobiapi/API_Docs_en/wiki/REST_Reference#get-v1accountaccountsaccount-idbalance-----get-balance-in-huobipro)	| Отобразить баланс учетной записи |
[GET /v1/order/orders/{order-id}](https://github.com/huobiapi/API_Docs_en/wiki/REST_Reference#get-v1orderordersorder-id----get-order-info)	|Отобразить детали ордера|
[GET /v1/order/orders/{order-id}/matchresults](https://github.com/huobiapi/API_Docs_en/wiki/REST_Reference#get-v1orderordersorder-idmatchresults--get-order-matchresult) 	 | Получить подробные результаты соответствий ордеру |
[GET /v1/order/orders](https://github.com/huobiapi/API_Docs_en/wiki/REST_Reference#get-v1orderorders--get-order-list) |	Поиск группы ордеров, соответствующих определенным критериям (до 100) |
[GET /v1/order/matchresults](https://github.com/huobiapi/API_Docs_en/wiki/REST_Reference#get-v1ordermatchresults----get-order-matchresults) |	Поиск трейдинговых записей аккаунта |
[GET /v1/order/openOrders](https://github.com/huobiapi/API_Docs_en/wiki/REST_Reference#get-v1orderopenorders-provide-open-orders-of-a-symbol-for-an-account) |	Получить открытые ордера учетной записи (до 500)|


# hbdm.com
## Websocket API(Рынок)

* [Reference](https://github.com/huobiapi/API_doc_ru_for_HBDM/blob/master/ws_ru.md)
* Demo：[Python](https://github.com/huobiapi/Futures-Python-demo) [Node.js](https://github.com/huobiapi/Futures-Node.js-demo)<br>

## REST API(Рынок & Торговля)

* [Reference](https://github.com/huobiapi/API_doc_ru_for_HBDM/blob/master/res_ru.md)
* Demo：[Python](https://github.com/huobiapi/Futures-Python-demo)  [Java](https://github.com/huobiapi/Futures-Java-demo) [Node.js](https://github.com/huobiapi/Futures-Node.js-demo) [PHP](https://github.com/huobiapi/Futures-PHP-demo) [C#](https://github.com/huobiapi/Futures-CSharp-demo) [Go](https://github.com/huobiapi/Futures-Go-demo)<br>
