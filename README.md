# SDR FAQ

Тут мы ловим КВ на свистки без конвертера, дрочим на HackRF и bladeRF, пытаемся настроить DSD, учимся GNUть Radio, принимаем Метеор М2 на вешалку, да и вообще занимаемся всякими непотребствами.
 
#### Какой приёмник покупать?
Любой на чипсете RTL2832U + R820T2, можешь купить и с R820T, но он вроде чуть хуже.
 
#### Где купить?
[aliexpress.com](http://www.aliexpress.com/wholesale?catId=0&SearchText=sdr+rtl2832u+r820t2)
 
#### Цена вопроса
~10$
 
#### Хочу что-то покруче!
HackRF + upconverter.
 
#### Железка не нужна!
[Выбирай](http://websdr.org), но помни, что без интернетов ты соснешь, а железка не такая уж дорогая.
 
#### Хочу слушать без компа
Если у тебя есть мобилка или планшет с ведром и USB OTG, на которую ты можешь накатить SDR Touch — слушай сколько влезет.
 
#### А у меня ведро без OTG, что можно сделать?
У меня тоже.
Можно поднять rtl_tcp например на Raspberry PI (или ноутбуке, лежащем в рюкзаке), поднять Wi-Fi AP на ней же и коннектится мобилкой к Raspberry через SDR Touch. Raspberry PI у меня не было, но был Wi-Fi роутер WR703N, я изъебнулся и накатил rtl_tcp на него, впрочем не прокатило, так как SDR Touch не может в 0,25 MSPS, а роутер не может в 2,4 (или около того) MSPS, но вот с компа всё работало отлично, если не считать помех от пауэрбанка, который питал роутер.
 
#### Ну купил я его, что дальше?
Скачиваешь SDRSharp, ставишь драйвера, запуская «install-rtlsdr.bat» а потом запуская «zadig.exe», который скачался в папку с шарпом. После ставишь [патч](http://www.rtl-sdr.com/new-experimental-r820t-rtl-sdr-driver-tunes-13-mhz-lower/). Теперь можешь принимать от ~3 МГц до ~1850 МГц с разной чувствительностью, а не от 24 до 1700, как везде пишут. Но ниже 13 будет довольно паршиво, и для этого лучше купить Degen DE1103 и использовать свисток как рисовалку водопадика, а на Дегене уже слушать.
Ставишь Virtual Audio Cable (далее — VAC) и fldigi.

#### DSD+ 
Да, раньше он работал как говно, а то и вообще не работал, но теперь его допилили, и этой прогой ты можешь слушать цифру типа АПКО25, например, евпочя. Всё что нужно сделать — это отключить все программные фильтры и улучшалки звука, направить вывод шарпа в первый лайн VAC и в виндовом микшере сделать чтобы вывод по умолчанию шел через твой обычный аудиовыход, а после запустить DSD и настроиться на канал в NFM. Канал, кстати, не обязательно может быть голосовой, если ты видишь, что канал не прерывается, ебашит сутками напролет и вообще самый мощный, а вокруг него тусуются много послабее, то голоса там можешь не ждать, это вероятно управляющий канал и его надо «слушать» через Unitrunker 

#### Unitrunker 
Подключи свисток, жмякай плюсик, выбирай RTL2832, в появившемся окне в поле RTL Device выбирай свое устройство, ставь галочку на Auto Gain, внизу жми VCO, в нём в поле Park прописываешь частоту своего канала и сверху жмешь треугольник плей. Если всё сделал правильно и это действительно управляющий канал, который Unitrunker поддерживает, то ты услшишь звук как в SDRSharp когда ты настроился на свой канал, еще выскочит окошко, в котором будут появляться частоты, на которых говорят голосом и прочая инфа. А еще в VCO в вкладке высвечивается что именно там у тебя за тип сигнала. 

#### PSHHH PSHHH, YOBA, PLOHOY PRIYOM!
Отрубаешь антенну, которая была в комплекте и цепляешь к чему угодно, что не находится под напряжением (во многих домах антенный кабель подключен к кабельному телевидению, к нему не подключай, так как есть риск спалить свисток. Спасибо анону за инфу). Отлично подойдет проволока или обычная телескопическая от ТВ. Поиграйся с плагином Digital Noise Reduction в SDRSharp. Хочешь лучше — пили антенну по гайдам, коих в интернатах навалом.
 
#### Хочу фоточку с NOAA
WXtoImg соединяешь с SDRSharp через VAC, в WXtoImg указываешь правильное местоположение.

«File → Update Keplers» — ты загрузил расписание и частоты спутников.

«File → Satellite Pass List» — тут ты можешь его посмотреть.

Настраиваешься на нужную частоту в SDRSharp и тыкаешь в WXtoImg «File → Auto Process», и дальше он всё сделает за тебя. Вместо WXtoImg можно использовать Aptdecoder, он вроде даже лучше, хотя я его не пробовал, так что точно не скажу и мануал по нему не запилю.
 
#### Что-то Доплер мешает
Двигайся вместе со спутником^U
Ставь Оrbitron и плагин для SDRSharp, соединяющий их, тогда SDRSharp еще и частоту за тебя настроит, и будет поддерживать нужную.
 
#### А как принимать КВ?
Да так же, как и выше. Ты же пропатчил тем патчем, ссылку на который я давал выше? Вот только если ты живешь в большом городе, да еще и в квартире, то получится принять у тебя разве что радио Китая и ему подобные. Можешь, конечно, из окна на дерево проволоку кинуть. А еще не забудь, что в разное время суток прохождение разное, так что пробуй в разное время. Эфирные радиостанции принимаются в AM, радиолюбители — в LSB и USB, погодные факсы — в USB.
 
#### А нахуя я ставил fldigi?
Чтобы декодить всякую хуйню вроде морзянки и WEFAX. Не забудь указать в настройках fldigi  и SDRSharp свой VAC.
 
#### О! А как погодный факс декодить?
Fldigi.
 
#### А rtty?
Fldigi.
 
#### А…
Fldigi! Если чего-то нет в fldigi, то оно есть в MultiPSK, если это не что-то специфическое.
 
#### Что за хуйню я поймал?
Тебе нужны [гайд по идентификации сигналов](http://www.sigidwiki.com/wiki/Signal_Identification_Guide) и [бесплатная софтина](http://www.rtl-sdr.com/artemis-free-signal-identification-software/).
 
#### А как найти частоту c хуйнёй? А что за хуйня на частоте?
Смотри радиосканеровскую [базу](http://radioscanner.ru/base).

#### У меня тут вещает хуйня, но в базе ее нет
Укажи город и возможно мы чего знаем. А возможно это просто помехи, попробуй выключить свой холодильник, который видел еще товарища Сталина.
  
#### Хочу больше всякой хуйни
[rtl-sdr.com](http://rtl-sdr.com)

Радиосканер частенько падает, так что вот [скрипт](http://pastebin.com/mDF1gWru) на случай его вставания (дампит базу с Радиосканера). Благодарю анона, написавшего скрипт.