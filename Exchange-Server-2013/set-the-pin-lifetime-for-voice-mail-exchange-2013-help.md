﻿---
title: 'Задать время жизни ПИН-код голосовой почты: Exchange 2013 Help'
TOCTitle: Задать время жизни ПИН-код голосовой почты
ms:assetid: d17f0bf6-0ad6-40a4-bdd5-f7098f39250d
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/Bb124712(v=EXCHG.150)
ms:contentKeyID: 50556488
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Задать время жизни ПИН-код голосовой почты

 

_**Применимо к:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Последнее изменение раздела:** 2013-02-22_

Можно настроить срок действия ПИН-кода для пользователей с включенной поддержкой единой системы обмена сообщениями. Время жизни ПИН — это максимальный период времени, в течение которого ПИН-код голосового доступа к Outlook будет действовать для получателей с включенной поддержкой единой системы обмена сообщениями. Параметр срока действия ПИН-кода настраивается в политике почтовых ящиков единой системы обмена сообщениями и применяется ко всем пользователям единой системы обмена сообщениями, которые связаны с политикой почтовых ящиков единой системы обмена сообщениями.

Несколько параметров, связанных с ПИН-кодом, можно настроить в политике почтовых ящиков единой системы обмена сообщениями. Срок действия ПИН-кода определяет временной интервал в днях с даты последнего изменения ПИН-кода пользователем голосового доступа к Outlook до даты, когда пользователь снова должен будет изменить свой ПИН-код. Диапазон значений — от 0 до 999, значение по умолчанию — 60 дней. Если значение равно 0, срок действия ПИН-кода пользователя не ограничен. Не рекомендуется указывать для этого параметра значение 0, потому что это значительно снижает безопасность сети.

> [!IMPORTANT]  
> Единая система обмена сообщениями не извещает пользователя о том, что срок действия ПИН-кода истекает.


Сведения о дополнительных задачах, связанных с обеспечением безопасности при помощи ПИН-кода голосового доступа к Outlook, см. в разделе [Процедуры безопасности ПИН-кода](pin-security-procedures-exchange-2013-help.md).

## Что нужно знать перед началом работы

  - Предполагаемое время для завершения: менее 1 минуты.

  - Для выполнения этих процедур необходимы соответствующие разрешения. Сведения о необходимых разрешениях см. в статье Запись «Политики почтовых ящиков единой системы обмена сообщениями» в разделе [Разрешения единой системы обмена сообщениями](unified-messaging-permissions-exchange-2013-help.md).

  - Перед выполнением этих процедур убедитесь, что абонентская группа единой системы обмена сообщениями создана. Дополнительные сведения см. в разделе [Создание абонентской группы единой системы обмена сообщениями](create-a-um-dial-plan-exchange-2013-help.md).

  - Перед выполнением этих процедур убедитесь, что политика почтовых ящиков единой системы обмена сообщениями создана. Дополнительные сведения см. в разделе [Создание политики почтовых ящиков единой системы обмена сообщениями](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Сочетания клавиш для процедур, описанных в этой статье, приведены в статье [Сочетания клавиш в Центре администрирования Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]  
> Возникли проблемы? Обратитесь за помощью к участникам форумов, посвященных Exchange. Посетите форумы по таким продуктам: <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> или <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Что необходимо сделать?

## Настройка срока действия ПИН-кода с помощью Центра администрирования Exchange

1.  В Центре администрирования Exchange последовательно выберите пункты **Единая система обмена сообщениями** \> **Абонентские группы единой системы обмена сообщениями**.

2.  Выберите из списка абонентскую группу единой системы обмена сообщениями, которую необходимо изменить, и нажмите кнопку **Правка**![Значок редактирования](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Значок редактирования").

3.  На странице **Абонентская группа единой системы обмена сообщениями** в разделе **Политики почтовых ящиков единой системы обмена сообщениями** выберите изменяемую политику и нажмите кнопку **Правка**![Значок редактирования](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Значок редактирования").

4.  На вкладке **Политики ПИН-кода** в поле **Включить срок действия ПИН-кода (дней)** введите значение от 0 до 999.

5.  Нажмите кнопку **Сохранить**.

## Настройка срока действия ПИН-кода с помощью командной консоли

В этом примере количество дней, в течение которых пользователи голосового доступа к Outlook, связанные с политикой почтовых ящиков единой системы обмена сообщениями с именем `MyUMMailboxPolicy`, могут использовать ПИН-код, задается равным 30.

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -PINLifetime 30

В этом примере настраиваются следующие параметры, относящиеся к ПИН-кодам, для пользователей голосового доступа к Outlook, связанным с политикой почтовых ящиков единой системы обмена сообщениями `MyUMMailboxPolicy`.

  - Количество неудачных попыток входа до сброса ПИН-кода пользователя задается равным 3,

  - Максимальное количество попыток входа в систему задается равным 5.

  - минимальная длина ПИН-кода задается равной 9 цифрам,

  - срок действия ПИН-кода задается равным 40 дням.

<!-- end list -->

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -LogonFailuresBeforePINReset 3
    -MaxLogonAttempts 5 -MinPINLength 9 -PINLifetime 40

