---
title: Руководство по программированию на C#. Элементы
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- types [C#], nested types
- C# language, type members
ms.assetid: 4a30a4ab-d690-4936-9124-92ce9448665a
ms.openlocfilehash: e8429df6ef633f11df50ee5526496f9688f845ea
ms.sourcegitcommit: bdd930b5df20a45c29483d905526a2a3e4d17c5b
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2018
ms.locfileid: "53245108"
---
# <a name="members-c-programming-guide"></a>Члены (Руководство по программированию на C#)
В классах и структурах есть члены, представляющие их данные и поведение. Члены класса включают все члены, объявленные в этом классе, а также все члены (кроме конструкторов и методов завершения), объявленные во всех классах в иерархии наследования данного класса. Закрытые члены в базовых классах наследуются, но недоступны из производных классов.  
  
 В следующей таблице перечислены виды членов, которые содержатся в классе или в структуре.  
  
|Член|Описание:|  
|------------|-----------------|  
|[Поля](../../../csharp/programming-guide/classes-and-structs/fields.md)|Поля являются переменными, объявленными в области класса. Поле может иметь встроенный числовой тип или быть экземпляром другого класса. Например, в классе календаря может быть поле, содержащее текущую дату.|  
|[Константы](../../../csharp/programming-guide/classes-and-structs/constants.md)|Константы — это поля или свойства, значения которых устанавливаются во время компиляции и не изменяются.|  
|[Свойства](../../../csharp/programming-guide/classes-and-structs/properties.md)|Свойства — это методы класса. Доступ к ним осуществляется так же, как если бы они были полями этого класса. Свойство может защитить поле класса от изменений (независимо от объекта).|  
|[Методы](../../../csharp/programming-guide/classes-and-structs/methods.md)|Методы определяют действия, которые может выполнить класс. Методы могут принимать параметры, предоставляющие входные данные, и возвращать выходные данные посредством параметров. Методы могут также возвращать значения напрямую, без использования параметров.|  
|[События](../../../csharp/programming-guide/events/index.md)|События предоставляют другим объектам уведомления о различных случаях, таких как нажатие кнопки или успешное выполнение метода. События определяются и переключаются с помощью делегатов.|  
|[Инструкции](../../../csharp/programming-guide/statements-expressions-operators/operators.md)|Перегруженные операторы считаются членами класса. При перегрузке оператора его следует определять как открытый статический метод в классе. Предопределенные операторы (`+`, `*`, `<` и т. д.) не считаются членами. Дополнительные сведения см. в разделе [Перегружаемые операторы](../../../csharp/programming-guide/statements-expressions-operators/overloadable-operators.md).|  
|[Индексаторы](../../../csharp/programming-guide/indexers/index.md)|Индексаторы позволяют индексировать объекты аналогично массивам.|  
|[Конструкторы](../../../csharp/programming-guide/classes-and-structs/constructors.md)|Конструкторы — это методы, которые вызываются при создании объекта. Зачастую они используются для инициализации данных объекта.|  
|[Методы завершения](../../../csharp/programming-guide/classes-and-structs/destructors.md)|Методы завершения очень редко используются в C#. Они являются методами, вызываемыми средой выполнения, когда объект нужно удалить из памяти. Они обычно применяются для правильной обработки ресурсов, которые должны быть высвобождены.|  
|[Вложенные типы](../../../csharp/programming-guide/classes-and-structs/nested-types.md)|Вложенными типами являются типы, объявленные в другом типе. Вложенные типы часто применяются для описания объектов, использующихся только типами, в которых эти объекты находятся.|  
  
## <a name="see-also"></a>См. также

- [Руководство по программированию на C#](../../../csharp/programming-guide/index.md)  
- [Классы](../../../csharp/programming-guide/classes-and-structs/classes.md)  
- [Методы](../../../csharp/programming-guide/classes-and-structs/methods.md)  
- [Конструкторы](../../../csharp/programming-guide/classes-and-structs/constructors.md)  
- [Методы завершения](../../../csharp/programming-guide/classes-and-structs/destructors.md)  
- [Свойства](../../../csharp/programming-guide/classes-and-structs/properties.md)  
- [Поля](../../../csharp/programming-guide/classes-and-structs/fields.md)  
- [Индексаторы](../../../csharp/programming-guide/indexers/index.md)  
- [События](../../../csharp/programming-guide/events/index.md)  
- [Вложенные типы](../../../csharp/programming-guide/classes-and-structs/nested-types.md)  
- [Инструкции](../../../csharp/programming-guide/statements-expressions-operators/operators.md)  
- [Перегружаемые операторы](../../../csharp/programming-guide/statements-expressions-operators/overloadable-operators.md)
