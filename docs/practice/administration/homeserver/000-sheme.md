# Идея и схема

Мне нужно развернуть некоторое программное обеспечение для:

- **Эксплуатации полезных сервисов (email, web, репозитории)**

- **Быстрого разворачивания тестовых машин:**

- как по отдельности, так и групп;
- как пустых, так и с предустановленными системами;

## Планируемая архитектура

<img src="/img/aprt-home-network.JPG">

### Сетевое обрудование

Нужно иметь маршрутизатор на границе с провайдером. Также нужно иметь несколько коммутаторов: как минимум один управляемый и два неуправляемых. Благодаря этому можно будет разделить сеть на VLAN'ы.

Так как на данный момент у меня отсуствует острая потребность в обеспечении работоспособности полного спектра сервисов, необходимых с точки зрения безопасности, а также отсутствует программируемый маршрутизатор, то и некоторые сетевые сервисы будут работать на том уровне, который позволяет поддерживать моё сетевое оборудование. Однако, стоит оговориться, что крайне важно устанавливать такие вещи как сетевой экран (pfSense) на отдельной машине, прописывать правила и ... но у меня нет подходящей машины с кучей _ethernet_ розеток.

В дальнейшем, если будут свободные средства, я заменю маршрутизатор на отельный мини-компьютер, на который установлю Proxmox, в котором разверну целый спектр машин и уже они будут выполнять роль сетевых экранов, маршрутизировать траффик, разрешать доменные имена и делать тому подобные вещи. Ну а для беспроводной сети я сделаю отдельную точку доступа.

Для маршрутизатора я присмотрел вот [эту](https://aliexpress.ru/item/1005004302428997.html?spm=a2g2w.cart.cart_split.106.686e4aa6ukQm1I&sku_id=12000030761524529&_ga=2.230971807.1678829290.1679163308-1884218760.1677150525) штучку на **_Intel Celeron N5105_**. Но её стоимость пока не позволяет мне купить эту игрушку. Что касается таких устройств как **Orange Pi R1 Plus LTS** или что-то подобное из моделей **Raspberry Pi**, то я не думаю, что на них есть смысл тратить деньги. Есть ещё вариант купить материнскую карту от майнинг-фермы и вместо видеокарт в разъёмы _PCI Express 16_, которых там будет от 4 до 8 штук, вставить гигабитные сетевые карты.

### Машины

Центром системы станет сервер виртуализации _Proxmox_, который будет установлен на самой мощной машине. Отдельными машинами будут _NAS_ и сервер для сетевых сервисов. Пока не стану делать какие-либо LDAP-сервера или файерволы - подобные вещи в качестве упражнений я реализую в виде виртуальных машин.

Пока к системе не будет постоянного доступа из внешней сети. Постоянный IP-адрес, как показала практика, мой провайдер выдаёт, но в таком случае Интернет работает крайне нестабильно. Провайдер выдаёт через подключение _L2TP_ и динамический IP адрес. Это глобальный адрес, поэтому в дальнейшем можно использовать какой-нибудь DDNS предоставляемый или роутером, или _Open Source_ систему, или самописную.

Внутри же будет свой локальный домен (опять же без AD DC) - `aprt`, то есть `node1.aprt`, `admin.aprt` и так далее.