---
title: Справочник по C#. Ключевое слово this
ms.custom: seodec18
description: Ключевое слово this (справочник по C#)
ms.date: 07/20/2015
f1_keywords:
- this
- this_CSharpKeyword
helpviewer_keywords:
- this keyword [C#]
ms.assetid: d4f827fe-4710-410b-89b8-867dad44b8a3
ms.openlocfilehash: af39ba6e20fb1a7c9e1a356ef5015afd885dbbca
ms.sourcegitcommit: bdd930b5df20a45c29483d905526a2a3e4d17c5b
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2018
ms.locfileid: "53241172"
---
# <a name="this-c-reference"></a>this (Справочник по C#)

Ключевое слово `this` ссылается на текущий экземпляр класса, а также используется в качестве модификатора первого параметра метода расширения.

> [!NOTE]
> В этой статье рассматривается использование `this` с экземплярами класса. Дополнительные сведения об использовании этого ключевого слова в методах расширения см. в разделе [Методы расширения](../../../csharp/programming-guide/classes-and-structs/extension-methods.md).

Ниже перечислены наиболее частые способы использования `this`.

- Для квалификации элементов, скрытых одинаковыми именами, например:

  [!code-csharp[csrefKeywordsAccess#4](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsAccess/CS/csrefKeywordsAccess.cs#4)]  

- Для передачи другим методам объекта в качестве параметра, например:

  ```csharp
  CalcTax(this);
  ```

- Для объявления индексаторов, например:

  [!code-csharp[csrefKeywordsAccess#5](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsAccess/CS/csrefKeywordsAccess.cs#5)]

У статических функций-членов нет указателя `this`, так как они существуют только на уровне класса и не являются частями объектов. Использование ссылки на `this` в статическом методе является недопустимым.

## <a name="example"></a>Пример

В этом примере `this` используется для квалификации членов класса `Employee`, `name` и `alias`, которые скрыты одинаковыми именами. Это ключевое слово также используется для передачи объекта в метод `CalcTax`, который принадлежит другому классу.

[!code-csharp[csrefKeywordsAccess#3](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsAccess/CS/csrefKeywordsAccess.cs#3)]

## <a name="c-language-specification"></a>Спецификация языка C#

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>См. также

- [Справочник по C#](../index.md)
- [Руководство по программированию на C#](../../programming-guide/index.md)
- [Ключевые слова в C#](index.md)
- [base](base.md)
- [Методы](../../programming-guide/classes-and-structs/methods.md)
