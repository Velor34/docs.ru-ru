---
title: Команда dotnet build — CLI .NET Core
description: Команда dotnet build выполняет сборку проекта и всех его зависимостей.
ms.date: 12/04/2018
ms.openlocfilehash: 5d47fdfca14d20b3f2a134a8e734f76b1c86c498
ms.sourcegitcommit: ccd8c36b0d74d99291d41aceb14cf98d74dc9d2b
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/10/2018
ms.locfileid: "53149163"
---
# <a name="dotnet-build"></a>dotnet build

[!INCLUDE [topic-appliesto-net-core-all](../../../includes/topic-appliesto-net-core-all.md)]

## <a name="name"></a>name

`dotnet build` — собирает проект и все его зависимости.

## <a name="synopsis"></a>Краткий обзор

# <a name="net-core-2xtabnetcore2x"></a>[.NET Core 2.x](#tab/netcore2x)
```
dotnet build [<PROJECT>|<SOLUTION>] [-c|--configuration] [-f|--framework] [--force] [--no-dependencies] [--no-incremental]
    [--no-restore] [-o|--output] [-r|--runtime] [-v|--verbosity] [--version-suffix]

dotnet build [-h|--help]
```
# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)
```
dotnet build [<PROJECT>|<SOLUTION>] [-c|--configuration] [-f|--framework] [--no-dependencies] [--no-incremental] [-o|--output]
    [-r|--runtime] [-v|--verbosity] [--version-suffix]

dotnet build [-h|--help]
```
---

## <a name="description"></a>Описание

Команда `dotnet build` выполняет сборку проекта и его зависимостей в набор двоичных файлов. Эти двоичные файлы содержат код проекта в виде файлов на промежуточном языке с расширением *DLL*, а также файлы символов для отладки с расширением *PDB*. Создается JSON-файл зависимостей (*\*.deps.json*), содержащий список зависимостей приложения. Создает файл *\*.runtimeconfig.json*, указывающий общую среду выполнения и ее версию для приложения.

Если проект имеет зависимости от сторонних компонентов, таких как библиотеки из NuGet, они разрешаются из кэша NuGet и недоступны в выходных данных сборки проекта. Учитывая это, продукт `dotnet build` не готов к переносу на другой компьютер для выполнения. Это отличается от поведения в .NET Framework, где сборка исполняемого проекта (приложения) создает выходные данные, которые можно запустить на любом компьютере с установленной платформой .NET Framework. Чтобы обеспечить аналогичное поведение в .NET Core, необходимо использовать команду [dotnet publish](dotnet-publish.md). Дополнительные сведения см. в разделе [Развертывание приложений .NET Core](../deploying/index.md).

Для сборки нужен файл *project.assets.json*, содержащий список зависимостей приложения. Он создается при выполнении команды [`dotnet restore`](dotnet-restore.md). Без файла ресурсов инструментарий не способен разрешать базовые сборки, что приводит к ошибкам. При использовании пакета SDK для .NET Core 1.x необходимо было явным образом выполнять команду `dotnet restore` перед выполнением `dotnet build`. Начиная с версии SDK для .NET Core 2.0 команда `dotnet restore` выполняется автоматически при выполнении `dotnet build`. Чтобы отключить неявное восстановление при выполнении команды сборки, можно передать параметр `--no-restore`.

[!INCLUDE[dotnet restore note + options](~/includes/dotnet-restore-note-options.md)]

То, является ли проект исполняемым, определяется свойством `<OutputType>` в файле проекта. Следующий пример описывает проект, который создает исполняемый код:

```xml
<PropertyGroup>
  <OutputType>Exe</OutputType>
</PropertyGroup>
```

Чтобы создать библиотеку, опустите свойство `<OutputType>`. Основное различие в выходных данных заключается в том, что библиотека DLL на промежуточном языке не содержит ни одной точки входа и ее нельзя выполнить.

### <a name="msbuild"></a>MSBuild

`dotnet build` использует MSBuild для сборки проекта, поддерживая при этом как параллельные, так и инкрементные сборки. Дополнительные сведения см. в разделе [Инкрементные сборки](/visualstudio/msbuild/incremental-builds).

Помимо своих параметров, команда `dotnet build` принимает и параметры MSBuild, например `-p` для задания свойств или `-l` для определения средства ведения журнала. Дополнительные сведения об этих параметрах см. в [справочнике по командной строке MSBuild](/visualstudio/msbuild/msbuild-command-line-reference). Либо же вы можете использовать команду [dotnet msbuild](dotnet-msbuild.md).

Выполнение `dotnet build` эквивалентно `dotnet msbuild -restore -target:Build`.

## <a name="arguments"></a>Аргументы

