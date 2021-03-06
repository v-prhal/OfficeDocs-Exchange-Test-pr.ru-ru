﻿---
title: 'Exchange 2013: управление параметрами UM на сервере клиентского доступа'
TOCTitle: Управление параметрами единой системы обмена сообщениями на сервере клиентского доступа
ms:assetid: 08667911-fa86-404e-84b1-65cedd94d579
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/JJ673507(v=EXCHG.150)
ms:contentKeyID: 50556330
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Управление параметрами единой системы обмена сообщениями на сервере клиентского доступа

 

_**Применимо к:** Exchange Server 2013, Exchange Server 2016_

_**Последнее изменение раздела:** 2013-04-09_

После установки сервера клиентского доступа, который работает под управлением службы маршрутизатора вызовов единой системы обмена сообщениями Microsoft Exchange, можно настроить несколько параметров, включая количество одновременных вызовов, прослушивающие порты TCP и TLS, состояние и режим запуска.

> [!NOTE]  
> Чтобы абонентская группа единой системы обмена сообщениями могла обрабатывать вызовы для данной системы, в эту группу не нужно предварительно добавлять серверы клиентского доступа. Исключение составляют случаи интеграции единой системы обмена сообщениями и серверов Microsoft Office Communications Server 2007 R2 или Microsoft Lync Server. По умолчанию все серверы клиентского доступа в организации способны отвечать на входящие вызовы.


Дополнительные сведения, связанные с единой системой обмена сообщениями и серверами клиентского доступа, см. в разделе [Процедуры служб единой системы обмена СООБЩЕНИЯМИ](um-services-procedures-exchange-2013-help.md).

## Что нужно знать перед началом работы

  - Предполагаемое время для завершения: 5 минут.

  - Для выполнения этих процедур необходимы соответствующие разрешения. Сведения о необходимых разрешениях см. в статье подраздел «Сервер клиентского доступа (служба маршрутизатора вызовов единой системы обмена сообщениями)» в разделе [Разрешения единой системы обмена сообщениями](unified-messaging-permissions-exchange-2013-help.md).

  - Убедитесь, что сервер клиентского доступа установлен либо на том же компьютере, что и сервер почтовых ящиков, либо на отдельном компьютере.

  - Сочетания клавиш для процедур, описанных в этой статье, приведены в статье [Сочетания клавиш в Центре администрирования Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]  
> Возникли проблемы? Обратитесь за помощью к участникам форумов, посвященных Exchange. Посетите форумы по таким продуктам: <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> или <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Что необходимо сделать?

## Использовать командную консоль для настройки свойств единой системы обмена сообщениями на сервере клиентского доступа

В этом примере показано, как удалить сервер клиентского доступа с именем `MyClientAccessServer` из всех абонентских групп на основе протокола SIP.

    Set-UMCallRouterSettings -DialPlans $null - Server MyClientAccessServer

В этом примере показано, как добавить сервер клиентского доступа с именем `MyClientAccessServer` в абонентскую группу на основе протокола SIP с именем `MySIPDialPlan`, а также установить максимальное число входящих голосовых вызовов.

    Set-UMCallRouterSettings -DialPlans MySIPDialPlan -MaxCalls 150 -Server MyClientAccessServer

В этом примере показано, как установить значение 5077 для прослушивающего порта SIP TCP, а также задать двойной режим запуска на сервере клиентского доступа с именем `MyClientAccessServer`.

    Set-UMCallRouterSettings  -Server MyClientAccessServer-SipTCPListeningPort 5077 -UMStartUpMode -Dual 

## Использовать командную консоль для просмотра свойств сервера клиентского доступа

В этом примере отображается список всех серверов клиентского доступа.

    Get-UMCallRouterSettings

В этом примере отображается форматированный список свойств для сервера клиентского доступа.

    Get-UMCallRouterSettings | Format-List

