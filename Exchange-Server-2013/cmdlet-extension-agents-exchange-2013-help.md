﻿---
title: 'Агенты расширения командлета: Exchange 2013 Help'
TOCTitle: Агенты расширения командлета
ms:assetid: 0257790d-3988-46c3-8882-25ca11559e84
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/Dd335054(v=EXCHG.150)
ms:contentKeyID: 50556326
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Агенты расширения командлета

 

_**Применимо к:** Exchange Server 2013_

_**Последнее изменение раздела:** 2015-03-09_

Агенты расширения командлетов — это компоненты Microsoft Exchange Server 2013, вызываемые с помощью командлетов Exchange 2013 при запуске командлета. Агенты расширения командлета расширяют возможности командлетов, которые их вызывают, при обработке данных или выполнении дополнительных действий в зависимости от требований командлета. Агенты расширения командлетов доступны на любой роли сервера.

Агенты позволяют изменять, заменять или расширять функции командлетов консоли управления Exchange. Агент позволяет указать значение необходимого параметра, которое не указано в команде, заменить определенное пользователем значение, выполнять другие действия за пределами рабочего потока командлета во время работы командлета и т. д.

Например, командлет **New-Mailbox** принимает параметр *Database*, который указывает базу данных почтовых ящиков, в которой необходимо создать новый почтовый ящик. В Microsoft Exchange Server 2007, если параметр *Database* не указан при запуске командлета **New-Mailbox**, происходит ошибка команды. При этом в Exchange 2013 командлет **New-Mailbox** при запуске вызывает агент `Mailbox Resources Management`. Если параметр *Database* не указан, агент `Mailbox Resources Management` автоматически определяет подходящую базу данных почтовых ящиков, в которой необходимо создать новый почтовый ящик, и добавляет значение в параметр *Database*.

Агенты расширения командлетов можно вызывать только в командлетах Exchange 2013 и Microsoft Exchange Server 2010. Командлеты Exchange 2007 и командлеты, предоставленные другими продуктами Майкрософт и сторонних производителей, не могут вызывать агенты расширения командлетов. Сценарии также не позволяют вызывать агенты расширения командлетов напрямую. Тем не менее, если сценарии содержат командлеты Exchange 2013, эти командлеты позволяют вызывать агенты расширения командлетов.

Необходимы сведения о других задачах управления, связанных с агентами расширения командлетов? См. раздел [Управление агентами расширения командлетов](manage-cmdlet-extension-agents-exchange-2013-help.md).

## Приоритет агентов

Приоритет агента определяет порядок вызова агентов во время работы командлета. Агент с более высоким приоритетом (ближе к 0) вызывается в первую очередь. Приоритет агента очень важен, когда два или более агентов пытаются установить значение одного свойства. Свойство устанавливает агент с наиболее высоким приоритетом, а все последующие попытки установки этого же свойства агентами с более низким приоритетом пропускаются. Например, если свойство **Name** объекта изменено агентом с приоритетом 3, и другой агент с приоритетом 6 попытается изменить этот же объект, изменения агента с приоритетом 6 будут пропущены.

Чтобы использовать `Scripting agent` для установки значений свойств, которые могут быть установлены другими агентами с более высоким приоритетом, выполните следующие действия.

  - Отключите агент, который в настоящее время устанавливает свойство.

  - Установите для `Scripting agent` приоритет выше, чем у существующего агента, который необходимо заменить.

  - Не изменяйте приоритеты агентов и убедитесь, что сценарий, запущенный в `Scripting agent`, учитывает значение, предоставленное другими агентами.

> [!CAUTION]  
> Изменение приоритета или замена функций встроенного агента являются дополнительными операциями. Убедитесь, что имеете полное представление о производимых изменениях.


Дополнительные сведения об изменении приоритета агента см. в разделе [Управление агентами расширения командлетов](manage-cmdlet-extension-agents-exchange-2013-help.md).

## Встроенные агенты