`PROJECT | SOLUTION`

Файл проекта или решения для сборки. Если файл проекта или решения не указан, MSBuild ищет в текущем рабочем каталоге файл с расширением, заканчивающимся на *PROJ* или *SLN*, и использует его.

## <a name="options"></a>Параметры

# <a name="net-core-2xtabnetcore2x"></a>[.NET Core 2.x](#tab/netcore2x)

* **`-c|--configuration {Debug|Release}`**

  Определяет конфигурацию сборки. Значение по умолчанию — `Debug`.

* **`-f|--framework <FRAMEWORK>`**

  Выполняет компиляцию для конкретной [платформы](../../standard/frameworks.md). Платформа должна быть определена в [файле проекта](csproj.md).

* **`--force`**

  Принудительное разрешение всех зависимостей, даже если последнее восстановление прошло успешно. Указание этого флага дает тот же результат, что удаление файла *project.assets.json*.

* **`-h|--help`**

  Выводит краткую справку по команде.

* **`--no-dependencies`**

  Межпроектные (P2P) ссылки игнорируются, и выполняется сборка только указанного корневого проекта.

* **`--no-incremental`**

  Помечает сборку как небезопасную для добавочной сборки. Этот флаг отключает инкрементную компиляцию и запускает принудительную полную перестройку схемы зависимостей проекта.

* **`--no-restore`**

  Во время сборки не выполняется неявное восстановление.

* **`-o|--output <OUTPUT_DIRECTORY>`**

  Каталог, в который будут помещаться собранные двоичные файлы. При указании этого параметра также необходимо определить `--framework`. Если значение не указано, путь по умолчанию — `./bin/<configuration>/<framework>/`.

* **`-r|--runtime <RUNTIME_IDENTIFIER>`**

  Указывает целевую среду выполнения. Список идентификаторов сред выполнения (RID) см. в [каталоге RID](../rid-catalog.md).

* **`-v|--verbosity <LEVEL>`**

  Задает уровень детализации команды. Допустимые значения: `q[uiet]`, `m[inimal]`, `n[ormal]`, `d[etailed]` и `diag[nostic]`.

* **`--version-suffix <VERSION_SUFFIX>`**

  Определяет суффикс версии для звездочки (`*`) в поле версия файла проекта. Формат соответствует рекомендациям в отношении версий NuGet.

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

* **`-c|--configuration {Debug|Release}`**

  Определяет конфигурацию сборки. Значение по умолчанию — `Debug`.

* **`-f|--framework <FRAMEWORK>`**

  Выполняет компиляцию для конкретной [платформы](../../standard/frameworks.md). Платформа должна быть определена в [файле проекта](csproj.md).

* **`-h|--help`**

  Выводит краткую справку по команде.

* **`--no-dependencies`**

  Межпроектные (P2P) ссылки игнорируются, и выполняется сборка только указанного корневого проекта.

* **`--no-incremental`**

  Помечает сборку как небезопасную для добавочной сборки. Этот флаг отключает инкрементную компиляцию и запускает принудительную полную перестройку схемы зависимостей проекта.

* **`-o|--output <OUTPUT_DIRECTORY>`**

  Каталог, в который будут помещаться собранные двоичные файлы. При указании этого параметра также необходимо определить `--framework`.

* **`-r|--runtime <RUNTIME_IDENTIFIER>`**

  Указывает целевую среду выполнения. Список идентификаторов сред выполнения (RID) см. в [каталоге RID](../rid-catalog.md).

* **`-v|--verbosity <LEVEL>`**

  Задает уровень детализации команды. Допустимые значения: `q[uiet]`, `m[inimal]`, `n[ormal]`, `d[etailed]` и `diag[nostic]`.

* **`--version-suffix <VERSION_SUFFIX>`**

  Определяет суффикс версии для звездочки (`*`) в поле версия файла проекта. Формат соответствует рекомендациям в отношении версий NuGet.

---

## <a name="examples"></a>Примеры

* Сборка проекта и его зависимостей:

  ```console
  dotnet build
  ```

* Сборка проекта и его зависимостей с помощью конфигурации Release:

  ```console
  dotnet build --configuration Release
  ```

* Сборка проекта и его зависимостей для определенной среды выполнения (в этом примере это Ubuntu 16.04):

  ```console
  dotnet build --runtime ubuntu.16.04-x64
  ```

* Выполните сборку проекта и используйте указанный источник пакета NuGet во время операции восстановления (пакет SDK для .NET Core 2.0 и более поздних версий).

  ```console
  dotnet build --source c:\packages\mypackages
  ```

* Создайте проект и задайте версию 1.2.3.4 как параметр сборки:

  ```console
  dotnet build -p:Version=1.2.3.4
  ```