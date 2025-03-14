# Быстрая настройка Windows

Специально для тех, кто хочет побыстрее начать, но не хочет слишком углубляться в простыню [readme.md](./readme.md).
> [!CAUTION]  
> Как обычно, компьютерная грамотность ложится полностью на вас.
> Вы должны уметь работать с консолью windows и иметь минимальные навыки обращения с командными файлами `bat`, `cmd`.
> Если грамотность отсутствует и возникает куча _"как?"_ на базовых вещах, значит эта программа не для вас.
> Разработчик не будет отвечать на вопросы из серии школы компьютерной грамотности.
> Если вы все-таки хотите продолжать, задавайте вопросы в дискуссиях на github или на форумах.
> Возможно, кто-то вам поможет. Но не надо писать issue на github. Они будут закрываться сразу.

## Немного разъяснений

Обход DPI является хакерской методикой. Под этим словом понимается метод, которому сопротивляется окружающая среда,
которому автоматически не гарантирована работоспособность в любых условиях и на любых ресурсах,
требуется настройка под специфические условия у вашего провайдера. Условия могут меняться со временем,
и методика может начинать или переставать работать, может потребоваться повторный анализ ситуации.
Могут обнаруживаться отдельные ресурсы, которые заблокированы иначе, и которые не работают или перестали работать.
Могут и сломаться отдельные незаблокированные ресурсы.
Поэтому очень желательно иметь знания в области сетей, чтобы иметь возможность проанализировать техническую ситуацию.
Не будет лишним иметь обходные каналы проксирования трафика на случай, если обход DPI не помогает.

Вариант, когда вы нашли стратегию где-то в интернете и пытаетесь ее приспособить к своему случаю - заведомо проблемный.
Нет универсальной таблетки. Везде ситуация разная. В сети гуляют написанные кем-то откровенные глупости, которые тиражируются массово ничего не понимающей публикой.
Такие варианты чаще всего работают нестабильно, только на части ресурсов, только на части провайдеров, не работают вообще или ломают другие ресурсы. В худших случаях еще и устраивают флуд в сети.
Если даже вариант когда-то и работал неплохо, завтра он может перестать, а в сети останется устаревшая информация.

Особо осторожным нужно быть со сторонними сборками. Там могут быть вирусы. Не в каждой сборке, но уже были замечены скаммеры.
Видео на ютубе как просто обойти блокировку, прилагающийся архив, в котором какая-то ерунда, написанная на питоне, скачивающая зловред.

Будем считать, что у вас есть windows 7 или выше. Задача - обойти блокировки с самой системы.

> [!NOTE]  
> Есть решение самое простое, а есть "как положено".

## САМОЕ ПРОСТОЕ РЕШЕНИЕ

_"Совсем ничего не могу, все очень сложно, дайте мне таблетку."_ ©Простой пользователь

1) Скачайте и распакуйте архив https://github.com/bol-van/zapret-win-bundle/archive/refs/heads/master.zip.
2) Запустите `zapret-winws/preset_russia.cmd` от имени администратора. Возможно, заведется сразу.

   > То же самое с ограничителем по автоматически создаваемому хост-листу `preset_russia_autohostlist.cmd`.
   > Что такое `autohostlist` - читайте [readme.md](./readme.md). Проще говоря, мы обходим только то, что долго и упорно не хочет открываться.
   > Сначала не будет, но надо пытаться много раз, и тогда сработает, а дальше будет всегда срабатывать.
   > Остальное не будет ломаться. Использовать только, если первый вариант тоже работает.

Не помогла _"таблетка"_ ? Это вовсе не значит, что ничего не получится. Но придется делать по нормальному.

## НЕ ПОМОГЛО, КАК ТЕПЕРЬ ЭТО УДАЛИТЬ

Если вы не устанавливали zapret как службу или запланированную задачу (а это требует редактирования cmd файлов),
достаточно закрыть окно с winws и запустить windivert_delete.cmd.
Альтернатива - перезагрузить компьютер.
После чего можно удалить папку с zapret. На этом деинсталляция закончена.
Если же вы устанавливали zapret как службу, то вы наверняка знаете как ее удалить.

## РЕШЕНИЕ "КАК ПОЛОЖЕНО"

1) Скачайте и распакуйте архив https://github.com/bol-van/zapret-win-bundle/archive/refs/heads/master.zip.

2) Если у вас Windows 7 x64, однократно запустите `win7/install_win7.cmd`. Батник заменит файлы windivert на совместимую с Windows 7 версию.

> [!WARNING]  
> Для 32-битных систем Windows нет готового полного варианта.

   > На windows 11 arm64 выполните `arm64/install_arm64.cmd` от имени администратора и перезагрузите компьютер.
   > Читайте [docs/windows.md](./windows.md)
   >
   > Имейте в виду, что антивирусы могут плохо реагировать на windivert.
   > cygwin так же имеет внушительный список несовместимостей с антивирусами, хотя современные антивирусы
   > более-менее научились с ним дружить.
   > Если проблема имеет место , используйте исключения. Если не помогает - отключайте антивирус совсем.

