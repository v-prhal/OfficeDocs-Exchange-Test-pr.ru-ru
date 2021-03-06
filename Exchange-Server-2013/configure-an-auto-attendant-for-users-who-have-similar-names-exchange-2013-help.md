﻿---
title: 'Настройка автосекретаря для пользователей со схожими именами'
TOCTitle: Настройка автосекретаря для пользователей со схожими именами
ms:assetid: 2e7318a0-67f9-4d7b-8300-5f0ef77656a8
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/Aa997135(v=EXCHG.150)
ms:contentKeyID: 52059121
ms.date: 04/30/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Настройка автосекретаря для пользователей со схожими именами

 

_**Применимо к:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Последнее изменение раздела:** 2012-12-16_

Метод настройки для пользователей со сходными именами можно выбрать, используя параметры автосекретаря **Адресная книга и доступ оператора**, или их можно оставить по умолчанию и настроить этот параметр на абонентской группе, связанной с автосекретарем. По умолчанию автосекретарь не может устранить неоднозначность при выборе из нескольких пользователей со сходными именами, так как параметр по умолчанию для автосекретаря — **Наследовать из абонентской группы**.

> [!NOTE]  
> Чтобы включаемая информация о пользователях со сходными именами работала правильно, необходимо указать должность, отдел и сведения о местоположении получателей в вашей организации Microsoft Exchange.


Дополнительные задачи управления, связанные с автосекретарями единой системы обмена сообщениями, см. в разделе [Процедуры автосекретаря единой системы обмена сообщениями](um-auto-attendant-procedures-exchange-2013-help.md).

## Что нужно знать перед началом работы

  - Предполагаемое время для завершения: менее 1 минуты.

  - Для выполнения этих процедур необходимы соответствующие разрешения. Сведения о необходимых разрешениях см. в статье Запись «Автосекретари единой системы обмена сообщениями» в разделе [Разрешения единой системы обмена сообщениями](unified-messaging-permissions-exchange-2013-help.md).

  - Перед выполнением этих процедур убедитесь, что абонентская группа единой системы обмена сообщениями создана. Дополнительные сведения см. в разделе [Создание абонентской группы единой системы обмена сообщениями](create-a-um-dial-plan-exchange-2013-help.md).

  - Перед выполнением этих процедур убедитесь, что автосекретарь единой системы обмена сообщениями создан. Дополнительные сведения см. в разделе [Создание автосекретаря единой системы обмена сообщениями](create-a-um-auto-attendant-exchange-2013-help.md).

  - Сочетания клавиш для процедур, описанных в этой статье, приведены в статье [Сочетания клавиш в Центре администрирования Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]  
> Возникли проблемы? Обратитесь за помощью к участникам форумов, посвященных Exchange. Посетите форумы по таким продуктам: <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> или <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Что необходимо сделать?

## Использование Центра администрирования Exchange для настройки автосекретаря единой системы обмена сообщениями для пользователей со сходными именами

1.  В Центре администрирования Exchange последовательно выберите пункты **Единая система обмена сообщениями** \> **Абонентские группы единой системы обмена сообщениями**. Выберите из списка абонентскую группу единой системы обмена сообщениями, которую необходимо изменить, и нажмите кнопку **Правка**![Значок редактирования](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Значок редактирования").

2.  На странице **Абонентская группа единой системы обмена сообщениями** в разделе **Автосекретари единой системы обмена сообщениями** выберите автосекретаря единой системы обмена сообщениями, которого необходимо настроить, а затем нажмите кнопку **Изменить**![Значок редактирования](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Значок редактирования").

3.  На странице **Автосекретари единой системы обмена сообщениями** нажмите кнопку **Адресная книга и доступ оператора**, а затем в разделе **Включаемая информация для пользователей со сходными именами**, выберите одно из следующих действий.
    
      - **Должность**   Автосекретарь будет добавлять должность каждого пользователя при выводе совпадений.
    
      - **Отдел**   Автосекретарь будет добавлять отдел каждого пользователя при выводе совпадений.
    
      - **Местоположение**   Автосекретарь будет добавлять местоположение каждого пользователя при выводе совпадений.
    
      - **Нет**. Автосекретарь не будет добавлять дополнительные сведения при перечислении совпадений.
    
      - **Запросить псевдоним**. Автосекретарь будет запрашивать у абонента псевдоним пользователя.
    
      - **Наследовать из абонентской группы**. Автосекретарь будет использовать параметр по умолчанию, заданный для абонентской группы, которая связана с этим автосекретарем.

4.  Нажмите кнопку **Сохранить**.

## Использование командной консоли для настройки автосекретаря единой системы обмена сообщениями для пользователей со сходными именами

В этом примере показана информация, которую следует включить для пользователей со сходными именами при запросе псевдонима для автосекретаря единой системы обмена сообщениями с именем `MyUMAutoAttendant`.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -MatchedNameSelectionMethod PromptForAlias

В этом примере показана информация, которую для пользователей со сходными именами следует добавить в должность пользователей. Кроме того, здесь показано, как включить поиск по именам, а также дать возможность абонентам, которые вызывают автосекретаря, с помощью нажатия клавиши "\*" получать приветствие от службы голосового доступа Outlook для автосекретаря единой системы обмена сообщениями с именем `MyUMAutoAttendant`.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -MatchedNameSelectionMethod Title -NameLookupEnabled $true -StarOutToDialPlanEnabled $true

