﻿---
title: 'Настраиваемое приветствие для пользователей голосового доступа к Outlook'
TOCTitle: Включение настраиваемого приветствия для пользователей голосового доступа к Outlook
ms:assetid: abd418ec-2c65-4720-859d-c11a2698dc06
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/Bb124125(v=EXCHG.150)
ms:contentKeyID: 50556468
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Включение настраиваемого приветствия для пользователей голосового доступа к Outlook

 

_**Применимо к:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Последнее изменение раздела:** 2016-12-09_

По умолчанию каждая абонентская группа серверов единой системы обмена сообщениями использует стандартный WAV-файл для приветствия, которое воспроизводится для абонентов, включая пользователей голосового доступа к Outlook, набирающих заданный номер голосового доступа к Outlook. Тем не менее, вы можете создать WMA- или WAV-файл для приветствия, а затем использовать его в абонентской группе единой системы обмена сообщениями.

Например, может потребоваться заменить приветствие по умолчанию другим, которое больше подходит компании, например: "Добро пожаловать в систему голосового доступа к Outlook банка Woodgrove Bank". Для этого необходимо сначала записать пользовательское приветствие и сохранить его как WAV- или WMA-файл. Затем нужно настроить абонентскую группу с использованием настроенного приветствия.

Дополнительные сведения о параметрах меню, доступных для пользователей голосового доступа к Outlook просмотрите краткий справочник для Outlook голосового доступа к которой доступен из [Центра загрузки Майкрософт](https://go.microsoft.com/fwlink/p/?linkid=272767).

Дополнительные задачи управления, связанные с абонентскими группами единой системы обмена сообщениями, см. в разделе [Процедуры плана телефонным единой системы обмена СООБЩЕНИЯМИ](um-dial-plan-procedures-exchange-2013-help.md).

## Что нужно знать перед началом работы

  - Предполагаемое время для завершения: менее 1 минуты.

  - Для выполнения этих процедур необходимы соответствующие разрешения. Сведения о необходимых разрешениях см. в статье запись "Абонентская группа единой системы обмена сообщениями" в разделе [Разрешения единой системы обмена сообщениями](unified-messaging-permissions-exchange-2013-help.md).

  - Перед выполнением этих процедур убедитесь, что абонентская группа единой системы обмена сообщениями создана. Дополнительные сведения см. в разделе [Создание абонентской группы единой системы обмена сообщениями](create-a-um-dial-plan-exchange-2013-help.md).

  - Сочетания клавиш для процедур, описанных в этой статье, приведены в статье [Сочетания клавиш в Центре администрирования Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]  
> Возникли проблемы? Обратитесь за помощью к участникам форумов, посвященных Exchange. Посетите форумы по таким продуктам: <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> или <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Что необходимо сделать?

## Используйте Центр администрирования Exchange для включения настраиваемого приветствия

1.  В Центре администрирования Exchange последовательно выберите пункты **Единая система обмена сообщениями** \> **Абонентские группы единой системы обмена сообщениями**.

2.  Выберите из списка абонентскую группу единой системы обмена сообщениями, которую необходимо изменить, и нажмите кнопку **Правка**![Значок редактирования](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Значок редактирования").

3.  На странице **Абонентская группа единой системы обмена сообщениями** нажмите кнопку **Настроить**.

4.  В разделе **Голосовой доступ к Outlook** в поле **Приветствие** нажмите кнопку **Изменить**, а затем — кнопку **Обзор**, чтобы найти файл.
    
    > [!IMPORTANT]  
    > Файл, используемый для приветствия, должен иметь формат WMA или WAV.


5.  Указав расположение файла, нажмите кнопку **Открыть**, а затем — **Сохранить**.

## Использование командной консоли для включения настраиваемого приветствия

В следующем примере задействуется приветствие, которое представляет собой файл C:\\UMPrompts\\welcome.wav, для абонентской группы единой системы обмена сообщениями `MyUMDialPlan`.

    Set-UMDialPlan -Identity MyUMDialPlan -WelcomeGreetingEnabled $true -WelcomeGreetingFilename c:\UMPrompts\welcome.wav

