---
title: Каталог идентификаторов сред выполнения (RID) в .NET Core
description: Сведения об идентификаторах сред выполнения и их использовании в .NET Core.
author: mairaw
ms.author: mairaw
ms.date: 07/19/2018
ms.openlocfilehash: ff0449f7c6f878131f0ec4b16d685d2c02d26719
ms.sourcegitcommit: 2eceb05f1a5bb261291a1f6a91c5153727ac1c19
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43517383"
---
# <a name="net-core-rid-catalog"></a>Каталог идентификаторов сред выполнения (RID) в .NET Core

RID — это сокращение от *Runtime IDentifier* (идентификатор среды выполнения). Идентификаторы RID служат для идентификации целевых платформ, на которых выполняется приложение.
Они используются пакетами .NET для представления ресурсов, специфичных для платформы, в пакетах NuGet. Некоторые примеры идентификаторов RID: `linux-x64`, `ubuntu.14.04-x64`, `win7-x64` или `osx.10.12-x64`.
Для пакетов с собственными зависимостями они указывают, на каких платформах можно восстановить пакет.

Один идентификатор RID можно задать в элементе `<RuntimeIdentifier>` вашего файла проекта. Несколько идентификаторов RID можно определить в виде списка, разделенного точкой с запятой, в элементе `<RuntimeIdentifiers>` файла проекта. Они также используются с помощью параметра `--runtime` со следующими [командами интерфейса командной строки .NET Core](./tools/index.md):

- [dotnet build](./tools/dotnet-build.md)
- [dotnet clean](./tools/dotnet-clean.md)
- [dotnet pack](./tools/dotnet-pack.md)
- [dotnet publish](./tools/dotnet-publish.md)
- [dotnet restore](./tools/dotnet-restore.md)
- [dotnet run](./tools/dotnet-run.md)
- [dotnet store](./tools/dotnet-store.md)

Идентификаторы RID, представляющие отдельные операционные системы, обычно имеют следующий формат: `[os].[version]-[architecture]-[additional qualifiers]`, где:

- `[os]` — это моникер платформы или операционной системы. Например, `ubuntu`.

- `[version]` — это версия операционной системы в виде номера, разделенного точкой (`.`). Например, `15.10`.

  - Это **не должен быть** коммерческий номер версии, так как такой номер часто представляет отдельные версии операционной системы с различными контактными зонами API.

- `[architecture]` — это архитектура процессора. Например, `x86`, `x64`, `arm` или `arm64`.

- `[additional qualifiers]` дополнительно дифференцируют разные платформы. Пример: `aot` или `corert`.

## <a name="rid-graph"></a>Схема RID

