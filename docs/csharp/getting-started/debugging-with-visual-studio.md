---
title: "Отладка приложения Hello World на C# в Visual Studio 2017"
description: "Сведения об отладке приложения Hello World, написанного на C#, в Visual Studio 2017."
keywords: ".NET Core, консольное приложение .NET Core, отладка .NET Core"
author: BillWagner
ms.author: wiwagn
ms.date: 04/17/2017
ms.topic: article
ms.prod: .net-core
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: cb213625-cc60-438b-9b9e-49aed0e4a974
ms.translationtype: Human Translation
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: a3ed6572d0c8f64f89f77527aa21df454b30982c
ms.contentlocale: ru-ru
ms.lasthandoff: 07/28/2017

---

# <a name="debugging-your-c-hello-world-application-with-visual-studio-2017"></a>Отладка приложения Hello World на C# в Visual Studio 2017

Итак, вы уже создали и запустили простое консольное приложение, воспользовавшись инструкциями из раздела [Создание приложения Hello World на C# с помощью .NET Core в Visual Studio 2017](.\with-visual-studio.md). После создания и компиляции приложения можно приступить к тестированию. Visual Studio включает широкий набор инструментальных средств, которые можно использовать для тестирования приложений и устранения неполадок.

## <a name="debugging-in-debug-mode"></a>Отладка в режиме отладки

В Visual Studio по умолчанию используются две конфигурации сборки — *Отладка* и *Выпуск*. Используемая конфигурация сборки отображается на панели инструментов. На следующем рисунке показана панель инструментов Visual Studio с активным режимом **отладки**.

   ![Панель инструментов Visual Studio](./media/debugging-with-visual-studio/toolbar1.png)

Тестирование всегда следует начинать с режима отладки. В режиме отладки компилятор отключает большинство инструментов оптимизации и предоставляет более подробные сведения о процессе сборки.

## <a name="setting-a-breakpoint"></a>Задание точки останова

Запустите программу в режиме отладки и попробуйте использовать некоторые функции отладки:

1. *Точка останова* приостанавливает выполнение приложения на инструкции, *предшествующей* той строке, в которой установлена точка останова. Установите точку останова в строке `Console.WriteLine("\nHello, {0}, on {1:d} at {1:t}", name, date);`. Для этого щелкните в левом поле этой строки в окне редактирования кода или выберите эту строку и затем пункт меню **Отладка** > **Точка останова**. Как видно на следующем рисунке, строку с точкой останова Visual Studio обозначает подсветкой текста и красным кругом в ее левом поле.

   ![Окно приложения Visual Studio с установленной точкой останова](./media/debugging-with-visual-studio/setbreakpoint.png)

1. Запустите программу в режиме отладки. Для этого нажмите кнопку **HelloWorld** с зеленой стрелкой на панели инструментов, нажмите клавишу F5 или выберите пункт меню **Отладка** > **Начать отладку**.

1. Когда программа запросит имя, введите любую строку в окне консоли и нажмите клавишу ВВОД.

1. Выполнение программы остановится, когда будет достигнута точка останова, то есть перед выполнением метода `Console.WriteLine`. В окне **Видимые** отображаются значения всех переменных, которые используются рядом с текущей строкой. В окне **Локальные** отображаются значения переменных, которые определены в текущем выполняемом методе.

   ![Окно приложения Visual Studio](./media/debugging-with-visual-studio/break.png)

1. Вы можете изменить значения переменных и посмотреть, как это повлияет на работу программы. Если **окно интерпретации** не отображается, откройте его, выбрав пункт меню **Отладка** > **Окна** > **Интерпретация**. **Окно интерпретации** позволяет взаимодействовать с приложением, которое вы отлаживаете.

1. Вы можете изменять значения переменных и отслеживать изменения. Введите `name = "Gracie"` в **окно интерпретации** и нажмите клавишу ВВОД.

1. Введите `date = new DateTime(2016,11,01,11,59,00)` в **окно интерпретации** и нажмите клавишу ВВОД.

   В **окне интерпретации** отображается значение строковой переменной и свойства значения @System.DateTime. Кроме того, значения переменных обновляются в окнах **Видимые** и **Локальные**.

   ![Окно "Видимые" и окно интерпретации](./media/debugging-with-visual-studio/autosimmediate.png)

1. Возобновите выполнение программы, нажав кнопку **Продолжить** на панели инструментов или выбрав пункт меню **Отладка** > **Продолжить**. Значения, отображаемые в окне консоли, соответствуют изменениям, произведенным в **окне интерпретации**.

   ![Окно консоли с набранным значением "Jack" в ответ на вопрос "What is your name?", за которым следует надпись "Hello Gracie" и дата и время "11/1/2016 11:59am"](./media/debugging-with-visual-studio/changed.png)

1. Нажмите любую клавишу, чтобы выйти из приложения и закрыть режим отладки.

## <a name="setting-a-conditional-breakpoint"></a>Установка условной точки останова

Ваша программа отображает строку, которую вводит пользователь. Что произойдет, если пользователь ничего не введет? Это можно проверить с помощью одной из полезных функций отладки — *условной точки останова*. Условная точка останова прерывает выполнение программы, если соблюдены одно или несколько условий.

Чтобы проверить поведение программы в случае, когда пользователь не вводит текст, задайте условную точку останова следующим образом.

1. Щелкните правой кнопкой мыши красную точку, обозначающую точку останова. В контекстном меню выберите **Условия**. Откроется диалоговое окно **Параметры точки останова**. Установите флажок **Условия**.

   ![Панель параметров точки останова](./media/debugging-with-visual-studio/breakpointsettings.png)

1. В поле **Выражение условия** замените "e.g. x == 5" на следующее условие:

   ```csharp
   String.IsNullOrEmpty(name)
   ```

   Здесь мы проверяем условие выполнения. Также можно указать *количество обращений* (в этом случае выполнение программы будет прерываться до тех пор, пока не будет достигнуто заданное количество обращений) или *условие фильтра* (в этом случае выполнение программы будет прерываться на основе таких атрибутов, как идентификатор потока, имя процесса и имя потока).

1. Нажмите кнопку **Закрыть**, чтобы закрыть диалоговое окно.

1. Запустите программу в режиме отладки.

1. Когда в окне консоли появится предложение ввести имя, просто нажмите клавишу ВВОД.

1. Так как указанное нами условие соблюдается (`name` имеет значение `null` или [`String.Empty`](xref:System.String.Empty)), выполнение программы будет приостановлено при достижении точки останова, то есть перед выполнением метода `Console.WriteLine`.

1. Выберите окно **Локальные**, в котором отображаются значения локальных переменных для текущего выполняемого метода (в нашем примере это метод `Main`). Обратите внимание, что переменная `name` имеет значение `""`, или [`String.Empty`](xref:System.String.Empty).

1. Убедитесь в том, что переменная содержит пустую строку, введя следующую инструкцию в **окне интерпретации**. Результат равен `true`.

   ```csharp
   ? name == String.Empty
   ```

   ![Значение true в окне интерпретации после выполнения инструкции](./media/debugging-with-visual-studio/emptystring.png)

1. Нажмите кнопку **Продолжить** на панели инструментов, чтобы возобновить выполнение программы.

1. Нажмите любую клавишу, чтобы закрыть окно консоли и закрыть режим отладки.

1. Снимите точку останова. Для этого щелкните точку в левом поле окна изменения кода или установите курсор в строку с точкой останова и выберите пункт меню **Отладка > Точка останова**.

## <a name="stepping-through-a-program"></a>Пошаговое выполнение программы

Visual Studio позволяет выполнять программу пошагово, отслеживая результат ее выполнения. Обычно для использования этой функции задают точку останова и затем пошагово выполняют небольшой фрагмент программного кода. Так как наша программа невелика, давайте пошагово выполним всю программу. Для этого сделайте следующее:

1. В строке меню выберите **Отладка** > **Выполнять по шагам** или нажмите клавишу F11. Следующая выполняемая строка будет выделена, и рядом с ней появится стрелка.

   ![Окно Visual Studio](./media/debugging-with-visual-studio/stepinto1.png)

   На этом этапе в окне **Видимые** будет показано, что в программе определена всего одна переменная — `args`. Так как в программу не передавались аргументы командной строки, значением этой переменной является пустой массив строк. Кроме того, Visual Studio открыла пустое окно консоли.

1. Выберите **Отладка** > **Выполнять по шагам** или нажмите клавишу F11. Будет выделена следующая выполняемая строка. Как показано на рисунке, на выполнение кода от предыдущей до текущей инструкции потребовалось менее одной миллисекунды. По-прежнему определена только одна переменная `args`. Окно консоли остается пустым.

   ![Окно Visual Studio](./media/debugging-with-visual-studio/stepinto2.png)

1. Выберите **Отладка** > **Выполнять по шагам** или нажмите клавишу F11. Visual Studio подсвечивает инструкцию, которая содержит присваивание значения переменной `name`. В окне **Видимые** отображается, что `name` имеет значение `null`, а в окне консоли появилась строка "What is your name?" (Введите имя:).

1. Ответьте на этот запрос, введя строку в окно консоли и нажав клавишу ВВОД. Консоль никак не отреагирует на это, и введенная строка не будет отображаться в окне консоли, но метод [`Console.ReadLine`](xref:System.Console.ReadLine) получит введенные входные данные.

1. Выберите **Отладка** > **Выполнять по шагам** или нажмите клавишу F11. Visual Studio подсвечивает инструкцию, которая содержит присваивание значения переменной `date`. В окне **Видимые** отображается значение свойства [`DateTime.Now`](xref:System.DateTime.Now) и значение, полученное в результате вызова метода [`Console.ReadLine`](xref:System.Console.ReadLine). Также в окне консоли появится строка, введенная в ответ на запрос консоли для ввода данных.

1. Выберите **Отладка** > **Выполнять по шагам** или нажмите клавишу F11. В окне **Видимые** отображается значение переменной `date`, которому было присвоено свойство [`DateTime.Now`](xref:System.DateTime.Now). В окне консоли изменений не произошло.

1. Выберите **Отладка** > **Выполнять по шагам** или нажмите клавишу F11. Visual Studio вызывает метод [`Console.WriteLine`](xref:System.Console.WriteLine(System.String,System.Object,System.Object)). Значения переменных `date` и `name` отображаются в окне **Видимые**, а окно консоли отображает форматированную строку.

1. Выберите **Отладка** > **Выйти из режима пошагового выполнения** или нажмите SHIFT+F11. Пошаговое выполнение на этом прекратится. В окне консоли отображается сообщение с предложением нажать любую клавишу для выхода.

1. Нажмите любую клавишу, чтобы закрыть окно консоли и закрыть режим отладки.

## <a name="building-a-release-version"></a>Сборка версии в режиме выпуска

После сборки приложения в режиме отладки следует скомпилировать и протестировать приложение в режиме выпуска. При сборке в режиме выпуска компилятор использует методы оптимизации, которые иногда могут негативно повлиять на поведение приложения. Например, оптимизации компилятора для повышения производительности могут привести к состоянию конкуренции в асинхронных и многопоточных приложениях.

Чтобы собрать и протестировать консольное приложение в режиме выпуска, переключите конфигурацию сборки из режима **Отладка** в режим **Выпуск** на панели инструментов.

![Изображение](./media/debugging-with-visual-studio/toolbar2.png)

Если нажать клавишу F5 или выбрать пункт **Собрать решение** в меню **Сборка**, Visual Studio скомпилирует версию консольного приложения в режиме выпуска, которую можно протестировать. Приложение, собранное в режиме выпуска, можно протестировать точно так же, как и в режиме отладки.

Завершив отладку приложения, вы можете опубликовать развертываемую версию своего приложения. Дополнительные сведения см. в разделе [Публикация приложения Hello World на C# в Visual Studio 2017](./publishing-with-visual-studio.md).