Exchange 2013 содержит несколько агентов, которые можно вызвать при запуске командлета. В следующей таблице перечислены агенты, их порядок и состояние по умолчанию (включен или отключен). Можно добавлять и удалять агенты на сервере Exchange 2013. Однако также можно воспользоваться `Scripting agent` для запуска сценариев Windows PowerShell с целью расширения функциональности командлетов, которые его используют. Дополнительные сведения о `Scripting agent` см. в разделе "Агент сценария" далее в этом разделе.

Можно включать или отключать агенты или изменять приоритет агентов, чтобы заменить функции определенного агента на функции настраиваемого сценария, вызываемого с помощью `Scripting agent`. Однако некоторые агенты нельзя отключить. Агенты, которые невозможно отключить, называются *системными*. Свойство *IsSystem* у них задано как `$True`. В следующей таблице приведены сведения об агентах расширения командлетов Exchange 2013, включая системные.

Конфигурация агентов хранится на уровне организации. При включении, отключении агента или установке его приоритета изменение конфигурации агента выполняется на каждом сервере организации. Исключением является добавление сценариев в `Scripting agent`. Обновление сценариев необходимо выполнять отдельно на каждом сервере. Дополнительные сведения о настройке сценариев для использования с `Scripting agent` см. в разделе "Агент сценария" далее в этом разделе.

> [!CAUTION]  
> В случае непонимания принципов работы агентов и способов их взаимодействия с командлетами Exchange изменение приоритета агентов, их включение или отключение может привести к непредвиденным последствиям. Перед изменением конфигурации агента убедитесь, что имеете полное представление о выполняемых изменениях и желаемых результатах, и проверьте правильность работы настраиваемого сценария.


### Агенты расширения командлета Exchange 2013

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Имя агента</th>
<th>Приоритет</th>
<th>Включено по умолчанию</th>
<th>Системный агент</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>Admin Audit Log agent</code></p></td>
<td><p>255</p></td>
<td><p>Истина</p></td>
<td><p>Да</p></td>
</tr>
<tr class="even">
<td><p><code>Scripting agent</code></p></td>
<td><p>6</p></td>
<td><p>Ложь</p></td>
<td><p>Нет</p></td>
</tr>
<tr class="odd">
<td><p><code>Mailbox Resources Management agent</code></p></td>
<td><p>5</p></td>
<td><p>Истина</p></td>
<td><p>Нет</p></td>
</tr>
<tr class="even">
<td><p><code>OAB Resources Management agent</code></p></td>
<td><p>4</p></td>
<td><p>Истина</p></td>
<td><p>Нет</p></td>
</tr>
<tr class="odd">
<td><p><code>Query Base DN agent</code></p></td>
<td><p>3</p></td>
<td><p>Истина</p></td>
<td><p>Нет</p></td>
</tr>
<tr class="even">
<td><p><code>Provisioning Policy agent</code></p></td>
<td><p>2</p></td>
<td><p>Истина</p></td>
<td><p>Нет</p></td>
</tr>
<tr class="odd">
<td><p><code>Rus agent</code></p></td>
<td><p>1</p></td>
<td><p>Истина</p></td>
<td><p>Нет</p></td>
</tr>
<tr class="even">
<td><p><code>Mailbox Creation Time agent</code></p></td>
<td><p>0</p></td>
<td><p>Истина</p></td>
<td><p>Нет</p></td>
</tr>
</tbody>
</table>


## Агент сценария

Агент расширения командлета `Scripting agent` в Exchange 2013 позволяет вставлять собственную логику сценария в алгоритм выполнения командлетов Exchange. С помощью `Scripting agent` можно добавлять условия, переопределять значения и настраивать функцию отчетов.

> [!CAUTION]  
> При включении агента расширения командлета <code>Scripting agent</code> он вызывается при каждом запуске командлета на сервере под управлением Exchange 2013. Это относится не только к командлетам, запускаемым пользователем в командной консоли Exchange, но и к командлетам, запускаемым службами Exchange и центром администрирования Exchange. Перед копированием обновленного файла конфигурации на серверы Exchange 2013 и включением агента расширения командлета <code>Scripting agent</code> рекомендуется протестировать сценарий и проверить все изменения, внесенные в файл конфигурации.


