---
title: Руководство по программированию на C#. Ограничение доступности методов доступа
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- read-only properties [C#]
- read-only indexers [C#]
- accessors [C#]
- properties [C#], read-only
- asymmetric accessor accesibility [C#]
- indexers [C#], read-only
ms.assetid: 6e655798-e112-4301-a680-6310a6e012e1
ms.openlocfilehash: d168444bb2e7df6aa71d729a44bd6f20f7bfce3d
ms.sourcegitcommit: bdd930b5df20a45c29483d905526a2a3e4d17c5b
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2018
ms.locfileid: "53242039"
---
# <a name="restricting-accessor-accessibility-c-programming-guide"></a>Ограничение доступности методов доступа (Руководство по программированию на C#)
Выражения [get](../../../csharp/language-reference/keywords/get.md) и [set](../../../csharp/language-reference/keywords/set.md) свойства или индексатора называются *методами доступа*. По умолчанию они имеют такие же уровни видимости или доступа, что и свойство или индексатор, которым они принадлежат. Дополнительные сведения см. в разделе [Уровни доступа](../../../csharp/language-reference/keywords/accessibility-levels.md). Тем не менее в некоторых случаях рекомендуется ограничить уровни доступа для этих методов. Как правило, в этом случае ограничивается уровень доступа для метода `set`, тогда как метод `get` остается общедоступным. Например:  
  
 [!code-csharp[csProgGuideIndexers#6](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/restricting-accessor-accessibility_1.cs)]  
  
 В этом примере свойство `Name` определяет методы доступа `get` и `set`. Метод доступа `get` получает уровень доступа самого свойства (в этом случае `public`), а к методу `set` явным образом применяется модификатор доступа [protected](../../../csharp/language-reference/keywords/protected.md).  
  
## <a name="restrictions-on-access-modifiers-on-accessors"></a>Ограничения модификаторов доступа для методов доступа  
 При использовании модификаторов доступа для свойств или индексаторов необходимо соблюдать следующие ограничения:  
  
-   Модификаторы доступа нельзя использовать в интерфейсе или явной реализации элемента [interface](../../../csharp/language-reference/keywords/interface.md).  
  
-   Модификаторы доступа можно использовать только в том случае, если для свойства или индексатора определены одновременно методы доступа `set` и `get`. В этом случае модификатор может применяться только к одному из двух методов доступа.  
  
-   Если свойству или индексатору назначен модификатор [override](../../../csharp/language-reference/keywords/override.md), модификатор доступа должен соответствовать методу доступа для переопределенного метода доступа, если такой существует.  
  
-   Уровень доступности для метода доступа должен быть более строгим по сравнению с уровнем доступа самого свойства или идентификатора.  
  
## <a name="access-modifiers-on-overriding-accessors"></a>Модификаторы доступа при переопределении методов доступа  
 При переопределении свойства или индексатора переопределенные методы доступа должны быть доступны коду переопределения. Кроме того, уровни доступа свойства или индексатора и их методов доступа должны совпадать с уровнями переопределенных свойства или индексатора и их методов доступа. Например:  
  
 [!code-csharp[csProgGuideIndexers#7](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/restricting-accessor-accessibility_2.cs)]  
  
## <a name="implementing-interfaces"></a>Реализация интерфейсов  
 Методы доступа, которые используются для реализации интерфейса, не могут иметь модификаторы доступа. Тем не менее при реализации интерфейса с использованием одного метода доступа (например, `get`) другой метод доступа может иметь модификатор доступа, как показано в следующем примере:  
  
 [!code-csharp[csProgGuideIndexers#8](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/restricting-accessor-accessibility_3.cs)]  
  
## <a name="accessor-accessibility-domain"></a>Домен доступности для метода доступа  
 При использовании модификатора доступа для метода доступа этот модификатор определяет [домен доступности](../../../csharp/language-reference/keywords/accessibility-domain.md) для такого метода.  
  
 Если к методу доступа не применяется модификатор доступа, домен доступности этого метода определяется уровнем доступности свойства или индексатора.  
  
## <a name="example"></a>Пример  
 В следующем примере определяются три класса: `BaseClass`, `DerivedClass` и `MainClass`. В классе `BaseClass` для обоих классов определены свойства `Name` и `Id`. В этом примере демонстрируется, как свойство `Id` класса `DerivedClass` может быть скрыто свойством `Id` класса `BaseClass` при использовании ограничивающего модификатора доступа, такого как [protected](../../../csharp/language-reference/keywords/protected.md) или [private](../../../csharp/language-reference/keywords/private.md). Таким образом, при присвоении значений этому свойству вместо него вызывается свойство класса `BaseClass`. Чтобы сделать это свойство доступным, необходимо заменить модификатор доступа на [public](../../../csharp/language-reference/keywords/public.md).  
  
 В этом примере также демонстрируется, что ограничивающий модификатор доступа (`private` или `protected`) для метода доступа `set` свойства `Name` в классе `DerivedClass` запрещает доступ к этому методу и при попытке присвоить ему значение возвращает ошибку.  
  
 [!code-csharp[csProgGuideIndexers#5](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/restricting-accessor-accessibility_4.cs)]  
  
## <a name="comments"></a>Комментарии  
 Обратите внимание, что если заменить объявление `new private string Id` на `new public string Id`, будут получены следующие выходные данные:  
  
 `Name and ID in the base class: Name-BaseClass, ID-BaseClass`  
  
 `Name and ID in the derived class: John, John123`  
  
## <a name="see-also"></a>См. также

- [Руководство по программированию на C#](../../../csharp/programming-guide/index.md)  
- [Свойства](../../../csharp/programming-guide/classes-and-structs/properties.md)  
- [Индексаторы](../../../csharp/programming-guide/indexers/index.md)  
- [Модификаторы доступа](../../../csharp/programming-guide/classes-and-structs/access-modifiers.md)
