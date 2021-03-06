﻿---
title: 'Отслеживание сообщений: Exchange 2013 Help'
TOCTitle: Отслеживание сообщений
ms:assetid: bada2ea7-6d7c-4630-b7f1-67f56818f0ff
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/Bb124375(v=EXCHG.150)
ms:contentKeyID: 51408071
ms.date: 04/30/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Отслеживание сообщений

 

_**Применимо к:** Exchange Server 2013_

_**Последнее изменение раздела:** 2016-12-09_

В Microsoft Exchange Server 2013 журнал отслеживания сообщений содержит подробные сведения о всей активности сообщений при их передаче на транспортную службу и с нее на серверы почтовых ящиков, в почтовые ящики на этих серверах и на пограничные транспортные серверы. Журналы отслеживания сообщений можно использовать для изучения сообщений, анализа потока почты, создания отчетов и устранения неполадок.

В Exchange 2013 можно использовать командлеты **Set-TransportService** и **Set-MailboxServer** для всех задач отслеживания конфигурации, поскольку на сервере почтовых ящиков Exchange 2013 расположена служба транспорта и почтовые ящики. Любой из этих командлетов можно использовать для внесения следующих изменений в настройку отслеживания сообщений.

  - Включение и отключение отслеживания сообщений. По умолчанию регистрация включена.

  - Выбор расположения файлов журналов отслеживания сообщений.

  - Задание максимального размера отдельных файлов журналов отслеживания сообщений. Значение по умолчанию — 10 МБ.

  - Задание максимального размера каталога, который содержит файлы журналов отслеживания сообщений. Значение по умолчанию — 1 000 MB.

  - Задание максимального времени хранения файлов журналов отслеживания сообщений. Значение по умолчанию — 30 дней.

  - Включение и отключение регистрации темы сообщений в журналах отслеживания сообщений. По умолчанию регистрация включена.

> [!NOTE]  
> Включать и отключать отслеживание сообщений, а также указывать расположение файлов журнала отслеживания сообщений можно также в Центре администрирования Exchange.


По умолчанию для ограничения пространства на диске, где хранятся журналы отслеживания сообщений, сервер Exchange использует циклическое ведение журнала, чтобы ограничивать размер этих журналов, исходя из размера файлов и срока их хранения.

**Содержание**

Поиск в журнале отслеживания сообщений

Структура файлов журналов отслеживания сообщений

Поля в файлах журналов отслеживания сообщений

Типы событий в журнале отслеживания сообщений

Значения источника в журнале отслеживания сообщений

Примеры записей в журнале отслеживания сообщений

Журнал отслеживания сообщений и вопросы безопасности

## Поиск в журнале отслеживания сообщений