3) Убедитесь, что у вас отключены все средства обхода блокировок, в том числе и сам zapret.

4) Если вы работаете в виртуальной машине, необходимо использовать соединение с сетью в режиме bridge. nat не подходит

5) Запустите `blockcheck\blockcheck.cmd`.  blockcheck в начале проверяет **DNS**.
Если выводятся сообщения о подмене адресов, то нужно будет решить проблему с **DNS**.
blockcheck перейдет в этом случае на **DoH** _(DNS over HTTPS)_ и будет пытаться получить и использовать реальные IP адреса.
Но если вы не настроите решение этой проблемы, обход будет работать только для тех программ,
которые сами реализуют механизмы SecureDNS. Для других программ обход работать не будет.

   > Решение проблемы DNS выходит за рамки проекта. Обычно она решается либо заменой DNS серверов
   > от провайдера на публичные (`1.1.1.1`, `8.8.8.8`), либо в случае перехвата провайдером обращений
   > к сторонним серверам - через специальные средства шифрования DNS запросов, такие как [dnscrypt](https://www.dnscrypt.org/), **DoT** _(DNS over TLS)_, **DoH**.
   > В современных броузерах чаще всего DoH включен по умолчанию, но curl будет использовать обычный системный DNS.
   > win11 поддерживает системные DoH из коробки. Они не настроены по умолчанию.
   > В последних билдах win10 существует неофициальный обходной путь для включения DoH.
   > Для остальных систем нужно стороннее решение, работающие по принципу DNS proxy.
   >
   > Тут все разжевано как и где это включается : https://hackware.ru/?p=13707

6) blockcheck позволяет выявить рабочую стратегию обхода блокировок.
Лог скрипта будет сохранен в `blockcheck\blockcheck.log`.
Запомните/перепишите найденные стратегии.

> [!WARNING]  
> Следует понимать, что blockcheck проверяет доступность только конкретного домена, который вы вводите в начале.
> Вероятно, все остальные домены блокированы подобным образом, но не факт.

