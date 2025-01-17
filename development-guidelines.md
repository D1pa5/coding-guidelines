Конфигурация
============

На всех девелоперских машинах обязательно иметь настроенными

    git config --global user.name "User Name"
    git config --global user.email "user@example.com"

У каждого коммиттера должна быть своя уникальная пара user.name / user.email,
чтобы знать, кого бить по рукам в случае чего. Коммиттеры не должны использовать
больше одной такой пары, чтобы не портить статистику.

Рекомендуется также настроить (по вкусу)

    git config --global rerere.enabled true
    git config --global color.diff auto
    git config --global color.interactive auto
    git config --global color.status auto

Коммиты
=======

Коммитим помельче — атомарными смысловыми кусками. Пользуемся возможностью
закоммитить часть файла (hunk). (Но без фанатизма — если сильно долго разбирать
лапшу, можно в качестве исключения закоммитить всё сразу.)

Сообщения о коммитах — на английском (можно на ломанном). Кириллицу иногда
тяжело просматривать в консоли на сервере.

Первая строка в сообщении о коммите — краткое описание того, что случилось (до
50-ти символов, не строго).

Если нужно детальное описание — оно идёт с отбивкой пустой строкой. Стандартные
гитовые тулзы заточены на такой формат.

Ветки
=====

Делаем push на сервер почаще. Приятно видеть хотя бы один пуш в день.

Ветку master не трогаем ни при каких обстоятельствах — её трогает только
maintainer.

Все остальные не "системные" ветки называем с префиксом:
<developer-initials>/<branch-name> (ag/mybranch, ik/otherbranch)

Плодим свои ветки как удобно. Рекомендую подход с feature (aka topic) branches —
по ветке на фичу.

Новые ветки начинаем от мастера.

Если майнтейнер тормозит с обновлением мастера, вполне допускается начать ветку
от невлитой ветки с нужными фичами (майнтейнеру при этом нужно выписать пинка,
чтобы не тормозил).

Регулярно перематываем (rebase) ветки, находящиеся в работе, к мастеру, чтобы
облегчить слияние в конце разработки. В идеале — перематываем каждый раз когда
мастер изменяется.

Когда работа над веткой завершена, делаем ей rebase к мастеру, тестируем и даём
мейнтейнеру отмашку на вливание ветки в мастер. Влитые в мастер ветки стираем
(либо ресетим к мастеру, если очень хочется сохранить).

(Для прикладных /не библиотечных/ проектов.) На каждую инсталляцию есть по ветке
(обычно называются по имени хоста, без префикса), голова которой указывает на
тот код, который сейчас вылит на эту инсталляцию. Эти ветки контролирует и
обновляет тот, кто производит выливку на соответствующие инсталляции (может быть
несколько человек, если это, например, инсталляция для первичного тестирования).

Во многих проектах есть директория lib, в которой живут зависимости. Некоторые 
из этоих зависимостей могут быть притянуты как git subtree. Коммититься в них 
из репозитория проекта нельзя ни в коем случае. Нужно сделать коммит в основной 
репозиторий, запушиться и притянуть правки (обычно через bin/update-subtrees update).

В зависимости от проекта и библиотеки могут быть шорткаты для тестирования —
спрашивайте лидов :)