Журналы отслеживания сообщений содержат большое количество данных, собранных при перемещении сообщений через сервер почтовых ящиков Exchange 2013. При поиске в журналах отслеживания сообщений можно использовать несколько разных параметров.

  - **Get-MessageTrackingLog**   С помощью этого командлета администраторы могут искать в журнале отслеживания сообщений информацию о сообщениях, используя различные критерии фильтрации. Подробнее см. в разделе [Поиск в журналах отслеживания сообщений](search-message-tracking-logs-exchange-2013-help.md).

  - **Отчеты о доставке для администраторов**   С помощью вкладки **Отчеты о доставке** в Центре администрирования Exchange или командлетов **Search-MessageTrackingReport** и **Get-MesageTrackingReport** администраторы могут искать в журналах отслеживания сообщений информацию о сообщениях, отправленных или полученных определенным почтовым ящиком организации. Дополнительные сведения см. в разделе [Отчеты о доставке для администраторов](delivery-reports-for-administrators-exchange-2013-help.md).

  - **Отчеты о доставке для пользователей**   С помощью вкладки **Отчеты о доставке** в Outlook Web App пользователи могут искать в журналах отслеживания сообщений информацию о сообщениях, отправленных или полученных их собственным почтовым ящиком. Дополнительные сведения см. в разделе [Отчеты о доставке для пользователей](https://go.microsoft.com/fwlink/?linkid=279920).

В начало

## Структура файлов журналов отслеживания сообщений

По умолчанию файлы журнала отслеживания сообщений сохраняются в каталоге %ExchangeInstallPath%TransportRoles\\Logs\\MessageTracking.

Для файлов журнала в каталоге журнала слежения за сообщениями используется следующий шаблон имени: `MSGTRK`*ггггммдд-нннн*`.log`, `MSGTRKMA`*ггггммдд-нннн*`.log`, `MSGTRKMD`*ггггммдд-нннн*`.log` и `MSGTRKMS`*ггггммдд-нннн*`.log`. Различные журналы используются следующими службами.

  - **MSGTRK**   Эти журналы связаны со службой транспорта.

  - **MSGTRKMA**   В этих журналах регистрируются одобрения и отклонения, используемые управляемым транспортом. Подробнее см. в разделе [Управление утверждением сообщений](manage-message-approval-exchange-2013-help.md).

  - **MSGTRKMD**   Это журналы для сообщений, доставляемых в почтовые ящики службы доставки почты.

  - **MSGTRKMS**   Это журналы для сообщений, отправляемых из почтовых ящиков службы отправки почтовых ящиков.

Прототипы в именах файлов журналов означают следующее:

  - Прототип *ггггммдд* представляет собой дату создания файла журнала в формате UTC (*гггг* = год, *мм* = месяц и *дд* =  день).

  - Прототип *nnnn* — это номер экземпляра, который ежедневно начинается с 1 для каждого префикса имен файлов журналов отслеживания сообщений.

Данные будут записываться в каждый файл журнала до тех пор, пока размер файла не достигнет максимально допустимого значения. После этого будет открыт новый файл журнала со следующим порядковым номером. Эта процедура повторяется в течение дня. Функциональная возможность циклического ведения журналов удаляет наиболее старые файлы журнала при выполнении одного из следующих условий:

  - файл журнала достиг максимального установленного срока хранения;

  - каталог журналов отслеживания сообщений достиг максимального размера.
    
    > [!IMPORTANT]  
    > Максимальный размер каталога журналов отслеживания сообщений равен общему размеру всех файлов журнала, которые имеют одинаковый префикс имен. При расчете общего размера каталога не учитываются другие файлы, которые не соответствуют соглашению о префиксе имен. Переименование старых файлов журнала или копирование других файлов в каталог журналов отслеживания сообщений может привести к превышению заданного максимального размера каталога.<br />
    Максимальный размер каталога журнала отслеживания сообщений для серверов почтовых ящиков Exchange 2013 представляет собой указанное значение, умноженное на три. Несмотря на то что файлы журнала отслеживания сообщений, создаваемые четырьмя различными службами, имеют четыре различных префикса имен, количество и частота данных, записываемых в файлы журнала <strong>MSGTRKMA</strong>, являются незначительными по сравнению с тремя другими префиксами.


Файлы журналов отслеживания сообщений представляют собой текстовые файлы с данными в формате CSV. Каждый файл журнала отслеживания сообщений имеет заголовок, содержащий следующие сведения:

  - **\#Software:**    Название программы, создавшей файл журнала отслеживания сообщений. Как правило, значением является: Microsoft Exchange Server.

  - **\#Version:**    Номер версии программы, создавшей файл журнала отслеживания сообщений. Текущее значение — 15.0.0.0.

  - **\#Log-Type:**    Значение типа журнала — "Message Tracking Log".

  - **\#Date:**    Дата и время создания файла журнала в формате UTC. Дата и время в формате UTC переводятся в формат по стандарту ISO 8601: *yyyy-mm-dd*T*hh:mm:ss.fff*Z, где *yyyy* — год, *mm* — месяц, *dd* — день, *hh* — час, *mm* — минута, *ss* — секунда, *fff* — доли секунды. "T" указывает на начало кода времени. "Z" значит "время зулу" (еще одно обозначение формата UTC).

  - **\#Fields**   Разделенные запятыми имена полей, используемые в файлах журнала отслеживания сообщений.

В начало

## Поля в файлах журналов отслеживания сообщений

В журнале отслеживания сообщений каждое событие, связанное с сообщением, заносится в отдельную строку. Информация о событиях с сообщениями упорядочена по полям, разделенным запятыми. Обычно имя поля достаточно полно характеризует информацию, которая в нем хранится. Однако некоторые поля могут оставаться пустыми и может изменяться тип информации, которая хранится в поле, в зависимости от типа события с сообщением и типа файла журнала отслеживания сообщений, где было записано событие. В следующей таблице приводятся общие описания полей, которые используются для классификации каждого события отслеживания сообщений.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Имя поля</th>
<th>Описание</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>date-time</strong></p></td>
<td><p>Дата и время события отслеживания сообщений в формате UTC. Дата и время в формате UTC переводятся в формат по стандарту ISO 8601: <em>yyyy-mm-dd</em>T<em>hh:mm:ss.fff</em>Z, где <em>yyyy</em> — год, <em>mm</em> — месяц, <em>dd</em> — день, <em>hh</em> — час, <em>mm</em> — минута, <em>ss</em> — секунда, <em>fff</em> — доли секунды. &quot;T&quot; указывает на начало кода времени. &quot;Z&quot; значит &quot;время зулу&quot; (еще одно обозначение формата UTC).</p></td>
</tr>
<tr class="even">
<td><p><strong>client-ip</strong></p></td>
<td><p>Адрес IPv4 или IPv6 сервера или клиента, который отправил сообщение.</p></td>
</tr>
<tr class="odd">
<td><p><strong>client-hostname</strong></p></td>
<td><p>Имя узла или полное доменное имя сервера или клиента обмена сообщениями , который отправил сообщение.</p></td>
</tr>
<tr class="even">
<td><p><strong>server-ip</strong></p></td>
<td><p>Адрес IPv4 или IPv6 исходного сервера или сервера назначения Exchange.</p></td>
</tr>
<tr class="odd">
<td><p><strong>server-hostname</strong></p></td>
<td><p>Имя узла или полное доменное имя сервера назначения.</p></td>
</tr>
<tr class="even">
<td><p><strong>source-context</strong></p></td>
<td><p>Дополнительная информация, относящаяся к полю <strong>источника</strong>. Например, информация об агенте транспорта.</p></td>
</tr>
<tr class="odd">
<td><p><strong>connector-id</strong></p></td>
<td><p>Имя исходного или конечного соединителя отправки или приема. Например, <em>Имя_сервера</em>\<em>Имя_соединителя</em> или <em>Имя_соединителя</em>.</p></td>
</tr>
<tr class="even">
<td><p><strong>source</strong></p></td>
<td><p>Компонент транспорта Exchange, отвечающий за событие, связанное с отслеживанием сообщений. Значения, которые содержатся в этом поле, описаны в разделе Значения источника в журнале отслеживания сообщений далее.</p></td>
</tr>
<tr class="odd">
<td><p><strong>event-id</strong></p></td>
<td><p>Тип события. Типы событий описаны в разделеТипы событий в журнале отслеживания сообщений далее.</p></td>
</tr>
<tr class="even">
<td><p><strong>internal-message-id</strong></p></td>
<td><p>Идентификатор сообщения, назначенный сервером Exchange, который выполняет текущую обработку сообщения.</p>
<p>В журнале отслеживания сообщений на каждом из серверов Exchange, которые участвуют в передаче сообщения, для каждого отдельного сообщения будет указываться свое значение <strong>internal-message-id</strong>. Пример значения: <code>73014444033</code>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>message-id</strong></p></td>
<td><p>Значение поля заголовка <strong>Message-Id:</strong> в заголовке сообщения. Если поле заголовка <strong>Message-Id:</strong> не существует или пусто, назначается произвольное значение. Это значение не изменяется на протяжении всего времени жизни сообщения. Для созданных в Exchange сообщений значение указывается в формате <code>&lt;GUID@ServerFQDN&gt;</code>, включая угловые скобки (<code>&lt; &gt;</code>). Например, <code>&lt;4867a3d78a50438bad95c0f6d072fca5@mailbox01.contoso.com&gt;</code>. В других системах обмена сообщениями могут использоваться другие значения или синтаксис.</p></td>
</tr>
<tr class="even">
<td><p><strong>network-message-id</strong></p></td>
<td><p>Уникальное значение идентификатора сообщения, которое сохраняется в различных копиях сообщения, которые могут создаваться в связи с развертыванием или расширением группы рассылки. Пример значения: <code>1341ac7b13fb42ab4d4408cf7f55890f</code>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>recipient-address</strong></p></td>
<td><p>Адрес электронной почты получателя сообщения. Если указано несколько адресов, то они отделяются друг от друга точкой с запятой (;).</p></td>
</tr>
<tr class="even">
<td><p><strong>recipient-status</strong></p></td>
<td><p>Это поле содержит состояния каждого получателя, разделенные символом точки с запятой (;). Значения состояния представляются получателям в таком же порядке, как и значения в поле <strong>recipient-address</strong>. Примеры значений состояния: <code>250 2.1.5 Recipient OK</code> и <code>550 4.4.7 QUEUE.Expired;&lt;ErrorText&gt;</code>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>total-bytes</strong></p></td>
<td><p>Размер сообщения с учетом вложений (в байтах).</p></td>
</tr>
<tr class="even">
<td><p><strong>recipient-count</strong></p></td>
<td><p>Количество получателей сообщения.</p></td>
</tr>
<tr class="odd">
<td><p><strong>related-recipient-address</strong></p></td>
<td><p>В этом поле для событий <strong>EXPAND</strong>, <strong>REDIRECT</strong> и <strong>RESOLVE</strong> выводятся другие адреса получателей, связанные с сообщением.</p></td>
</tr>
<tr class="even">
<td><p><strong>reference</strong></p></td>
<td><p>В этом поле содержится дополнительная информация о конкретных типах событий. Например:</p>
<p><strong>DSN</strong>   Содержит ссылку на отчет, которая является значением <strong>Message-Id</strong> связанного уведомления о доставке (DSN), если после события создается DSN. Если это сообщение DSN, в поле <strong>Reference</strong> содержится значение <strong>Message-Id</strong> исходного сообщения, для которого был создан DNS.</p>
<p><strong>EXPAND</strong>   Справочное поле содержит значение <strong>related-recipient-address</strong> связанных сообщений.</p>
<p><strong>RECEIVE</strong>   Справочное поле может содержать значение <strong>Message-Id</strong> связанного сообщения, если сообщение было создано другими процессами, например ведением журнала или правилами для папки &quot;Входящие&quot;.</p>
<p><strong>SEND</strong>   Справочное поле содержит значение <strong>Internal-Message-Id</strong> любых сообщений DSN.</p>
<p><strong>THROTTLE</strong>   Справочное поле содержит причину регулирования сообщения.</p>
<p><strong>TRANSFER</strong>   В данном справочном поле содержится идентификатор Internal-Message-Id сообщения с ветвлением.</p>
<p>Для сообщений, созданных правилами для папки &quot;Входящие&quot;, поле <strong>Справка</strong> содержит значение <strong>Internal-Message-Id</strong> входящего сообщения, из-за которого правило для папки &quot;Входящие&quot; создало исходящее сообщение.</p>
<p>Для других типов событий поле <strong>Справка</strong> может содержать значение <strong>Internal-Message-Id</strong> для разветвленных сообщений.</p>
<p>Для остальных типов событий поле <strong>Справка</strong> не заполняется.</p></td>
</tr>
<tr class="odd">
<td><p><strong>message-subject</strong></p></td>
<td><p>Тема сообщения указывается в поле заголовка <code>Subject:</code>. Отслеживание тем сообщений контролируется параметром <em>MessageTrackingLogSubjectLoggingEnabled</em> в командлете <strong>Set-TransportService</strong> или <strong>Set-MailboxServer</strong>. По умолчанию отслеживание тем сообщений включено.</p></td>
</tr>
<tr class="even">
<td><p><strong>sender-address</strong></p></td>
<td><p>Адрес электронной почты, указанный в поле заголовка <code>Sender:</code> или в поле заголовка <code>From:</code> (если заголовок <code>Sender:</code> отсутствует).</p></td>
</tr>
<tr class="odd">
<td><p><strong>return-path</strong></p></td>
<td><p>Обратный адрес электронной почты, указанный в параметре <code>MAIL FROM:</code> конверта сообщения. Несмотря на то что это поле всегда заполнено, в нем может быть указан нулевой адрес отправителя в виде значения <code>&lt;&gt;</code>.</p></td>
</tr>
<tr class="even">
<td><p><strong>message-info</strong></p></td>
<td><p>Дополнительные сведения о сообщении. Например:</p>
<ul>
<li><p>Дата и время поступления сообщения в формате UTC для событий <strong>DELIVER</strong> и <strong>SEND</strong>. Это дата и время первоначального поступления сообщения в организацию Exchange. Дата и время в формате UTC переводятся в формат по стандарту ISO 8601: <em>yyyy-mm-dd</em>T<em>hh:mm:ss.fff</em>Z, где <em>yyyy</em> — год, <em>mm</em> — месяц, <em>dd</em> — день, <em>hh</em> — час, <em>mm</em> — минута, <em>ss</em> — секунда, <em>fff</em> — доли секунды. &quot;T&quot; указывает на начало кода времени. &quot;Z&quot; значит &quot;время зулу&quot; (еще одно обозначение формата UTC).</p></li>
<li><p>Ошибки проверки подлинности. Например, может отображаться значение <code>11a</code> и тип проверки подлинности, который использовался, когда произошла ошибка.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>directionality</strong></p></td>
<td><p>Направление сообщения. Примеры значений: <code>Incoming</code>, <code>Undefined</code> и <code>Originating</code>.</p></td>
</tr>
<tr class="even">
<td><p><strong>tenant-id</strong></p></td>
<td><p>Это поле не используется в локальных организациях Exchange 2013.</p></td>
</tr>
<tr class="odd">
<td><p><strong>original-client-ip</strong></p></td>
<td><p>Адрес IPv4 или IPv6 исходного клиента.</p></td>
</tr>
<tr class="even">
<td><p><strong>original-server-ip</strong></p></td>
<td><p>Адрес IPv4 или IPv6 исходного сервера.</p></td>
</tr>
<tr class="odd">
<td><p><strong>custom-data</strong></p></td>
<td><p>Это поле содержит данные, связанные с определенными типами событий. Например, агент правил транспорта использует это поле для записи GUID правила транспорта или политики DLP, которая применялась к сообщению. Дополнительные сведения об этих значениях агента правил транспорта см. в подразделе &quot;Ведение журнала данных&quot; в разделе <a href="view-dlp-policy-detection-reports-exchange-2013-help.md">Просмотр отчетов об обнаружении политик защиты от потери данных</a>.</p></td>
</tr>
</tbody>
</table>


В начало

## Типы событий в журнале отслеживания сообщений

Различные типы событий в поле **event-id** используются для классификации событий, связанных с сообщениями, в журнале отслеживания сообщений. Некоторые события, связанные с сообщениями, отображаются только в одном типе файлов журнала отслеживания сообщений, а некоторые — во всех типах файлов. Типы событий, используемые для классификации каждого события, приведены в следующей таблице.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Имя события</th>
<th>Описание</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>AGENTINFO</strong></p></td>
<td><p>Это событие используется агентами транспорта для журналирования пользовательских данных.</p></td>
</tr>
<tr class="even">
<td><p><strong>BADMAIL</strong></p></td>
<td><p>Сообщение отправлено каталогом раскладки или каталогом преобразования и не может быть доставлено и возвращено.</p></td>
</tr>
<tr class="odd">
<td><p><strong>DEFER</strong></p></td>
<td><p>Доставка сообщения отложена.</p></td>
</tr>
<tr class="even">
<td><p><strong>DELIVER</strong></p></td>
<td><p>Сообщение было доставлено в локальный почтовый ящик.</p></td>
</tr>
<tr class="odd">
<td><p><strong>DROP</strong></p></td>
<td><p>Сообщение было отклонено без уведомления о доставке (также называемого сообщением возврата или отчетом о недоставке). Например:</p>
<ul>
<li><p>сообщения о выполненных запросах для утверждения;</p></li>
<li><p>нежелательные сообщения, удаленные автоматически без отчета о недоставке.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>DSN</strong></p></td>
<td><p>Создано уведомление о доставке.</p></td>
</tr>
<tr class="odd">
<td><p><strong>DUPLICATEDELIVER</strong></p></td>
<td><p>Сообщение было доставлено получателю повторно. Повторная доставка сообщений может происходить в том случае, если получатель входит в несколько вложенных групп рассылки. Банк данных обнаруживает и удаляет дубликаты сообщений.</p></td>
</tr>
<tr class="even">
<td><p><strong>DUPLICATEEXPAND</strong></p></td>
<td><p>При расширении группы рассылки обнаружен повторяющийся получатель.</p></td>
</tr>
<tr class="odd">
<td><p><strong>DUPLICATEREDIRECT</strong></p></td>
<td><p>Альтернативный получатель сообщения уже являлся получателем.</p></td>
</tr>
<tr class="even">
<td><p><strong>EXPAND</strong></p></td>
<td><p>Была расширена группа рассылки.</p></td>
</tr>
<tr class="odd">
<td><p><strong>FAIL</strong></p></td>
<td><p>Не удается доставить сообщение. Источники: <strong>SMTP</strong>, <strong>DNS</strong>, <strong>QUEUE</strong> и <strong>ROUTING</strong>.</p></td>
</tr>
<tr class="even">
<td><p><strong>HADISCARD</strong></p></td>
<td><p>Теневое сообщение было отвергнуто, после того как основная копия была доставлена на следующий узел. Подробнее см. в разделе <a href="shadow-redundancy-exchange-2013-help.md">Теневая избыточность</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>HARECEIVE</strong></p></td>
<td><p>Теневое сообщение было получено сервером в локальной группе обеспечения доступности баз данных или на сайте Active Directory.</p></td>
</tr>
<tr class="even">
<td><p><strong>HAREDIRECT</strong></p></td>
<td><p>Создано теневое сообщение.</p></td>
</tr>
<tr class="odd">
<td><p><strong>HAREDIRECTFAIL</strong></p></td>
<td><p>Не удалось создать теневое сообщение. Сведения сохранены в поле <strong>source-context</strong>.</p></td>
</tr>
<tr class="even">
<td><p><strong>INITMESSAGECREATED</strong></p></td>
<td><p>Сообщение отправлено контролируемому получателю, поэтому оно отправлено в почтовый ящик вынесения решения для утверждения. Подробнее см. в разделе <a href="manage-message-approval-exchange-2013-help.md">Управление утверждением сообщений</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>LOAD</strong></p></td>
<td><p>Сообщение успешно загружено при загрузке.</p></td>
</tr>
<tr class="even">
<td><p><strong>MODERATIONEXPIRE</strong></p></td>
<td><p>Модератор контролируемого получателя не утвердил и не отклонил сообщение, поэтому для него истек срок ожидания. Дополнительные сведения о контролируемых получателях см. в разделе <a href="manage-message-approval-exchange-2013-help.md">Управление утверждением сообщений</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>MODERATORAPPROVE</strong></p></td>
<td><p>Модератор контролируемого получателя утвердил сообщение, поэтому оно было доставлено контролируемому получателю.</p></td>
</tr>
<tr class="even">
<td><p><strong>MODERATORREJECT</strong></p></td>
<td><p>Модератор контролируемого получателя отклонил сообщение, поэтому оно не было доставлено контролируемому получателю.</p></td>
</tr>
<tr class="odd">
<td><p><strong>MODERATORSALLNDR</strong></p></td>
<td><p>Все запросы утверждения, отправленные всем модераторам контролируемого получателя, не могли быть доставлены и привели к отправке отчетов о недоставке.</p></td>
</tr>
<tr class="even">
<td><p><strong>NOTIFYMAPI</strong></p></td>
<td><p>Сообщение было обнаружено в папке &quot;Исходящие&quot; почтового ящика на локальном сервере.</p></td>
</tr>
<tr class="odd">
<td><p><strong>NOTIFYSHADOW</strong></p></td>
<td><p>Сообщение было обнаружено в папке &quot;Исходящие&quot; почтового ящика на локальном сервере, и необходимо создать теневую копию сообщения.</p></td>
</tr>
<tr class="even">
<td><p><strong>POISONMESSAGE</strong></p></td>
<td><p>Сообщение помещено в очередь сообщений о сбое или удалено из нее.</p></td>
</tr>
<tr class="odd">
<td><p><strong>PROCESS</strong></p></td>
<td><p>Сообщение успешно обработано.</p></td>
</tr>
<tr class="even">
<td><p><strong>PROCESSMEETINGMESSAGE</strong></p></td>
<td><p>Сообщение о собрании обработано службой транспортной доставки почтовых ящиков.</p></td>
</tr>
<tr class="odd">
<td><p><strong>RECEIVE</strong></p></td>
<td><p>Сообщение было получено компонентом получения протокола SMTP службы транспорта или из каталога раскладки или каталога преобразования (источник: <code>SMTP</code>), или сообщение было отправлено из почтового ящика в службу отправки почтовых ящиков (источник: <code>STOREDRIVER</code>).</p></td>
</tr>
<tr class="even">
<td><p><strong>REDIRECT</strong></p></td>
<td><p>Сообщение перенаправлено другому получателю в результате поиска в Active Directory.</p></td>
</tr>
<tr class="odd">
<td><p><strong>RESOLVE</strong></p></td>
<td><p>В результате поиска в Active Directory для получателей сообщения был найден другой адрес электронной почты.</p></td>
</tr>
<tr class="even">
<td><p><strong>RESUBMIT</strong></p></td>
<td><p>Сообщение было автоматически повторно отправлено из сети безопасности. Подробнее см. в разделе <a href="safety-net-exchange-2013-help.md">Система безопасности</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>RESUBMITDEFER</strong></p></td>
<td><p>Сообщение, повторно отправленное из сети безопасности, было отложено.</p></td>
</tr>
<tr class="even">
<td><p><strong>RESUBMITFAIL</strong></p></td>
<td><p>Сообщение, повторно отправленное из сети безопасности, не удалось отправить.</p></td>
</tr>
<tr class="odd">
<td><p><strong>SEND</strong></p></td>
<td><p>Сообщение было отправлено протоколом SMTP между службами транспорта.</p></td>
</tr>
<tr class="even">
<td><p><strong>SUBMIT</strong></p></td>
<td><p>Служба отправки почтовых ящиков успешно передала сообщение службе транспорта. Для событий <strong>SUBMIT</strong> свойство <strong>source-context</strong> содержит следующие данные:</p>
<ul>
<li><p><strong>MDB</strong>   GUID базы данных почтовых ящиков.</p></li>
<li><p><strong>Mailbox</strong>   GUID почтового ящика.</p></li>
<li><p><strong>Event</strong>   Порядковый номер события.</p></li>
<li><p><strong>MessageClass</strong>   Тип сообщения. Например, <code>IPM.Note</code>.</p></li>
<li><p><strong>CreationTime</strong>   Дата и время отправки сообщения.</p></li>
<li><p><strong>ClientType</strong>   Например, <code>User</code>, <code>OWA</code> или <code>ActiveSync</code>.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>SUBMITDEFER</strong></p></td>
<td><p>Передача сообщения из службы доставки почты в почтовый ящик в службу транспорта была отложена.</p></td>
</tr>
<tr class="even">
<td><p><strong>SUBMITFAIL</strong></p></td>
<td><p>Передача сообщения из службы доставки почты в почтовый ящик в службу транспорта не была выполнена.</p></td>
</tr>
<tr class="odd">
<td><p><strong>SUPPRESSED</strong></p></td>
<td><p>Передача сообщения была отменена.</p></td>
</tr>
<tr class="even">
<td><p><strong>THROTTLE</strong></p></td>
<td><p>Сообщение было отрегулировано.</p></td>
</tr>
<tr class="odd">
<td><p><strong>TRANSFER</strong></p></td>
<td><p>В результате преобразования содержимого, ограничения числа получателей или работы агентов получатели были перемещены в сообщение с ветвлением. Источники: <strong>ROUTING</strong> или <strong>QUEUE</strong>.</p></td>
</tr>
</tbody>
</table>


В начало

## Значения источника в журнале отслеживания сообщений

Значения в поле **source** в журнале отслеживания сообщений указывает на компонент транспорта, ответственный за событие отслеживания сообщений. В следующей таблице описаны значения поля **source**.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Значение источника</th>
<th>Описание</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>ADMIN</strong></p></td>
<td><p>Источник события был введен пользователем. Например, администратор использовал средство просмотра, чтобы удалить сообщение, или отправил файлы сообщений с помощью каталога воспроизведения.</p></td>
</tr>
<tr class="even">
<td><p><strong>AGENT</strong></p></td>
<td><p>Источником события был агент транспорта.</p></td>
</tr>
<tr class="odd">
<td><p><strong>APPROVAL</strong></p></td>
<td><p>Источником события была платформа утверждения, используемая для контролируемых получателей. Подробнее см. в разделе <a href="manage-message-approval-exchange-2013-help.md">Управление утверждением сообщений</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>BOOTLOADER</strong></p></td>
<td><p>Источником события были необработанные сообщения, которые присутствовали на сервере на момент загрузки. Это относится к типу событий <strong>LOAD</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>DNS</strong></p></td>
<td><p>Источником события было DNS.</p></td>
</tr>
<tr class="even">
<td><p><strong>DSN</strong></p></td>
<td><p>Источником события было уведомление о доставке (DSN). Например, отчет о недоставке (NDR).</p></td>
</tr>
<tr class="odd">
<td><p><strong>GATEWAY</strong></p></td>
<td><p>Источником события был внешний соединитель. Подробнее см. в разделе <a href="foreign-connectors-exchange-2013-help.md">Внешние соединители</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>MAILBOXRULE</strong></p></td>
<td><p>Источником события было правило для папки &quot;Входящие&quot;. Дополнительные сведения см. в разделе <a href="https://go.microsoft.com/fwlink/?linkid=285479">Правило для папки &quot;Входящие&quot;</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>MEETINGMESSAGEPROCESSOR</strong></p></td>
<td><p>Источником события был обработчик сообщения о собрании, который обновляет календари в соответствии с обновлениями собрания.</p></td>
</tr>
<tr class="even">
<td><p><strong>ORAR</strong></p></td>
<td><p>Источником события был альтернативный получатель, запрошенный отправителем (ORAR). Вы можете включить или отключить поддержку ORAR на получающих соединителях, используя параметр <em>OrarEnabled</em> в командлете <strong>New-ReceiveConnector</strong> или <strong>Set-ReceiveConnector</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>PICKUP</strong></p></td>
<td><p>Источником события был каталог раскладки. Подробнее см. в разделе <a href="pickup-directory-and-replay-directory-exchange-2013-help.md">Каталог раскладки и каталог преобразования</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>POISONMESSAGE</strong></p></td>
<td><p>Источником события был идентификатор сообщения о сбое. Дополнительные сведения о сообщениях о сбое и очереди сообщений о сбое см. в разделе <a href="queues-exchange-2013-help.md">Очереди</a></p></td>
</tr>
<tr class="odd">
<td><p><strong>PUBLICFOLDER</strong></p></td>
<td><p>Источником события была общедоступная папка, поддерживающая почту.</p></td>
</tr>
<tr class="even">
<td><p><strong>QUEUE</strong></p></td>
<td><p>Источником события была очередь.</p></td>
</tr>
<tr class="odd">
<td><p><strong>REDUNDANCY</strong></p></td>
<td><p>Источником события было избыточное теневое копирование. Подробнее см. в разделе <a href="shadow-redundancy-exchange-2013-help.md">Теневая избыточность</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>ROUTING</strong></p></td>
<td><p>Источником события был компонент разрешения маршрутизации классификатора в службе транспорта.</p></td>
</tr>
<tr class="odd">
<td><p><strong>SAFETYNET</strong></p></td>
<td><p>Источником события была сеть безопасности. Подробнее см. в разделе <a href="safety-net-exchange-2013-help.md">Система безопасности</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>SMTP</strong></p></td>
<td><p>Сообщение было отправлено компонентом отправки или получения SMTP службы транспорта.</p></td>
</tr>
<tr class="odd">
<td><p><strong>STOREDRIVER</strong></p></td>
<td><p>Источником события была MAPI-отправка из почтового ящика на локальном сервере.</p></td>
</tr>
</tbody>
</table>


В начало

## Примеры записей в журнале отслеживания сообщений

Не вызвавшее событий сообщение, отправленное между двумя пользователями, создает несколько записей в журнале отслеживания сообщений. Результаты можно просмотреть с помощью командлета **Get-MessageTrackingLog**. Подробнее см. в разделе [Поиск в журналах отслеживания сообщений](search-message-tracking-logs-exchange-2013-help.md).

Это краткий пример записей журнала отслеживания сообщений, который создается, когда пользователь pavel@contoso.com успешно отправляет тестовое сообщение пользователю victor@contoso.com. У обоих пользователей есть почтовые ящики на одном и том же сервере.

    EventId    Source      Sender            Recipients             MessageSubject
    -------    ------      ------            ----------             --------------
    NOTIFYMAPI STOREDRIVER                   {}
    RECEIVE    STOREDRIVER chris@contoso.com {michelle@contoso.com} test
    SUBMIT     STOREDRIVER chris@contoso.com {michelle@contoso.com} test
    HAREDIRECT SMTP        chris@contoso.com {michelle@contoso.com} test
    RECEIVE    SMTP        chris@contoso.com {michelle@contoso.com} test
    AGENTINFO  AGENT       chris@contoso.com {michelle@contoso.com} test
    SEND       SMTP        chris@contoso.com {michelle@contoso.com} test
    DELIVER    STOREDRIVER chris@contoso.com {michelle@contoso.com} test

В начало

## Журнал отслеживания сообщений и вопросы безопасности

В журнале отслеживания сообщений не хранится содержимое сообщений. По умолчанию в этот журнал заносятся темы сообщений электронной почты. Для повышения безопасности и конфиденциальности функцию регистрации темы сообщения в журнале можно отключить. Прежде чем включить или отключить регистрацию тем сообщения в журнале, ознакомьтесь с политикой организации относительно раскрытия сведений в строке «Тема». Подробнее см. в разделе [Настройка отслеживания сообщений](configure-message-tracking-exchange-2013-help.md).

В начало

