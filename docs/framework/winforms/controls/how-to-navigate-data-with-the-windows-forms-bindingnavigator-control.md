---
title: Практическое руководство. Переход между данными с помощью элемента управления BindingNavigator в Windows Forms
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- BindingNavigator control [Windows Forms], navigating data
- data [Windows Forms], navigating
- data navigation
- examples [Windows Forms], BindingNavigator control
ms.assetid: 0e5d4f34-bc9b-47cf-9b8d-93acbb1f1dbb
ms.openlocfilehash: 14f845e33b38da39b900b32c07297a350326350d
ms.sourcegitcommit: 2eceb05f1a5bb261291a1f6a91c5153727ac1c19
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43519617"
---
# <a name="how-to-navigate-data-with-the-windows-forms-bindingnavigator-control"></a>Практическое руководство. Переход между данными с помощью элемента управления BindingNavigator в Windows Forms
С появлением элемента управления <xref:System.Windows.Forms.BindingNavigator> в Windows Forms разработчики получили возможность предоставлять конечным пользователям простой пользовательский интерфейс для перехода и управления данными в формах, которые они создают.  
  
 Элемент управления <xref:System.Windows.Forms.BindingNavigator> является элементом управления <xref:System.Windows.Forms.ToolStrip> с кнопками, предварительно настроенными для перехода к первой, последней, следующей и предыдущей записям набора данных, а также для добавления и удаления записей. Добавить кнопки в элемент управления <xref:System.Windows.Forms.BindingNavigator> просто, так как это элемент управления <xref:System.Windows.Forms.ToolStrip>.  См. также [Практическое руководство. Добавление кнопок загрузки, сохранения и отмены в элемент управления BindingNavigator в формах Windows Forms](https://msdn.microsoft.com/library/safa4957\(v=vs.110\)).  
  
 Каждой кнопке элемента управления <xref:System.Windows.Forms.BindingNavigator> соответствует член компонента <xref:System.Windows.Forms.BindingSource>, обеспечивающий ту же функциональность программным путем. Например, кнопка <xref:System.Windows.Forms.BindingNavigator.MoveFirstItem%2A> соответствует методу <xref:System.Windows.Forms.BindingSource.MoveFirst%2A> компонента <xref:System.Windows.Forms.BindingSource>, кнопка <xref:System.Windows.Forms.BindingNavigator.DeleteItem%2A> соответствует методу <xref:System.Windows.Forms.BindingSource.RemoveCurrent%2A> и т. д. Таким образом, обеспечение перехода по данным с помощью элемента управления <xref:System.Windows.Forms.BindingNavigator> — простая процедура, требующая присвоения свойству <xref:System.Windows.Forms.BindingNavigator.BindingSource%2A> соответствующего компонента <xref:System.Windows.Forms.BindingSource> в форме.  
  
### <a name="to-set-up-the-bindingnavigator-control"></a>Настройка элемента управления BindingNavigator  
  
1.  Добавьте компонент <xref:System.Windows.Forms.BindingSource> с именем `bindingSource1` и два элемента управления <xref:System.Windows.Forms.TextBox> с именами `textBox1` и `textBox2`.  
  
2.  Свяжите `bindingSource1` с данными, а элементы управления текстового поля — с `bindingSource1`. Для этого вставьте приведенный ниже код в форму и вызовите `LoadData` из конструктора формы или метода обработки событий <xref:System.Windows.Forms.Form.Load>.  
  
     [!code-csharp[System.Windows.Forms.BindingNavigatorNavigate#2](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.BindingNavigatorNavigate/CS/Form1.cs#2)]
     [!code-vb[System.Windows.Forms.BindingNavigatorNavigate#2](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.BindingNavigatorNavigate/VB/Form1.vb#2)]  
  
3.  Добавьте элемент управления <xref:System.Windows.Forms.BindingNavigator> с именем `bindingNavigator1` в форму.  
  
4.  Присвойте свойству <xref:System.Windows.Forms.BindingNavigator.BindingSource%2A> элемента `bindingNavigator1` значение `bindingSource1`. Это можно сделать с помощью конструктора или в коде.  
  
     [!code-csharp[System.Windows.Forms.BindingNavigatorNavigate#3](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.BindingNavigatorNavigate/CS/Form1.cs#3)]
     [!code-vb[System.Windows.Forms.BindingNavigatorNavigate#3](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.BindingNavigatorNavigate/VB/Form1.vb#3)]  
  
## <a name="example"></a>Пример  
 В примере кода ниже полностью представлены предыдущие шаги.  
  
 [!code-csharp[System.Windows.Forms.BindingNavigatorNavigate#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.BindingNavigatorNavigate/CS/Form1.cs#1)]
 [!code-vb[System.Windows.Forms.BindingNavigatorNavigate#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.BindingNavigatorNavigate/VB/Form1.vb#1)]  
  
## <a name="compiling-the-code"></a>Компиляция кода  
 Для этого примера требуются:  
  
-   ссылки на сборки System, System.Data, System.Drawing, System.Windows.Forms и System.Xml.  
  
 Сведения о выполнении сборки этого примера из командной строки для Visual Basic или Visual C#, см. в разделе [построение из командной строки](~/docs/visual-basic/reference/command-line-compiler/building-from-the-command-line.md) или [командной строки создания с помощью csc.exe](~/docs/csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md). Можно также сборке этого примера в Visual Studio путем вставки кода в новый проект.  См. также [Практическое руководство. Компиляция и выполнение откомпилированного примера кода формы Windows Forms с помощью Visual Studio](https://msdn.microsoft.com/library/Bb129228\(v=vs.110\)).  
  
## <a name="see-also"></a>См. также  
 <xref:System.Windows.Forms.BindingNavigator>  
 [Элемент управления BindingNavigator](../../../../docs/framework/winforms/controls/bindingnavigator-control-windows-forms.md)  
 [Элемент управления ToolStrip](../../../../docs/framework/winforms/controls/toolstrip-control-windows-forms.md)
