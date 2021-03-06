﻿---
title: 'Папка "Элементы для восстановления": Exchange 2013 Help'
TOCTitle: Папка "Элементы для восстановления"
ms:assetid: efc48fb4-2ed8-4d05-93af-f3505fbc389d
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/Ee364755(v=EXCHG.150)
ms:contentKeyID: 50489433
ms.date: 04/30/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Папка \"Элементы для восстановления\"

 

_**Применимо к:** Exchange Server 2013_

_**Последнее изменение раздела:** 2016-12-09_

Для защиты от случайного или намеренного удаления элементов, а также для упрощения процесса их обнаружения до или во время судебных процессов и расследований в Microsoft Exchange Server 2013 и Exchange Online используется папку корзины. Эта папка заменяет компонент, называемый *корзиной* в более ранних версиях Exchange. Папка корзины используется для следующих функций сервера Exchange:

  - Хранение удаленного элемента

  - Восстановление отдельных элементов

  - Хранение на месте

  - Хранение для судебного разбирательства

  - Ведение журнала аудита почтового ящика

  - Журнал календаря

**Содержание**

Терминология

Папка корзины

  - Хранение удаленного элемента

  - Восстановление отдельных элементов

  - Хранение на месте и хранение для судебного разбирательства

  - Защита страниц от копирования при записи и измененные элементы

Квоты почтового ящика элементов для восстановления

## Терминология

Знание следующих терминов поможет получить общее представление о сведениях, приводимых в этом разделе.

  - **Удаление**  
    Описывает операцию, при которой элемент перемещается из какой-либо папки в папку "Удаленные", настроенную по умолчанию.

<!-- end list -->

  - **Удалить без возможности восстановления**  
    Описывает операцию, при которой элемент перемещается из папки "Удаленные" в папку корзины. Кроме того, такой термин применяется, если пользователь Microsoft Outlook удаляет элемент, нажав сочетание клавиш SHIFT+DELETE, что позволяет обойти папку "Удаленные" и добавить его непосредственно в папку корзины.

<!-- end list -->

  - **Очистка**  
    Описывает операцию, при которой элемент помечается для удаления из базы данных почтовых ящиков. Такое действие также называется *необратимым удалением из хранилища*.

К началу

## Папка корзины

Указанная папка находится в поддереве сообщений каждого почтового ящика, не являющихся межабонентскими. Поддерево сообщений, не являющихся межабонентскими, представляет собой область хранения в почтовом ящике, содержащую данные о его эксплуатации. Такое поддерево не отображается для пользователей, работающих с Outlook, Microsoft OfficeOutlook Web App или другими почтовыми клиентами.

Указанное изменение архитектуры обеспечивает следующие преимущества.

  - Если почтовый ящик перемещается в другую базу данных почтовых ящиков, папка корзины перемещается вместе с ним.

  - Папка корзины индексируется службой поиска Exchange и может быть обнаружена с помощью локального обнаружения электронных данных.

  - Папка корзины имеет свою собственную квоту хранения данных.

  - Сервер Exchange может препятствовать удалению данных из папки корзины.

  - На сервере Exchange доступно отслеживание изменений определенного содержимого.

Папка корзины содержит следующие подпапки.

  - **Deletions**   Эта подпапка содержит все элементы, удаленные из папки "Удаленные". (В Outlook пользователь может безвозвратно удалить элемент, нажав клавиши Shift+Delete.) Эта подпапка доступна пользователям при работе с функцией "Восстановить удаленные элементы" в Outlook и Outlook Web App.

  - **Versions**   Если включено хранение на месте или хранение для судебного разбирательства, эта подпапка содержит исходные и измененные копии удаленных элементов. Эта папка не отображается для конечных пользователей.

  - **Purges**   Если включены хранение для судебного разбирательства или функция восстановления отдельных элементов, эта подпапка содержит все очищенные элементы. Эта папка не отображается для конечных пользователей.

  - **Audits**   Если для почтового ящика включено ведение журнала аудита, эта подпапка будет содержать записи журнала аудита. Дополнительные сведения о ведении журнала аудита почтовых ящиков см. в разделе [Ведение журнала аудита почтового ящика](mailbox-audit-logging-exchange-2013-help.md).

  - **DiscoveryHolds**   Если включено хранение на месте, в этой вложенной папке содержатся все очищенные элементы, которые соответствуют параметрам запроса на хранение.

  - **Calendar Logging**   В этой вложенной папке содержатся изменения календаря, которые вносятся в почтовом ящике. Эта папка не отображается для пользователей.