При каждом запуске командлета Exchange вызывается агент расширения командлета `Scripting agent`. При вызове этого агента командлет проверяет, необходимо ли выполнение какого-либо сценария. Если для командлета настроено выполнение сценария, командлет пытается вызвать любой из интерфейсов API, определенных в сценарии. В сценарии доступны следующие API, вызываемые в указанном ниже порядке.

1.  **ProvisionDefaultProperties**   Этот API используется для настройки значений свойств объектов при их создании. При установке значения оно возвращается командлету, который устанавливает его для свойства. Администратор может задать значения для свойств, если они не были указаны пользователем, или может переопределить значение, указанное пользователем. Этот API учитывает значения, установленные агентами с более высоким приоритетом. Агент расширения командлета `Scripting agent` не переопределяет значения, установленные агентами с более высоким приоритетом.

2.  **UpdateAffectedIConfigurable**   Этот API используется для установки значений свойств объектов после завершения всех других процессов обработки и до вызова интерфейса API `Validate`. Этот API учитывает значения, установленные агентами с более высоким приоритетом. Агент расширения командлета `Scripting agent` не переопределяет значения, установленные агентами с более высоким приоритетом.

3.  **Validate**   Этот API используется для проверки значений свойств объектов, которые будут установлены командлетом. Он вызывается непосредственно перед записью командлетом каких-либо данных. Проверку можно настроить таким образом, чтобы командлет мог пройти или не пройти ее. Если командлет проходит проверку в этом API, то ему разрешается запись данных. Если командлет не проходит проверку, он возвращает ошибку, определенную в этом API.

4.  **OnComplete**   Этот API используется после завершения всех операций обработки командлета. Он может использоваться для выполнения задач после обработки, таких как запись данных во внешнюю базу данных.

> [!NOTE]  
> Агент расширения командлета <code>Scripting agent</code> не вызывается при запуске командлетов с командой <code>Get</code>.


## Файл конфигурации агента сценария

Файл конфигурации `Scripting agent` содержит все сценарии, которые требуется предоставить `Scripting agent` для запуска. Сценарии в файле конфигурации заключены в тегах XML, которые определяют начало и конец сценария, а также различные входные параметры, необходимые для передачи данных в сценарий. Сценарии пишутся по синтаксическим правилам Windows PowerShell. В файле конфигурации, имеющем формат XML, используются элементы и атрибуты, приведенные в следующей таблице.

### Атрибуты файла конфигурации агента сценария

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Элемент</th>
<th>Атрибут</th>
<th>Описание</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>Configuration</code></p></td>
<td><p>Неприменимо</p></td>
<td><p>Этот элемент содержит все сценарии, которые могут выполняться агентом расширения командлета <code>Scripting agent</code>. Тег <code>Feature</code> является дочерним для этого тега.</p>
<p>В файле конфигурации существует только один тег <code>Configuration</code>.</p></td>
</tr>
<tr class="even">
<td><p><code>Feature</code></p></td>
<td><p>Неприменимо</p></td>
<td><p>Этот элемент содержит набор сценариев, относящихся к какой-либо функции. Каждый сценарий, определенный в дочернем теге <code>ApiCall</code>, расширяет определенный участок конвейера выполнения командлета. В этом теге содержатся атрибуты <code>Name</code> и <code>Cmdlets</code>.</p>
<p>Может существовать несколько тегов <code>Feature</code> на каждый тег <code>Configuration</code>.</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p><code>Name</code></p></td>
<td><p>Этот атрибут содержит имя функции. Этот атрибут позволяет определить функцию, которая расширяется сценарием, содержащимся в теге.</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p><code>Cmdlets</code></p></td>
<td><p>В этом атрибуте содержится список командлетов Exchange, которые будут использоваться набором сценариев в этом расширении функции. Можно указать несколько командлетов, разделяя их запятыми.</p></td>
</tr>
<tr class="odd">
<td><p><code>ApiCall</code></p></td>
<td><p>Неприменимо</p></td>
<td><p>Этот элемент содержит сценарии, которые могут расширять участок конвейера выполнения командлета. Каждый сценарий определяется именем вызова API в расширяемом конвейере выполнения командлета. Ниже приведены имена API, которые могут быть расширены.</p>
<ul>
<li><p><code>ProvisionDefaultProperties</code></p></li>
<li><p><code>UpdateAffectedIConfigurable</code></p></li>
<li><p><code>Validate</code></p></li>
<li><p><code>OnComplete</code></p></li>
</ul></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p><code>Name</code></p></td>
<td><p>Этот атрибут включает в себя имя вызова API, который расширяет конвейер выполнения командлета.</p></td>
</tr>
<tr class="odd">
<td><p><code>Common</code></p></td>
<td><p>Неприменимо</p></td>
<td><p>Этот элемент содержит функции, которые могут использоваться любым сценарием в файле конфигурации.</p></td>
</tr>
</tbody>
</table>