Схема RID или резервная схема среды выполнения — это список идентификаторов RID, которые совместимы друг с другом. Идентификаторы RID определены в пакете [Microsoft.NETCore.Platforms](https://www.nuget.org/packages/Microsoft.NETCore.Platforms/). Список поддерживаемых идентификаторов RID и схема RID содержатся в файле [*runtime.json*](https://github.com/dotnet/corefx/blob/master/pkg/Microsoft.NETCore.Platforms/runtime.json), который находится в репозитории CoreFX. В этом файле можно увидеть, что все идентификаторы RID, кроме основного, содержат оператор `"#import"`. Эти операторы указывают совместимые RID.

Когда NuGet восстанавливает пакеты, он пытается найти точное совпадение для указанной среды выполнения.
Если его не удается найти, NuGet проходит схему до тех пор, пока не найдет ближайшую совместимую систему в соответствии со схемой RID.

Ниже приведена запись для идентификатора RID `osx.10.12-x64`:

```json
"osx.10.12-x64": {
    "#import": [ "osx.10.12", "osx.10.11-x64" ]
}
```

Приведенный выше идентификатор RID указывает, что `osx.10.12-x64` импортирует `osx.10.11-x64`. Таким образом, когда NuGet восстанавливает пакеты, он пытается найти в пакете точное совпадение для `osx.10.12-x64`. Например, если NuGet не удается найти определенную среду выполнения, он может восстановить пакеты, которые определяют среды выполнения `osx.10.11-x64`.

В следующем примере показана немного большая схема RID, которая также указана в файле *runtime.json*:

```
    win7-x64    win7-x86
       |   \   /    |
       |   win7     |
       |     |      |
    win-x64  |  win-x86
          \  |  /
            win
             |
            any
```

Все идентификаторы RID в конечном итоге сопоставляются с корневым идентификатором RID `any`.

При работе с идентификаторами RID следует учитывать некоторые моменты:

- RID являются **непрозрачными строками**, и их следует рассматривать как "черные ящики".
- Не следует создавать идентификаторы RID программным способом.
- Используйте только те идентификаторы RID, которые уже определены для платформы.
- Идентификаторы RID должны указываться точно. Предположения недопустимы.

## <a name="using-rids"></a>Использование идентификаторов RID

Для использования идентификаторов RID необходимо знать, какие идентификаторы RID существуют. В платформу регулярно добавляются новые идентификаторы.
Последнюю и полную версию см. в файле [runtime.json](https://github.com/dotnet/corefx/blob/master/pkg/Microsoft.NETCore.Platforms/runtime.json) в репозитории CoreFX.

SDK для .NET Core 2.0 представляет концепцию переносных идентификаторов RID. Это новые значения, добавленными в схему RID, которые не привязаны к конкретной версии или дистрибутиву ОС. Их особенно удобно использовать при работе с несколькими дистрибутивами Linux.

Ниже представлен список наиболее распространенных RID, используемых для каждой ОС. Он не охватывает значения `arm` или `corert`.

## <a name="windows-rids"></a>Идентификаторы RID для Windows

- Портативные
  - `win-x86`
  - `win-x64`
- Windows 7 или Windows Server 2008 R2
  - `win7-x64`
  - `win7-x86`
- Windows 8 или Windows Server 2012
  - `win8-x64`
  - `win8-x86`
  - `win8-arm`
- Windows 8.1 или Windows Server 2012 R2
  - `win81-x64`
  - `win81-x86`
  - `win81-arm`
- Windows 10 или Windows Server 2016
  - `win10-x64`
  - `win10-x86`
  - `win10-arm`
  - `win10-arm64`

Дополнительные сведения см. в разделе [Необходимые компоненты для .NET Core в Windows](windows-prerequisites.md).

## <a name="linux-rids"></a>Идентификаторы RID для Linux

- Портативные
  - `linux-x64`
- CentOS
  - `centos-x64`
  - `centos.7-x64`
- Debian
  - `debian-x64`
  - `debian.8-x64`
  - `debian.9-x64` (.NET Core 1.1 или более поздние версии)
- Fedora
  - `fedora-x64`
  - `fedora.27-x64`
  - `fedora.28-x64` (.NET Core 1.1 или более поздние версии)
- Gentoo (.NET Core 2.0 или более поздние версии)
  - `gentoo-x64`
- openSUSE
  - `opensuse-x64`
  - `opensuse.42.3-x64`
- Oracle Linux
  - `ol-x64`
  - `ol.7-x64`
  - `ol.7.0-x64`
  - `ol.7.1-x64`
  - `ol.7.2-x64`
  - `ol.7.3-x64`
  - `ol.7.4-x64`
- Red Hat Enterprise Linux
  - `rhel-x64`
  - `rhel.6-x64` (.NET Core 2.0 или более поздние версии)
  - `rhel.7-x64`
  - `rhel.7.1-x64`
  - `rhel.7.2-x64`
  - `rhel.7.3-x64` (.NET Core 2.0 или более поздние версии)
  - `rhel.7.4-x64` (.NET Core 2.0 или более поздние версии)
- Tizen (.NET Core 2.0 или более поздние версии)
  - `tizen`
  - `tizen.4.0.0`
  - `tizen.5.0.0`
- Ubuntu
  - `ubuntu-x64`
  - `ubuntu.14.04-x64`
  - `ubuntu.16.04-x64`
  - `ubuntu.17.10-x64`
  - `ubuntu.18.04-x64`
- Производные дистрибутивы Ubuntu
  - `linuxmint.17-x64`
  - `linuxmint.17.1-x64`
  - `linuxmint.17.2-x64`
  - `linuxmint.17.3-x64`
  - `linuxmint.18-x64` (.NET Core 2.0 или более поздние версии)
  - `linuxmint.18.1-x64` (.NET Core 2.0 или более поздние версии)
  - `linuxmint.18.2-x64` (.NET Core 2.0 или более поздние версии)
  - `linuxmint.18.3-x64` (.NET Core 2.0 или более поздние версии)
- SUSE Enterprise Linux (SLES) (.NET Core 2.0 или более поздних версий)
  - `sles-x64`
  - `sles.12-x64`
  - `sles.12.1-x64`
  - `sles.12.2-x64`
  - `sles.12.3-x64`
- Alpine Linux (.NET Core 2.1 или более поздних версий)
  - `alpine-x64`
  - `alpine.3.7-x64`

Дополнительные сведения см. в разделе [Необходимые компоненты для .NET Core в Linux](linux-prerequisites.md).

## <a name="macos-rids"></a>Относительные идентификаторы macOS

Относительные идентификаторы macOS используют старую фирменную символику "OSX".

- `osx-x64` (.NET Core 2.0 или более поздние версии, минимальная версия — `osx.10.12-x64`)
- `osx.10.10-x64`
- `osx.10.11-x64`
- `osx.10.12-x64` (.NET Core 1.1 или более поздние версии)
- `osx.10.13-x64`

Дополнительные сведения см. в разделе [Необходимые компоненты для .NET Core в macOS](macos-prerequisites.md).

## <a name="android-rids-net-core-20-or-later-versions"></a>Идентификаторы RID для Android (.NET Core 2.0 или более поздние версии)

- `android`
- `android.21`

## <a name="see-also"></a>См. также

* [Идентификаторы среды выполнения](https://github.com/dotnet/corefx/blob/master/pkg/Microsoft.NETCore.Platforms/readme.md)
