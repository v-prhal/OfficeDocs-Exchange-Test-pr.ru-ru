﻿---
title: Технический обзор советов политик в Exchange Online и Exchange 2013
TOCTitle: Советы политик
ms:assetid: 4266b83c-dd8a-4b3d-99ff-402e68fc810c
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/JJ150512(v=EXCHG.150)
ms:contentKeyID: 50487170
ms.date: 04/30/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Советы политик

 

_**Применимо к:** Exchange Online, Exchange Server 2013_

_**Последнее изменение раздела:** 2015-07-22_

Чтобы предотвратить несанкционированную отправку конфиденциальных сведений по электронной почте пользователями Microsoft Outlook, Outlook Web App (OWA) и OWA для устройств в вашей организации, вы можете создать политики защиты от потери данных, включающие уведомления с *подсказками политики*. Так же как подсказки, которые появились в Microsoft Exchange Server 2010, уведомления с подсказками политики выводятся в Outlook, когда пользователи создают сообщения электронной почты. Уведомления с подсказками политики появляются только в том случае, если сообщение отправителя каким-либо образом нарушает действующую политику предотвращения потери данных и эта политика включает правило, предусматривающее вывод уведомлений при соблюдении заданных условий. Более общие сведения о предотвращении потери данных см. в разделе [Защита от потери данных](technical-overview-of-dlp-data-loss-prevention-in-exchange.md).

Чтобы отправители электронной почты получали подсказки политики, в правила нужно включить действие **Уведомлять отправителя с помощью подсказки политики**. Добавить его можно с помощью редактора правил в Центре администрирования Exchange. Подробнее см. в разделе [Управление подсказками политик](how-to-configure-and-manage-policy-tips-a-dlp-feature-exchange.md).

Агент правил транспорта, который применяет политики предотвращения потери данных, не делает различий между вложениями в сообщения электронной почты, основным текстом и строками темы в процессе анализа сообщений и условий политик. Например, если пользователь создает сообщение электронной почты с номером кредитной карты в основном тексте и затем пытается отправить его получателю за пределами организации, в Outlook или Outlook Web App может отобразиться подсказка политики с напоминаем о правилах, действующих в организации в отношении подобной информации. Однако это уведомление выводится только в том случае, если вы настроили политику предотвращения потери данных, которая ограничивает выполнение определенных действий (в данном примере — добавление внешнего псевдонима электронной почты в заголовок сообщения, содержащего данные кредитной карты). При создании политик предотвращения потери данных вы можете выбрать различные условия, действия и исключения. Это позволяет вам адаптировать политику в соответствии с конкретными потребностями вашей организации.

Каждый раз при использовании действия уведомления отправителя или действия переопределения в правиле мы рекомендуем также включить условие того, что сообщение было отправлено из вашей организации. Это можно сделать с помощью редактора правил политики: **Расположение отправителя…** \> **внутри организации**. Дополнительные сведения об изменении существующих политик DLP см. в разделе [Управление политиками защиты от потери данных](manage-dlp-policies-exchange-2013-help.md). Это только рекомендация, так как действие уведомления отправителя применяется в рамках процесса создания сообщения вашей компании. Отправители, указанные в действии — это авторы сообщений в вашей компании. Взаимодействие с пользователем, предоставляемое подсказками политики, недоступно пользователям для входящих сообщений и будет игнорироваться, если отправитель расположен за пределами организации. Вы можете применить политики DLP для проверки входящих сообщений и выполнения различных действий. Но при этом не добавляйте действие уведомления отправителя.

Если отправители получают уведомления о требованиях и стандартах, принятых в организации, непосредственно в процессе создания сообщений с помощью подсказок политики, это снижает вероятность того, что они нарушат эти требования или стандарты.

> [!NOTE]  
> <ul><li><p>В Exchange Online защита от потери данных — дополнительная возможность, для использования которой требуется подписка на Exchange Online (план 2). Дополнительные сведения см. в статье о <a href="https://go.microsoft.com/fwlink/p/?linkid=286154">лицензировании Exchange Online</a>.</p></li>
> <li><p>В Exchange 2013 защита от потери данных — дополнительная возможность, для использования которой требуется корпоративная клиентская лицензия (CAL) на Exchange. Дополнительные сведения о клиентских лицензиях и лицензировании серверов см. в статье о <a href="https://go.microsoft.com/fwlink/p/?linkid=237292">лицензировании Exchange Server</a>.</p></li>
> <li><p>Если в вашей организации используется Exchange 2013 с пакетом обновления 1 (SP1) или Exchange Online, подсказки политики доступны для пользователей, отправляющих почту из Outlook 2013, Outlook Web App или Outlook Web App для устройств. Однако если в организации в настоящее время используется Exchange 2013, подсказки политики доступны только для пользователей, отправляющих электронную почту из Outlook 2013.</p></li></ul>


## Текст по умолчанию для подсказок политики и параметры правил