На каждом сервере Exchange 2013 содержится пример файла ScriptingAgentConfig.xml.sample в папке \<*installation path*\>\\V15\\Bin\\CmdletExtensionAgents. При включении агента расширения командлета «Агент сценария» имя этого файла необходимо изменить на ScriptingAgentConfig.xml на каждом сервере Exchange 2013. Пример файла конфигурации содержит образцы сценариев, которые помогут понять правила добавления сценариев в файл конфигурации.

После добавления сценария в файл конфигурации или при внесении изменений в этот файл его необходимо обновить на каждом сервере Exchange 2013 в организации. Это необходимо для того, чтобы на каждом сервере содержалась обновленная версия сценариев, выполняемых агентом расширения командлета `Scripting Agent`.

Некоторые символы, обычно используемые в сценариях, также имеют определенное значение в языке XML. Для использования этих символов в сценарии необходимо использовать escape-последовательности. Например, для следующих символов используются escape-последовательности.

  - Вместо символа «больше, чем» (`>`) используйте `&gt;`

  - Вместо символа «меньше, чем» (`<`) используйте `$lt;`

  - Вместо амперсанда (`&`) используйте `&amp;`

## Включение агента сценария

По умолчанию агент расширения командлета `Scripting agent` отключен. При включении `Scripting agent` он включается для всей организации Exchange 2013. Перед включением `Scripting agent` убедитесь, что файл конфигурации `Scripting agent` был правильно переименован и обновлен пользовательскими сценариями на каждом сервере Exchange 2013. Вы получите сообщение об ошибке при каждом запуске командлета, если неправильно переименовали файл конфигурации или не скопировали файл конфигурации на этот компьютер с другого сервера Exchange 2013.

Чтобы включить `Scripting agent`, выполните следующие действия.

1.  Переименуйте файлScriptingAgentConfig.xml.sample в папке **\<путь\_установки\>\\V15\\Bin\\CmdletExtensionAgents** в файл ScriptingAgentConfig.xml на каждом сервере Exchange 2013 в организации.
    
    > [!NOTE]  
    > Файл конфигурации можно скопировать с одного сервера Exchange 2013 на другие серверы Exchange 2013. Перед копированием файла конфигурации убедитесь, что он обновлен.


2.  Добавьте свой сценарий в переименованный файл конфигурации на каждом сервере Exchange 2013 в организации.

3.  Включите агент расширения командлета `Scripting agent`. Дополнительные сведения о включении агентов расширения командлета см. в разделе [Управление агентами расширения командлетов](manage-cmdlet-extension-agents-exchange-2013-help.md).

## Приоритет агента сценария

По умолчанию агент расширения командлета `Scripting agent` запускается после каждого второго агента, кроме агента `Scripting agent`. Если необходимо, чтобы существующий агент был заменен созданным сценарием, отключите другой агент или измените приоритет обоих агентов, чтобы агент `Scripting agent` запускался первым. Дополнительные сведения о способах отключения или изменения приоритета агентов см. в разделе [Управление агентами расширения командлетов](manage-cmdlet-extension-agents-exchange-2013-help.md).

