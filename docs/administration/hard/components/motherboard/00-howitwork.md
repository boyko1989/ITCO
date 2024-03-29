# Принцип работы материнских плат

Процессор и память - это та нерушимая связка, которая подразумевается, кога мы говорим о работе компьютера. Соответственно, от этой точки можно отталкиваться, когда мы хотим понять как должно происходить внутреннее взаимодействие компонентов.

## Чипсет

Исторически в материнской плате было два важных узла: северный и южный мост. Через северный мост осуществлялось взаимодействие оператвной памяти и процессора. Сейчас это устройство "переехало" в CPU, что позволило снизить задержки.

Южный же мост (уж коли нет северного), теперь называют просто "чипсет". Это важная характеристика материнки. По терминологии Intel, связь процессора с данным узелом происходит по шине DMI (DMI 4.0 поддерживает по четрём линиям скорость в 3,93 ГБ/с в обе стороны). AMD называет эту шину "четыре линии PCI Express".

Для подключения переферии существует подсистема ввода/вывода (high speed i/o interface).

https://community.fs.com/ru/blog/pcie-card-selection-guide.html

<!--
- lm324
- MX BIOS
- NH82801GB
- Контроллер графики и памяти Intel® 82G31
- Контроллер графики и памяти Intel® 82G31
- W83627DHG-A
- GD75232DW
- P0903BDG MOSFET
- Сетевая карта Orient XWT-R81PEV2 1 x RJ45
-->

## Видеокарта
