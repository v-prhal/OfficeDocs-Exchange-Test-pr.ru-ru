﻿---
title: 'Создание настраиваемой политики DLP: Exchange 2013 Help'
TOCTitle: Создание настраиваемой политики DLP
ms:assetid: b3299a39-9663-41e4-b76e-9d2f7879d486
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/JJ150550(v=EXCHG.150)
ms:contentKeyID: 50487297
ms.date: 04/30/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Создание настраиваемой политики DLP

 

_**Применимо к:** Exchange Online, Exchange Server 2013_

_**Последнее изменение раздела:** 2016-03-18_

Настраиваемая политика предотвращения потери данных (DLP) позволяет устанавливать условия, правила и действия для соответствия конкретным потребностям организации, которые может не охватывать один из уже существующих шаблонов DLP.

Условия правил, доступные в отдельной политике, включают все обычные правила транспорта дополнительно к типам конфиденциальных сведений, приведенным в разделе [Что позволяют искать типы конфиденциальной информации в Exchange](what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md). Дополнительные сведения о правилах транспорта см. в разделах [Правила обработки почтового потока и транспорта](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md) (Exchange 2013) или [Правила потока обработки почты (правила транспорта) в Exchange Online](https://technet.microsoft.com/ru-ru/library/jj919238\(v=exchg.150\)) (Exchange Online).

> [!CAUTION]  
> Перед запуском политики DLP в рабочей среде ее нужно активировать в тестовом режиме. Во время таких тестов рекомендуется настроить образцы почтовых ящиков пользователей и отправить тестовые сообщения, запускающие тестовые политики, для подтверждения результатов. Дополнительные сведения см. в разделе <a href="test-a-mail-flow-rule-exchange-2013-help.md">Тестирование правила обработки почтового потока</a>.


Дополнительные задачи управления, связанные с созданием настраиваемой политики DLP, приведены в разделе [Процедуры защиты от потери данных](dlp-procedures-exchange-2013-help.md)(Exchange 2013) или [Процедуры защиты от потери данных](https://technet.microsoft.com/ru-ru/library/jj938003\(v=exchg.150\)) (Exchange Online).

## Что нужно знать перед началом работы

  - Предполагаемое время для завершения: 60 минут.

  - Для выполнения этих процедур необходимы соответствующие разрешения. Сведения о необходимых разрешениях см. в статье запись "Предотвращение потери данных (DLP)" в разделе [Политика обмена сообщениями и разрешения для соответствия требованиям](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Чтобы создать новую настраиваемую политику DLP, необходимо придерживаться инструкций по установке службы Exchange 2013. Дополнительные сведения о развертывании см. в разделе [Планирование и развертывание](planning-and-deployment-for-exchange-2013-installation-instructions.md).

  - Сочетания клавиш для процедур, описанных в этой статье, приведены в статье [Сочетания клавиш в Центре администрирования Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!NOTE]  
> Так как среды клиентов разнообразны, служба поддержки клиентов Майкрософт (CSS) не может участвовать в разработке или тестировании пользовательских сценариев регулярных выражений (сценариев RegEx). При разработке, тестировании и отладке пользовательских сценариев RegEX подписчикам на Office 365 придется полагаться на ИТ-специалистов организации. Пользователи Office 365 могут также обратиться во внешнюю консультационную службу, такую как Microsoft Consulting Services (MCS). Независимо от того, какие специалисты занимаются разработкой сценариев (внутренние или внешние), инженеры службы CSS, работающие с EXO и EOP, не могут содействовать в создании сценариев RegEx.


> [!TIP]  
> Возникли проблемы? Обратитесь за помощью к участникам форумов, посвященных Exchange. Посетите форумы по таким продуктам: <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> или <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Создание настраиваемой политики DLP без существующих правил с помощью Центра администрирования Exchange (EAC)

1.  В Центре администрирования Exchange откройте раздел **Управление соответствием требованиям** \> **Предотвращение потери данных**. Любые существующие настроенные политики указаны в списке.

2.  Щелкните стрелку рядом с пиктограммой **Добавить**![Значок добавления](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Значок добавления") и выберите **Создать настраиваемую политику**.
    
    > [!IMPORTANT]  
    > Если вместо стрелки щелкнуть пиктограмму <strong>Добавить</strong><img src="images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif" title="Значок добавления" alt="Значок добавления" />, будет создана новая политика на основе шаблона. Для получения дополнительных сведений об использовании шаблонов см. раздел <a href="how-to-new-dlp-data-loss-prevention-policy-template.md">Создание политики защиты от потери данных на основе шаблона</a>.


3.  На странице **Создание настраиваемой политики** заполните следующие поля:
    
    1.  **Имя**   Добавьте имя, которое будет отличать эту политику от других.
    
    2.  **Описание**   Можно добавить необязательное описание этой политики.
    
    3.  **Выберите состояние**   выберите режим или состояние для этой политики. Новая политика не будет полностью включена, если вы не сделаете этого явно. Режим по умолчанию для политики — испытание без уведомлений.

4.  Нажмите кнопку **Сохранить**, чтобы завершить создание ссылочной информации новой политики. Политику добавлено в список всех настроенных политик, хотя с этой новой настраиваемой политикой еще не связаны никакие правила или действия.

5.  Дважды щелкните только что созданную политику или выберите ее и нажмите кнопку **Изменить**![Значок редактирования](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Значок редактирования").

6.  На странице **Изменение политики DLP** нажмите кнопку **Правила**.
    
    Нажмите кнопку **Добавить**![Значок добавления](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Значок добавления"), чтобы добавить новое пустое правило. Можно установить условия с использованием всех обычных правил транспорта дополнительно к типам конфиденциальных сведений.
    
    Во избежание путаницы задайте уникальное имя каждой части политики или правила, когда есть возможность предоставить собственную строку символов. Существует несколько вариантов дополнительных доступных возможностей.
    
    1.  Щелкните стрелку рядом с пиктограммой **Добавить**![Значок добавления](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Значок добавления"), чтобы добавить правило об уведомлении отправителя или разрешении переопределений.
    
    2.  Чтобы удалить правило, выберите его и нажмите кнопку **Удалить**![Значок удаления](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Значок удаления").
    
    3.  Щелкните элемент **Дополнительные параметры**![Значок дополнительных параметров](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Значок дополнительных параметров"), чтобы добавить дополнительные условия и действия для этого правила, в том числе установленные временные границы принудительного применения или влияние на другие правила в данной политике.

7.  Нажмите кнопку **Сохранить**, чтобы закончить изменение политики и сохранить изменения.

Шаблоны политики DLP — один из типов функций Microsoft Exchange, с помощью которой можно конструировать и применять надежную политику и систему соответствия для среды сообщений. Дополнительные сведения о соответствии требованиям см. в разделе [Политика обмена сообщениями и соответствие требованиям](messaging-policy-and-compliance-exchange-2013-help.md) (Exchange 2013) или [Безопасность и соответствие требованиям для Exchange Online](https://technet.microsoft.com/ru-ru/library/jj200706\(v=exchg.150\)).

## Дополнительные сведения

[Защита от потери данных](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[Правила обработки почтового потока и транспорта](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)Exchange 2013

[Правила потока обработки почты (правила транспорта) в Exchange Online](https://technet.microsoft.com/ru-ru/library/jj919238\(v=exchg.150\))Exchange Online

[Интеграция правил конфиденциальной информации с правилами транспорта](integrating-sensitive-information-rules-with-transport-rules-exchange-2013-help.md)

