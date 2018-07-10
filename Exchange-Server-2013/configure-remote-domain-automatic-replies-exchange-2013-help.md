﻿---
title: 'Настройка отправки автоматических ответов через удаленные домены: Exchange 2013 Help'
TOCTitle: Настройка отправки автоматических ответов через удаленные домены
ms:assetid: 3d88a1fb-4b62-419a-a50d-ffd868e229d0
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/JJ657720(v=EXCHG.150)
ms:contentKeyID: 50487926
ms.date: 04/30/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Настройка отправки автоматических ответов через удаленные домены

 

_**Применимо к:**Exchange Server 2013_

_**Последнее изменение раздела:**2015-04-08_

Можно воспользоваться командной консолью Exchange, чтобы настроить способ отправки и получения сообщений электронной почты через удаленные домены. Ниже показано, как настроить обработку автоматических ответов в Exchange с помощью командной консоли Exchange.

## Что нужно знать перед началом работы?

  - Осталось времени до завершения: 10 минут

  - Для выполнения этой процедуры можно использовать только командную консоль.

  - Для выполнения этих процедур необходимы соответствующие разрешения. Сведения о необходимых разрешениях см. в статье запись "Удаленный домен" в разделе [Разрешения потока обработки почты](mail-flow-permissions-exchange-2013-help.md).

  - Сочетания клавиш для процедур, описанных в этой статье, приведены в статье [Сочетания клавиш в Центре администрирования Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="Совет" alt="Совет" />Совет.</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Возникли проблемы? Обратитесь за помощью к участникам форумов, посвященных Exchange. Посетите форумы по таким продуктам: <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> или <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.</td>
</tr>
</tbody>
</table>


## Использование командной консоли для настройки автоматических ответов

Командлет **Set-RemoteDomain** используется для настройки свойств удаленного домена.

В этом примере разрешаются автоматические ответы в удаленный домен Contoso. Этот параметр отключен по умолчанию.

    Set-RemoteDomain Contoso -AutoReplyEnabled $true

В этом примере разрешается автоматическая пересылка в удаленный домен. Этот параметр отключен по умолчанию.

    Set-RemoteDomain Contoso -AutoForwardEnabled $true
