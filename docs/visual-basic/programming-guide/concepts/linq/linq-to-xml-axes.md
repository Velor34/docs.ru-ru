---
title: Оси LINQ to XML (Visual Basic)
ms.date: 07/20/2015
ms.assetid: ecd3bd00-28e5-4517-a59f-53bff39fd478
ms.openlocfilehash: 23feaf0aee66002a59279a49192ad459afc682aa
ms.sourcegitcommit: e614e0f3b031293e4107f37f752be43652f3f253
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/26/2018
ms.locfileid: "42930136"
---
# <a name="linq-to-xml-axes-visual-basic"></a>Оси LINQ to XML (Visual Basic)
После создания XML-дерева или загрузки XML-документа в XML-дерево можно опросить его для поиска элементов и атрибутов и извлечения их значений.  
  
 Перед составлением каких-либо запросов необходимо понять назначение осей [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]. Существует два вида методов оси. Во-первых, есть методы, вызываемые применительно к одному объекту <xref:System.Xml.Linq.XElement>, объекту <xref:System.Xml.Linq.XDocument> или объекту <xref:System.Xml.Linq.XNode>. Данные методы работают с одним объектом и возвращают коллекцию объектов <xref:System.Xml.Linq.XElement>, <xref:System.Xml.Linq.XAttribute> или <xref:System.Xml.Linq.XNode>. Во-вторых, существуют методы расширения, работающие с коллекциями и возвращающие коллекции. В этих методах расширения создается перечисление исходной коллекции, вызывается соответствующий метод оси применительно к каждому элементу коллекции и осуществляется объединение результатов.  
  
## <a name="in-this-section"></a>Содержание  
  
|Раздел|Описание:|  
|-----------|-----------------|  
|[Обзор LINQ to XML осей (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-to-xml-axes-overview.md)|Определяет оси и содержит описание того, как они используются в контексте запросов [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)].|  
|[Практическое: извлечение коллекции элементов (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-retrieve-a-collection-of-elements-linq-to-xml.md)|Вводит метод <xref:System.Xml.Linq.XContainer.Elements%2A>. Этот метод получает коллекцию дочерних элементов того или иного элемента.|  
|[Практическое: извлечение значений элемента (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-retrieve-the-value-of-an-element-linq-to-xml.md)|Показывает способ получения значений элементов.|  
|[Практическое: фильтрация по именам элементов (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-filter-on-element-names-linq-to-xml.md)|Показывает способ фильтрации по именам элементов при использовании осей.|  
|[Практическое: связанные вызовы метода оси (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-chain-axis-method-calls-linq-to-xml.md)|Показывает, как соединять в цепочку вызовы для методов осей.|  
|[Практическое: извлечение одного дочернего элемента (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-retrieve-a-single-child-element-linq-to-xml.md)|Показывает способ получения одного дочернего элемента того или иного элемента по имени тега дочернего элемента.|  
|[Практическое: извлечение коллекции атрибутов (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-retrieve-a-collection-of-attributes-linq-to-xml.md)|Вводит метод <xref:System.Xml.Linq.XElement.Attributes%2A>. Этот метод извлекает атрибуты того или иного элемента.|  
|[Практическое: извлечение одного атрибута (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-retrieve-a-single-attribute-linq-to-xml.md)|Показывает способ получения одного атрибута элемента по имени атрибута.|  
|[Практическое: извлечение значений атрибута (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-retrieve-the-value-of-an-attribute-linq-to-xml.md)|Показывает способ получения значений атрибутов.|  
|[Практическое: извлечение поверхностного значения элемента (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-retrieve-the-shallow-value-of-an-element.md)|Показывает способ получения поверхностного значения элемента.|  
|[Встроенные в язык оси в Visual Basic (LINQ to XML)](../../../../visual-basic/programming-guide/concepts/linq/language-integrated-axes.md)|Перечислены осей интегрирован в Visual Basic.|  
  
## <a name="see-also"></a>См. также  
 [Руководство по программированию (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/programming-guide-linq-to-xml.md)
