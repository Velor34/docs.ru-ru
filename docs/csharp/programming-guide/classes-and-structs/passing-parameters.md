---
title: Руководство по программированию на C#. Передача параметров
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- parameters [C#], passing
- passing parameters [C#]
- arguments [C#]
- methods [C#], passing parameters
- C# language, method parameters
ms.assetid: a5c3003f-7441-4710-b8b1-c79de77e0b77
ms.openlocfilehash: 3e205ecba48df69c0e7f289ad8201765b35d5767
ms.sourcegitcommit: bdd930b5df20a45c29483d905526a2a3e4d17c5b
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2018
ms.locfileid: "53238147"
---
# <a name="passing-parameters-c-programming-guide"></a>Передача параметров (Руководство по программированию в C#)
В C# аргументы могут передаваться параметрам либо по значению, либо по ссылке. Передача по ссылке позволяет изменять и сохранять измененные значения параметров членов функций, методов, свойств, индексаторов, операторов и конструкторов в вызывающей среде. Чтобы передать параметр по ссылке, намереваясь изменить значение, используйте ключевое слово `ref` или `out`. Чтобы передать по ссылке, намереваясь предотвратить копирование, но не изменение значения, используйте модификатор `in`. Для простоты в этих примерах используется только ключевое слово `ref`. Дополнительные сведения о различиях между ключевыми словами `in`, `ref` и `out` см. в разделах [in](../../../csharp/language-reference/keywords/in-parameter-modifier.md), [ref](../../../csharp/language-reference/keywords/ref.md), [out](../../../csharp/language-reference/keywords/out-parameter-modifier.md).  
  
 В приведенном ниже примере показано различие между параметрами-значениями и ссылочными параметрами.  
  
 [!code-csharp[csProgGuideParameters#10](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/passing-parameters_1.cs)]  
  
 Дополнительные сведения см. в следующих разделах:  
  
-   [Передача параметров типа значения](../../../csharp/programming-guide/classes-and-structs/passing-value-type-parameters.md)  
  
-   [Передача параметров ссылочного типа](../../../csharp/programming-guide/classes-and-structs/passing-reference-type-parameters.md)  
  
## <a name="c-language-specification"></a>Спецификация языка C#  

Дополнительные сведения см. в разделе [Список аргументов](~/_csharplang/spec/expressions.md#argument-lists) в [Спецификации языка C#](../../language-reference/language-specification/index.md). Спецификация языка является предписывающим источником информации о синтаксисе и использовании языка C#.
  
## <a name="see-also"></a>См. также

- [Руководство по программированию на C#](../../../csharp/programming-guide/index.md)  
- [Методы](../../../csharp/programming-guide/classes-and-structs/methods.md)
