# Устройства оперативной памяти

### Об организации памяти

Чтобы понять, что это такое нужно вспомнить, как устроена адресация памяти. Полное описание всего этого с техническими подробностями будет [здесь](../../../administration/00-hard/arch/memory/README.md). В общих чертах можно сказать, что биты, которые являются минимальными единицами хранения информации, не адресуются. Адресовать можно байт (8 бит) или слово, длина которого чаще всего соответствует разрядности процессора.

В любом случае, для доступа к информации процессор обращается к этой минимальной единице по адресу. В конечном итоге вид адреса, по которому мы берём информацию из памяти называется **_физическим адресом_**.

В аргументах инструкций (например, языка ассемблера) указывается **_эффективный адрес_**, численно он совпадает с _виртуальным адресом_. Указывается он в качестве параметра сегмента памяти (байт, слово или что там у нас). Предполагается, что нам также известен номер сегмента (в параметре которого мы указали эффективный адрес). Сегмент же мы выбрали при помощи **селектора**. Его уже мы используем в паре чисел `selector:offset`, которая предствляет собой **_логический адрес_**. **_Сегментная адресация памяти_** — схема логической адресации памяти компьютера в архитектуре x86. Соответственно адресация происходит по схеме селектор - смещение.

Ещё раз, _сегментом_ называется условно выделенная область адресного пространства определённого размера, а _смещением_ — адрес ячейки памяти относительно начала сегмента. _Базой_ сегмента называется линейный адрес (адрес относительно всего объёма памяти), который указывает на начало сегмента в адресном пространстве. В результате получается **_сегментный (логический) адрес_**, который соответствует линейному адресу база _сегмента+смещение_ и который выставляется процессором на шину адреса.

**_Дескриптор сегмента_** — служебная структура в памяти, которая определяет сегмент. Соответственно, нужно организовать некие служебные структуры данных, чтобы хранить эти дескрипторы. Такие есть у нас и называются они **_дескрипторными таблицами_**, подвидом которых являются **_таблицы дескрипторов прерываний_** (IDT). Там содержатся список обработчиков прерываний(Interrupt handler, ISR) и список запросов прерываний (IRQ). Чтобы их свзять в существует структура данных "Таблицы векторов прерываний" (IVT).

Немного запутанно, нужно понять, что на русский язык аббревиатура IDT (Interrupt Descriptor Table) переводится в том числе как "Таблица векторов прерываний". Почему - для меня загадка...

### Обратно к INT 13H

**INT** - в данном случае, это инструкции ассемблера для 86x процессоров, которые генерируются программные прерывания. Инструкции пронумерованы в шестнадцатиричном виде. Каждое семейство процессоров имеет свои таблицы векторов прерываний (IVT) и дескрипторные таблицы (IDT).