> [!TIP]  
> В большинстве случаев можно обьединить несколько стратегий в одну универсальную, и это крайне желательно.

   > Необходимо понимать [как работают стратегии](./readme.md/#nfqws).
   > zapret не может пробить блокировку по IP адресу. Для проверки нескольких доменов вводите их через пробел.
   >
   > Сейчас блокираторы ставят на магистральных каналах. В сложных случаях у вас может быть несколько маршрутов
   > с различной длиной по ХОПам, с DPI на разных хопах. Приходится преодолевать целый зоопарк DPI,
   > которые еще и включаются в работу хаотичным образом или образом, зависящим от направления (IP сервера).
   > blockcheck не всегда может выдать вам в итогах оптимальную стратегию, которую надо просто переписать в настройки.
   > В некоторых случаях надо реально думать что происходит, анализируя результат на разных стратегиях.
   > Если вы применяете большой TTL, чтобы достать до магистрала, то не лишним будет добавить дополнительный ограничитель
   > `--dpi-desync-fooling`, чтобы не сломать сайты на более коротких дистанциях.
   > _md5sig_ наиболее совместим, но работатет только на linux серверах.
   > badseq может работать только на https и не работать на http.
   > Чтобы выяснить какие дополнительные ограничители работают, смотрите результат теста аналогичных стратегий без TTL
   > с каждым из этих ограничителей.
   >
   > При использовании autottl следует протестировать как можно больше разных доменов. Эта техника
   > может на одних провайдерах работать стабильно, на других потребуется выяснить при каких параметрах
   > она стабильна, на третьих полный хаос, и проще отказаться.
   >
   > Далее, имея понимание что работает на http, https, quic, нужно сконструировать параметры запуска winws
   > с использованием мультистратегии. Как работают мультистратегии описано в [readme.md](./readme.md#множественные-стратегии).
   >
   > Прежде всего вам нужно собрать фильтр перехватываемого трафика. Это делается через параметры
   > `--wf-l3`, `--wf-tcp`, `--wf-udp`.
   > `--wf-l3` относится к версии ip протокола - ipv4 или ipv6.
   > `--wf-tcp` и `--wf-udp` содержат перечень портов или диапазонов портов через запятую.
   > 
   > Пример стандартного фильтра для перехвата http, https, quic : `--wf-tcp=80,443` `--wf-udp=443`
   > 
   > Фильтр должен быть минимально необходимым. Перехват лишнего трафика приведет только к бессмысленному расходованию ресурсов процессора и замедлению интернета.
   >
   > Если кратко по мультистратегии, то обычно параметры конструируются так :
   > ```
   > --filter-udp=443 'параметры для quic' --new
   > --filter-tcp=80,443 'обьединенные параметры для http и https'
   > ```
   >
   > Или так :
   > ```
   > --filter-udp=443 'параметры для quic' --new
   > --filter-tcp=80 'параметры для http' --new
   > --filter-tcp=443 'параметры для https'
   > ```
   >
   > Если стратегии отличаются по версии ip протокола, и вы не можете их обьединить, фильтр пишется так :
   > ```
   > --filter-l3=ipv4 --filter-udp=443 "параметры для quic ipv4" --new
   > --filter-l3=ipv4 --filter-tcp=80 'параметры для http ipv4' --new
   > --filter-l3=ipv4 --filter-tcp=443 'параметры для https ipv4' --new
   > --filter-l3=ipv6 --filter-udp=443 "параметры для quic ipv6" --new
   > --filter-l3=ipv6 --filter-tcp=80 "параметры для http ipv6" --new
   > --filter-l3=ipv6 --filter-tcp=443 "параметры для https ipv6"
   > ```
   >
   > Но здесь совсем _"копи-пастный"_ вариант.
   > Чем больше вы обьедините стратегий и сократите их общее количество, тем будет лучше.
   >
   > Если вам не нужно дурение отдельных протоколов, лучше всего будет их убрать из системы перехвата трафика через
   > параметры `--wf-*` и убрать соответствующие им профили мультистратегии.
   > tcp 80 - http, tcp 443 - https, udp 443 - quic.
   >
   > Если используются методы нулевой фазы десинхронизации (`--mss`, `--wssize`, `--dpi-desync=syndata`) и фильтрация hostlist,
   > то все параметры, относящиеся к этим методам, следует помещать в отдельные профили мультистратегии, которые получат
   > управление до определения имени хоста. Необходимо понимать алгоритм работы мультистратегий.
   >
   > ```
   > --filter-tcp=80 'параметры для http' --new
   > --filter-tcp=443 'параметры для https' --hostlist=d:/users/user/temp/list.txt --new
   > --filter-tcp=443 --wssize 1:6
   > ```
   >
   > autohostlist профиль приоритетен, поэтому wssize нужно писать туда :
   >
   > ```
   > --filter-tcp=80 'параметры для http' --new
   > --filter-tcp=443 'параметры для https' --wssize 1:6 --hostlist-auto=d:/users/user/temp/autolist.txt
   > ```
   >
   > В этих примерах wssize будет применяться всегда к порту tcp 443, а хостлист будет игнорироваться.
   > К http применять wssize вредно и бессмысленно.

7) Протестируйте найденные стратегии на winws. Winws следует брать из zapret-winws.
Для этого откройте командную строку windows от имени администратора в директории zapret-winws.
Проще всего это сделать через `_CMD_ADMIN.cmd`. Он сам поднимет права и зайдет в нужную директорию.

8) Обеспечьте удобную загрузку обхода блокировок.

   > Есть 2 варианта. Ручной запуск через ярлык или автоматический при старте системы, вне контекста текущего пользователя.
   > Последний вариант разделяется на запуск через планировщик задач и через службы windows.
   >
   > Если хотите ручной запуск, скопируйте `preset_russia.cmd` в `preset_my.cmd` (`<ваше_название>.cmd`) и адаптируйте его под ваши параметра запуска.
   > Потом можно создать ярлык на рабочем столе на `preset_my.cmd`. Не забудьте, что требуется запускать от имени администратора.
   >
   > Но лучше будет сделать неинтерактивный автоматический запуск вместе с системой.
   > В zapret-winws есть командные файлы `task_*`, предназначенные для управления задачами планировщика.
   > Там следует поменять содержимое переменной `WINWS1` на свои параметры запуска winws. Пути с пробелами нужно экранировать кавычками с обратным слэшем : `\"`.
   > После создания задач запустите их. Проверьте, что обход встает после перезагрузки windows.
   >
   > Аналогично настраиваются и службы windows. Смотрите `service_*.cmd`

9) Если ломаются отдельные незаблокированные ресурсы, нужно пользоваться ограничивающим
ipset или хост листом. Читайте основной талмуд [readme.md](./readme.md) ради подробностей.
Но еще лучше будет подбирать такие стратегии, которые ломают минимум.
Есть стратегии довольно безобидные, а есть сильно ломающие, которые подходят только для точечного пробития отдельных ресурсов,
когда ничего лучше нет. Хорошая стратегия может сильно ломать из-за плохо подобранных ограничителей для фейков - ttl, fooling.

> [!CAUTION]  
> Это минимальная инструкция, чтобы соориентироваться с чего начать. Однако, это - не панацея.
> В некоторых случаях вы не обойдетесь без знаний и основного "талмуда".

Подробности и полное техническое описание расписаны в [readme.md](./readme.md)