На следующем рисунке показаны подпапки в папке корзины. Кроме того, указаны хранение удаленных элементов, восстановление отдельных элементов и рабочие процессы хранения, описанные в следующих разделах.

![Папка "Элементы для восстановления"](images/Ee364755.a1a08afc-3617-4adb-83ab-a6904516954e(EXCHG.150).gif "Папка \"Элементы для восстановления\"")

К началу

## Хранение удаленного элемента

Элемент считается безвозвратно удаленным в следующих случаях:

  - Пользователь удаляет один или все элементы из папки "Удаленные".

  - Пользователь нажимает сочетание клавиш SHIFT+DELETE, чтобы удалить элемент из любой другой папки почтового ящика.

Безвозвратно удаленные элементы перемещаются в подпапку "Удаленные" папки корзины. Это обеспечивает дополнительный уровень защиты, поэтому пользователи могут восстановить такие элементы, не прибегая к помощи службы поддержки. Для восстановления удаленного элемента пользователи могут выбрать функцию "Восстановить удаленные элементы" в приложении Outlook или Outlook Web App. Эту же функцию можно использовать для удаления элемента без возможности восстановления. Дополнительные сведения см. в следующих статьях:

  - [Восстановление удаленных элементов в Outlook](https://go.microsoft.com/fwlink/p/?linkid=524923)

  - [Восстановление удаленных элементов или электронной почты в Outlook Web App](https://go.microsoft.com/fwlink/p/?linkid=524924)

Элементы остаются в подпапке "Удаленные" до тех пор, пока не истечет период их хранения. По умолчанию период хранения удаленных элементов в базе данных почтовых ящиков равен 14 дням. Указанное значение можно изменить для всей базы данных или конкретного почтового ящика. Помимо периода хранения удаленных элементов, в отношении папки корзины применяются квоты. Дополнительные сведения см. в подразделе Квоты почтового ящика элементов для восстановления далее в этом разделе.

После окончания периода хранения удаленный элемент перемещается в папку Purges (Очищенные) и перестает отображаться для пользователя. Когда помощник для управляемых папок обрабатывает почтовый ящик, элементы в подпапке Purges удаляются из базы данных почтовых ящиков и их восстановление становится невозможным.

К началу

## Восстановление отдельных элементов

Если элемент удален из подпапки "Удаленные" (самим пользователем с помощью функции "Восстановить удаленные элементы" или автоматически, например, с помощью помощника по обслуживанию управляемых папок), пользователь не сможет его восстановить. В более ранних версиях Exchange для восстановления таких элементов администратору требовалось восстановить из резервных копий базу данных почтовых ящиков или отдельный почтовый ящик. Такие действия, как правило, задерживали процедуру восстановления на несколько минут или часов в зависимости от используемого механизма резервного копирования.

В Exchange 2013 представлена функция *восстановления отдельных элементов*, которую можно использовать для восстановления элементов без необходимости использования носителей с резервными копиями баз данных почтовых ящиков. В результате время восстановления значительно сокращается. Когда помощник по обслуживанию управляемых папок обрабатывает папку корзины в почтовом ящике, для которого включена функция восстановления отдельных элементов, любой элемент подпапки "Очищенные" продолжает храниться в ней, если для него еще не истек период хранения удаленных элементов.

В следующей таблице перечислены данные и действия, которые можно выполнять в папке корзины, если включена функция восстановления отдельных элементов.

### Папка корзины и восстановление отдельных элементов

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Состояние восстановления отдельных элементов</th>
<th>Папка корзины содержит безвозвратно удаленные элементы</th>
<th>Папка корзины содержит очищенные элементы</th>
<th>Пользователи могут удалять элементы из папки корзины</th>
<th>Помощник для управляемых папок автоматически удаляет элементы из папки корзины</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Включено</p></td>
<td><p>Да</p></td>
<td><p>Да</p></td>
<td><p>Да. Пользователи могут удалять элементы с помощью функции &quot;Восстановление удаленных элементов&quot; в Outlook или Outlook Web App. Но очищенные элементы не будут удалены из базы данных почтовых ящиков безвозвратно, пока не истечет срок их хранения.</p></td>
<td><p>Да. По умолчанию все элементы удаляются через 14 дней за исключением элементов календаря, которые удаляются через 31 дней.</p></td>
</tr>
<tr class="even">
<td><p>Отключено</p></td>
<td><p>Да</p></td>
<td><p>Нет</p></td>
<td><p>Да. В этом случае удаленные элементы помечаются как подлежащие окончательному удалению из базы данных почтовых ящиков, и их восстановление становится невозможным.</p></td>
<td><p>Да. По умолчанию все элементы удаляются через 14 дней за исключением элементов календаря, которые удаляются через 31 дней. Если до истечения периода хранения удаленных элементов достигается квота предупреждения элементов для восстановления, сообщения удаляются в порядке их поступления (ФИФО).</p></td>
</tr>
</tbody>
</table>


В Exchange 2013 функция восстановления отдельных элементов не включена по умолчанию для новых почтовых ящиков или ящиков, перемещенных из более ранней версии Exchange. Чтобы включить функцию восстановления отдельных элементов для почтового ящика, необходимо использовать командную консоль Exchange, после чего следует настроить или изменить период хранения удаленных элементов. Дополнительные сведения о способе восстановления отдельного элемента см. в разделе [Восстановление удаленных сообщений в почтовом ящике пользователя](recover-deleted-messages-in-a-user-s-mailbox-exchange-2013-help.md).

В начало

## Хранение на месте и хранение для судебного разбирательства

В Exchange 2013 и Exchange Online диспетчеры по обнаружению могут использовать локальное обнаружение электронных данных с делегированными правами [Управление обнаружением](discovery-management-exchange-2013-help.md) для поиска с целью обнаружения электронных данных содержимого почтового ящика. В Exchange 2013 и Exchange Online также представлена возможность локального хранения, позволяющего хранить элементы почтового ящика, соответствующие параметрам запроса, и защитить элементы от удаления пользователями или автоматизированными процессами. С помощью хранения для судебного разбирательства вы сможете сберечь все элементы в почтовых ящиках пользователей, предотвратив удаление этих элементов пользователями или автоматизированными процессами.

Если задать для почтового ящика хранение на месте или хранение для судебного разбирательства, помощник по обслуживанию управляемых папок не сможет автоматически удалить сообщения из вложенных папок "DiscoveryHolds" и "Очищенные". Кроме того, для почтового ящика также включается защита страниц от копирования при записи. Перед сохранением изменений в хранилище Exchange функция защиты страниц от копирования при записи создает копию исходного элемента. После отмены хранения для почтового ящика помощник по обслуживанию управляемых папок возобновляет автоматическое удаление.

В следующей таблице перечислены данные и действия, которые можно выполнять в папке корзины, если включено хранение для судебного разбирательства.

### Папка корзины и хранение

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Состояние хранения</th>
<th>Папка корзины содержит безвозвратно удаленные элементы</th>
<th>Папка корзины содержит измененные и очищенные элементы</th>
<th>Пользователи могут удалять элементы из папки корзины</th>
<th>Помощник для управляемых папок автоматически удаляет элементы из папки корзины</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Включено</p></td>
<td><p>Да</p></td>
<td><p>Да</p></td>
<td><p>Да. Пользователи могут удалять элементы с помощью функции &quot;Восстановление удаленных элементов&quot; в Outlook или Outlook Web App. Но помощник для управляемых папок не удаляет их окончательно из базы данных почтовых ящиков, если почтовый ящик помещен на хранение.</p></td>
<td><p>Нет</p></td>
</tr>
<tr class="even">
<td><p>Отключено</p></td>
<td><p>Да</p></td>
<td><p>Нет</p></td>
<td><p>Да</p></td>
<td><p>Да</p></td>
</tr>
</tbody>
</table>


Дополнительные сведения об обнаружении электронных данных на месте, хранении на месте и хранении для судебного разбирательства см. в следующих статьях:

  - [Обнаружение электронных данных на месте](in-place-ediscovery-exchange-2013-help.md)

  - [Хранение на месте и хранение для судебного разбирательства](in-place-hold-and-litigation-hold-exchange-2013-help.md)

В начало

## Защита страниц от копирования при записи и измененные элементы

Если пользователь, для которого включено хранение на месте или хранение для судебного разбирательства, изменяет конкретные свойства элемента почтового ящика, перед сохранением изменений создается копия исходного элемента почтового ящика. Исходная копия сохраняется в подпапке "Версии". Такой процесс называется *защитой страниц на основе копирования при записи*. Защита страниц от копирования при записи применяется к элементам, находящимся в любой папке почтового ящика. Подпапка "Версии" не отображается для пользователей.

В следующей таблице перечислены свойства сообщений, которые включают функцию защиты страниц от копирования при записи.

### Свойства, активирующие функцию защиты страниц на основе копирования при записи

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Тип элемента</th>
<th>Свойства, активирующие функцию защиты страниц на основе копирования при записи</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Сообщения (IPM.Note*)</p>
<p>Сообщения (IPM.Post*)</p></td>
<td><ul>
<li><p>Тема</p></li>
<li><p>Текст сообщения</p></li>
<li><p>Вложения</p></li>
<li><p>Отправители и получатели</p></li>
<li><p>Даты отправки и получения</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Элементы, отличные от сообщений</p></td>
<td><p>Любые изменения видимых свойств за исключением следующих:</p>
<ul>
<li><p>Расположение элемента (когда элемент перемещается между папками)</p></li>
<li><p>Изменение состояния элемента (прочитан или не прочитан)</p></li>
<li><p>Изменения тега хранения, применяемого к элементу</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Элементы в папке &quot;Черновики&quot; по умолчанию</p></td>
<td><p>Нет. На элементы в папке &quot;Черновики&quot; не распространяется действие функции защиты страниц от копирования при записи.</p></td>
</tr>
</tbody>
</table>


> [!IMPORTANT]  
> Функция защиты страниц от копирования при записи не сохраняет версию собрания, если его организатор получает ответы от участников и обновляются сведения об отслеживании собрания. Кроме того, функцией защиты страниц от копирования при записи не фиксируются изменения в RSS-каналах.


Когда почтовый ящик больше не находится на хранении на месте или хранении для судебного разбирательства, копии измененных элементов, которые хранятся в папке "Версии", удаляются.

В начало

## Квоты почтового ящика элементов для восстановления

Когда элемент перемещается в папку корзины, его размер вычитается из квоты почтового ящика и добавляется к размеру этой папки. В Exchange 2013 для баз данных почтовых ящиков применяется настраиваемая квота предупреждения элементов для восстановления (*нестрогая квота*) в размере 20 ГБ и квота элементов для восстановления (*строгая квота*) в размере 30 ГБ. По умолчанию указанные предельные значения наследуются всеми почтовыми ящиками в базе данных. Тем не менее можно настроить отдельные почтовые ящики с другими квотами. Дополнительные сведения см. в разделе [Настройка хранения удаленных элементов и квот элементов для восстановления](configure-deleted-item-retention-and-recoverable-items-quotas-exchange-2013-help.md).

В Exchange Online ограничения по умолчанию для квоты элементов для восстановления такие же, как и в Exchange 2013; нестрогое ограничение в размере 20 ГБ и строгое ограничение в размере 30 ГБ. Однако при помещении почтового ящика на хранение для судебного разбирательства или хранение на месте, квоты папки элементов для восстановления автоматически увеличиваются до 90 и 100 ГБ соответственно.

Когда размер папки корзины почтового ящика достигает соответствующей квоты, в ней будет невозможно сохранять дополнительные элементы. Это влияет на функции почтового ящика следующим образом.

  - Пользователи почтового ящика не могут удалять элементы.

  - Помощник для управляемых папок не может удалять элементы на основе тега хранения или параметров управляемых папок.

  - В случае почтовых ящиков, для которых задано хранение для судебного разбирательства, хранение на месте или восстановление отдельных элементов, защита страниц на основе копирования при записи не обеспечивает поддержку версий элементов, изменяемых пользователем.

  - Для почтовых ящиков с включенным ведением журнала аудита в подпапке "Аудиты" невозможно сохранить записи журнала аудита почтового ящика.

В случае почтовых ящиков, для которых не задано хранение на месте или хранение для судебного разбирательства, помощник по обслуживанию управляемых папок автоматически очищает содержимое папки корзины после окончания периода хранения удаленных элементов. Если размер папки достигает установленной квоты предупреждения элементов для восстановления, помощник автоматически удаляет элементы в порядке ФИФО.

Когда размер папки корзины достигает установленных по умолчанию строгих и нестрогих квот, пользователь информируется об этом с помощью журнала событий и предупреждения диспетчера Microsoft System Center Operations Manager. Такое предупреждение появляется, когда размер папки "Элементы для восстановления" впервые достигает установленных по умолчанию строгих и нестрогих квот, а затем выводится один раз в день.

В следующей таблице перечислены события, регистрируемые в журнале, когда размер папки корзины достигает установленных по умолчанию строгих и нестрогих квот.

### Предупреждения и ошибки, связанные с квотой элементов для восстановления

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Код события</th>
<th>Тип</th>
<th>Источник</th>
<th>Сообщение</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>10024</p></td>
<td><p>Предупреждение</p></td>
<td><p>Хранилище почтовых ящиков MSExchangeIS</p></td>
<td><p>Почтовый ящик для &lt;<em>пользователь_почтового_ящика</em>&gt; (<em>GUID</em>) превысил максимальную квоту предупреждения элементов для восстановления. Удалите элементы из числа элементов для восстановления или увеличьте квоту предупреждения элементов. Если квота элементов для восстановления будет превышена, пользователь не сможет удалять элементы из почтового ящика.</p></td>
</tr>
<tr class="even">
<td><p>10023</p></td>
<td><p>Ошибка</p></td>
<td><p>Хранилище почтовых ящиков MSExchangeIS</p></td>
<td><p>Почтовый ящик для &lt;<em>пользователь_почтового_ящика</em>&gt; (<em>GUID</em>) превысил максимальную квоту элементов для восстановления. Невозможно удалить элементы из этого почтового ящика. Необходимо сообщить владельцу о состоянии почтового ящика как можно скорее. Удалите элементы из числа элементов для восстановления или увеличьте квоту элементов для восстановления функциональности.</p></td>
</tr>
<tr class="odd">
<td><p>10023</p></td>
<td><p>Предупреждение</p></td>
<td><p>MSExchangeMailboxAssistants</p></td>
<td><p>Размер элементов для восстановления в почтовом ящике &lt;<em>пользователь_почтового_ящика</em>&gt; превысил предельный размер квоты предупреждения. Для предотвращения недоступности почтового ящика элементы из папок элементов для восстановления будут удалены. Квота предупреждения для элементов для восстановления: 20 ГБ (21 474 836 480 байт); первоначальный размер элементов для восстановления: 21475005311; текущий размер элементов для восстановления: 21474823820; статистика папки: - Обработанные папки: RecoverableItemsRoot, RecoverableItemsVersions, RecoverableItemsPurges, RecoverableItemsDeletions; первоначальные размеры папок: 21391661934, 55190914, 1987247, 26157788 (число элементов: 276828, 400, 84, 646); текущие размеры папок: 21391480443, 55190914, 1987247, 26157788 (число элементов: 276817, 400, 84, 646)</p></td>
</tr>
</tbody>
</table>


Если для почтового ящика задано хранение на месте или хранение для судебного разбирательства, защита страниц на основе копирования при записи не обеспечивает поддержку версий измененных элементов. Для обслуживания версий измененных элементов необходимо сократить размер папки корзины. Можно использовать командлет [Search-Mailbox](https://technet.microsoft.com/ru-ru/library/dd298173\(v=exchg.150\)) для копирования сообщений из папки "Элементы для восстановления" почтового ящика в почтовый ящик найденных сообщений, после чего удалить элементы из почтового ящика. Кроме того, можно увеличить квоту элементов для восстановления, настроенную для почтового ящика. Дополнительные сведения см. в разделе [Очистка папки "Элементы с возможностью восстановления"](clean-up-the-recoverable-items-folder-exchange-2013-help.md).

К началу

## Дополнительные сведения

  - Копирование при записи возможно, только если к почтовому ящику применено хранение на месте или хранение для судебного разбирательства.

  - Если пользователям требуется восстановить удаленные элементы из папки корзины, рекомендуем ознакомиться со следующими статьями:
    
      - [Восстановление удаленных элементов в Outlook](https://go.microsoft.com/fwlink/p/?linkid=524923)
    
      - [Восстановление удаленных элементов или электронной почты в Outlook Web App](https://go.microsoft.com/fwlink/p/?linkid=524924)

К началу