При добавлении правил уведомления отправителей в политики предотвращения потери данных вам на выбор предоставляются различные варианты. Если вы добавляете правило уведомления отправителей с помощью действия **Уведомлять отправителя с помощью подсказки политики** в рамках политики предотвращения потери данных, вы можете указать, насколько строгим должно быть это правило. Доступные параметры уведомления приведены в следующей таблице. Общие сведения о редактировании политик см. в разделе [Управление политиками защиты от потери данных](manage-dlp-policies-exchange-2013-help.md). Дополнительные сведения о создании подсказок политики см. в разделе [Управление подсказками политик](how-to-configure-and-manage-policy-tips-a-dlp-feature-exchange.md).


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Правило уведомлений</th>
<th>Смысл</th>
<th>Уведомление с подсказкой политики по умолчанию, которое будет выводиться для пользователей Outlook</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Только уведомить</strong></p></td>
<td><p>Так же как и в случае с подсказками почты, будет выводиться информационное сообщение с подсказкой о нарушении политики. Отправитель может отключить вывод подобных подсказок с помощью диалогового окна параметров подсказок политики, доступного в Outlook.</p></td>
<td><p>Это сообщение может включать конфиденциальное содержимое. Все получатели должны быть авторизованы для получения этого контента.</p></td>
</tr>
<tr class="even">
<td><p><strong>Отклонение сообщения</strong></p></td>
<td><p>Сообщение не будет доставлено, пока условие выполняется. Отправитель может указать, что его сообщение не содержит конфиденциальных данных. Это также называется переопределением ложных срабатываний. В этом случае приложение Outlook позволит сообщению покинуть папку исходящих сообщений, чтобы обеспечить возможность аудита отчета пользователя, но Exchange заблокирует отправку сообщения.</p></td>
<td><p>Это сообщение может включать конфиденциальное содержимое. Ваша организация не позволит отправить такое сообщение, пока это содержимое не будет удалено.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Отклонить, если не переопределено ложное срабатывание</strong></p></td>
<td><p>Результат применения этого правила уведомлений аналогичен правилу <strong>Отклонение сообщения</strong>. Однако в этом случае Exchange разрешит отправку сообщения получателю вместо его блокировки.</p></td>
<td><p><strong>Прежде чем отправитель выберет переопределение:</strong> Это сообщение может включать конфиденциальное содержимое. Ваша организация не позволит отправить такое сообщение, пока это содержимое не будет удалено.</p>
<p><strong>Когда отправитель выбирает переопределение:</strong> При отправке сообщения ваш отзыв будет отправлен администратору.</p></td>
</tr>
<tr class="even">
<td><p><strong>Отклонить, если не выбрано автоматическое переопределение</strong></p></td>
<td><p>Сообщение не будет доставлено, пока условие выполняется или пока отправитель не выберет переопределение. Отправитель может указать, что он хочет переопределить политику.</p></td>
<td><p><strong>Прежде чем отправитель выберет переопределение:</strong> Это сообщение может включать конфиденциальное содержимое. Ваша организация не позволит отправить такое сообщение, пока это содержимое не будет удалено.</p>
<p><strong>Когда отправитель выбирает переопределение:</strong> Вы переопределили политику организации для конфиденциального содержимого в этом сообщении. Ваши действия будут проверяться вашей организацией.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Отклонить, если не выбрано явное переопределение</strong></p></td>
<td><p>Результат применения этот правила уведомлений аналогичен правилу <strong>Отклонить, если не выбрано автоматическое переопределение</strong> за тем исключением, что если отправитель пытается переопределить политику, ему необходимо предоставить обоснование.</p></td>
<td><p><strong>Прежде чем отправитель выберет переопределение:</strong> Это сообщение может включать конфиденциальное содержимое. Ваша организация не позволит отправить такое сообщение, пока это содержимое не будет удалено.</p>
<p><strong>Когда отправитель выбирает переопределение:</strong> Вы переопределили политику организации для конфиденциального содержимого в этом сообщении. Ваши действия будут проверяться вашей организацией.</p></td>
</tr>
</tbody>
</table>


## Настройка уведомлений подсказки политики

Чтобы настроить текст уведомления подсказки политики, которое выводится в почтовой программе пользователей, выберите **Управление подсказками политики** на странице "Защита от потери данных". Для появления любого созданного вами пользовательского текста правило политики DLP должно включать действие **Уведомлять отправителя с помощью подсказки политики**. Добавьте действие в правило с помощью редактора правил предотвращения потери данных.

Инструкции по созданию собственных подсказок политики см. в разделе [Управление подсказками политик](how-to-configure-and-manage-policy-tips-a-dlp-feature-exchange.md). Текст, который вы создаете, может заменить текст по умолчанию, показанный в предыдущей таблице.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Действия и параметры уведомлений подсказок политики</th>
<th>Смысл</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Уведомить отправителя</strong></p></td>
<td><p>Ваш текст отображается только при запуске действия <strong>Уведомить отправителя, но разрешить отправку</strong>.</p></td>
</tr>
<tr class="even">
<td><p><strong>Разрешить отправителю переопределение</strong></p></td>
<td><p>Ваш текст появляется, только когда инициируются следующие действия: <strong>Блокировать сообщение, если это не ложное срабатывание</strong>, <strong>Блокировать сообщение, но разрешить отправителю переопределение и отправку</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Блокировать сообщение</strong></p></td>
<td><p>Ваш текст появляется, только когда инициируется действие <strong>Блокировать сообщение</strong>.</p></td>
</tr>
<tr class="even">
<td><p><strong>Ссылка на URL-адрес соответствия требованиям</strong></p></td>
<td><p>URL-адрес соответствия требованиям — это ссылка на веб-страницу, на которой можно объяснить политики соответствия требованиям и переопределить их. Эта ссылка отображается в подсказке политики, когда пользователь переходит по ссылке <strong>Подробнее</strong>.</p></td>
</tr>
</tbody>
</table>


## Дополнительные сведения

[Защита от потери данных](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[Управление политиками защиты от потери данных](manage-dlp-policies-exchange-2013-help.md)

[Управление подсказками политик](how-to-configure-and-manage-policy-tips-a-dlp-feature-exchange.md)

