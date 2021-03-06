---
title: 'Объектная модель рукописного ввода: Windows Forms и COM по сравнению с WPF'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- enabling ink [WPF]
- InkCanvas control [WPF]
- ink object model [WPF]
- tablet pen [WPF], events [WPF]
- ink [WPF], enabling
- events [WPF], tablet pen
ms.assetid: 577835be-b145-4226-8570-1d309e9b3901
ms.openlocfilehash: c351f3d6bf6dbaf94d865fd56e140c44edc20394
ms.sourcegitcommit: 586dbdcaef9767642436b1e4efbe88fb15473d6f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2018
ms.locfileid: "48842753"
---
# <a name="the-ink-object-model-windows-forms-and-com-versus-wpf"></a>Объектная модель рукописного ввода: Windows Forms и COM по сравнению с WPF

Существует три платформы, поддерживающие рукописный ввод: Платформа Tablet PC Windows Forms, платформа COM для планшетных ПК и платформы Windows Presentation Foundation (WPF).  Ресурс платформы Windows Forms и COM, аналогичной модели объекта, если объект модели для [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] платформы существенно отличается.  В этом разделе обсуждаются различия на высоком уровне, что разработчики, которые работали с одной модели объекта можно лучше понять другой.  
  
## <a name="enabling-ink-in-an-application"></a>Включение рукописного ввода в приложении  
 Все три платформы поставляют объекты и элементы управления, которые позволяют приложению получать входные данные от планшетного пера.  В Windows Forms и COM платформ поставляются с [Microsoft.Ink.InkPicture](https://msdn.microsoft.com/library/aa514604.aspx), [Microsoft.Ink.InkEdit](https://msdn.microsoft.com/library/ms835842.aspx), [Microsoft.Ink.InkOverlay](https://msdn.microsoft.com/library/ms833057.aspx) и [ Microsoft.Ink.InkCollector](https://msdn.microsoft.com/library/ms836493.aspx) классы.  [Microsoft.Ink.InkPicture](https://msdn.microsoft.com/library/aa514604.aspx) и [Microsoft.Ink.InkEdit](https://msdn.microsoft.com/library/ms835842.aspx) являются элементами управления, которые можно добавить к приложению для сбора рукописных фрагментов.  [Microsoft.Ink.InkOverlay](https://msdn.microsoft.com/library/ms833057.aspx) и [Microsoft.Ink.InkCollector](https://msdn.microsoft.com/library/ms836493.aspx) могут присоединяться к существующему окну с поддержкой рукописного ввода windows и пользовательских элементов управления.  
  
 Платформа WPF включает <xref:System.Windows.Controls.InkCanvas> элемента управления.  Вы можете добавить <xref:System.Windows.Controls.InkCanvas> в приложение и начать сбор рукописных данных немедленно. С помощью <xref:System.Windows.Controls.InkCanvas>, пользователь может скопировать, выберите и измените размер рукописного ввода.  Можно добавить другие элементы управления для <xref:System.Windows.Controls.InkCanvas>, и пользователь может вводить рукописные данные в эти элементы управления тоже.  Можно создать пользовательский элемент управления, поддержкой рукописного ввода, добавив <xref:System.Windows.Controls.InkPresenter> и сбора его точек пера.  
  
 В следующей таблице перечислены дополнительные сведения о включении рукописного ввода в приложении:  
  
|Для этого...|На платформе WPF...|На платформах Windows Forms и COM...|  
|-----------------|--------------------------|------------------------------------------|  
|Добавление элемента управления с поддержкой рукописного ввода в приложение|См. в разделе [начало работы с рукописными данными](../../../../docs/framework/wpf/advanced/getting-started-with-ink.md).|См. в разделе [утверждений автоматического формирования образца](/windows/desktop/tablet/auto-claims-form-sample)|  
|Включить рукописный ввод в пользовательский элемент управления|См. в разделе [создания заметки рукописного ввода входного элемента управления](../../../../docs/framework/wpf/advanced/creating-an-ink-input-control.md).|См. в разделе [рукописного ввода в буфер обмена образец](/windows/desktop/tablet/ink-clipboard-sample).|  
  
## <a name="ink-data"></a>Данные рукописного ввода  
 На платформах COM и Windows Forms [Microsoft.Ink.InkCollector](https://msdn.microsoft.com/library/ms836493.aspx), [Microsoft.Ink.InkOverlay](https://msdn.microsoft.com/library/ms833057.aspx), [Microsoft.Ink.InkEdit](https://msdn.microsoft.com/library/ms835842.aspx), и [ Microsoft.Ink.InkPicture](https://msdn.microsoft.com/library/aa514604.aspx) каждого предоставляют [Microsoft.Ink.Ink](https://msdn.microsoft.com/library/aa515768.aspx?displayProperty=nameWithType) объекта. [Microsoft.Ink.Ink](https://msdn.microsoft.com/library/aa515768.aspx) объект содержит данные для одного или нескольких [Microsoft.Ink.Stroke](https://msdn.microsoft.com/library/ms827842.aspx?displayProperty=nameWithType) объектов и предоставляет общие методы и свойства для управления эти штрихи.  [Microsoft.Ink.Ink](https://msdn.microsoft.com/library/aa515768.aspx) объекта управляет временем существования штрихов, она содержит; [Microsoft.Ink.Ink](https://msdn.microsoft.com/library/aa515768.aspx) объект создает и удаляет росчерки, которые ему принадлежат.  Каждый [Microsoft.Ink.Stroke](https://msdn.microsoft.com/library/ms827842.aspx) имеет идентификатор, который является уникальным в пределах родительского [Microsoft.Ink.Ink](https://msdn.microsoft.com/library/aa515768.aspx) объекта.  
  
 На платформе WPF <xref:System.Windows.Ink.Stroke?displayProperty=nameWithType> класс владеет и управляет своим временем существования. Группы <xref:System.Windows.Ink.Stroke> объектов можно собирать вместе в <xref:System.Windows.Ink.StrokeCollection>, который предоставляет методы для общих рукописного ввода операций по управлению данными такие как попаданий тестирования, стирание, преобразование и сериализация рукописных данных. Объект <xref:System.Windows.Ink.Stroke> может принадлежать ноль, один или более <xref:System.Windows.Ink.StrokeCollection> объектов на любом предоставить времени.  Вместо того, [Microsoft.Ink.Ink](https://msdn.microsoft.com/library/aa515768.aspx?displayProperty=nameWithType) объекта, <xref:System.Windows.Controls.InkCanvas> и <xref:System.Windows.Controls.InkPresenter> содержат <xref:System.Windows.Ink.StrokeCollection?displayProperty=nameWithType>.  
  
 В следующей паре иллюстраций сравниваются объектные модели данных рукописного ввода.  На платформах COM и Windows Forms [Microsoft.Ink.Ink](https://msdn.microsoft.com/library/aa515768.aspx?displayProperty=nameWithType) объект ограничивает время существования [Microsoft.Ink.Stroke](https://msdn.microsoft.com/library/ms827842.aspx?displayProperty=nameWithType) объекты и пакеты пера принадлежат отдельным штрихов.  Два или несколько штрихов можно ссылаются на тот же [Microsoft.Ink.DrawingAttributes](https://msdn.microsoft.com/library/ms837931.aspx?displayProperty=nameWithType) объекта, как показано на следующем рисунке.  
  
 ![Схема модели объекта Ink для COM&#47;Winforms. ](../../../../docs/framework/wpf/advanced/media/ink-inkownsstrokes.png "Ink_InkOwnsStrokes")  
  
 На [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], каждая <xref:System.Windows.Ink.Stroke?displayProperty=nameWithType> — это объект среды выполнения, которая существует до тех пор, пока что-нибудь имеет ссылку на него.  Каждый <xref:System.Windows.Ink.Stroke> ссылки <xref:System.Windows.Input.StylusPointCollection> и <xref:System.Windows.Ink.DrawingAttributes?displayProperty=nameWithType> объект, который также являются объектами среды CLR.  
  
 ![Схема модели объекта Ink для WPF. ](../../../../docs/framework/wpf/advanced/media/ink-wpfinkobjectmodel.png "Ink_WPFInkObjectModel")  
  
 В следующей таблице сравниваются способы выполнения некоторых общих задач на [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] платформы и платформы Windows Forms и COM.  
  
|Задача|Windows Presentation Foundation|Windows Forms и COM|  
|----------|-------------------------------------|---------------------------|  
|Сохранить рукописный ввод|<xref:System.Windows.Ink.StrokeCollection.Save%2A>|[Microsoft.Ink.Ink.Save](https://technet.microsoft.com/library/security/microsoft.ink.ink.save(v=vs.90))|  
|Загрузка рукописного ввода|Создание <xref:System.Windows.Ink.StrokeCollection> с <xref:System.Windows.Ink.StrokeCollection.%23ctor%2A> конструктор.|[Microsoft.Ink.Ink.Load](https://msdn.microsoft.com/library/microsoft.ink.ink.load(v=vs.90).aspx)|  
|Проверка нажатия|<xref:System.Windows.Ink.StrokeCollection.HitTest%2A>|[Microsoft.Ink.Ink.HitTest](https://msdn.microsoft.com/library/aa515934.aspx)|  
|Скопируйте рукописного ввода|<xref:System.Windows.Controls.InkCanvas.CopySelection%2A>|[Microsoft.Ink.Ink.ClipboardCopy](https://msdn.microsoft.com/library/microsoft.ink.ink.clipboardcopy(v=vs.100).aspx)|  
|Вставьте рукописного ввода|<xref:System.Windows.Controls.InkCanvas.Paste%2A>|[Microsoft.Ink.Ink.ClipboardPaste](https://msdn.microsoft.com/library/microsoft.ink.ink.clipboardpaste(v=vs.100).aspx)|  
|Доступ к настраиваемым свойствам в коллекцию штрихов|<xref:System.Windows.Ink.StrokeCollection.AddPropertyData%2A> (внутренне хранятся и доступны через свойства <xref:System.Windows.Ink.StrokeCollection.AddPropertyData%2A>, <xref:System.Windows.Ink.StrokeCollection.RemovePropertyData%2A>, и <xref:System.Windows.Ink.StrokeCollection.ContainsPropertyData%2A>)|Используйте [Microsoft.Ink.Ink.ExtendedProperties](https://msdn.microsoft.com/library/microsoft.ink.ink.extendedproperties(v=vs.100).aspx)|  
  
### <a name="sharing-ink-between-platforms"></a>Совместное использование рукописного ввода между платформами  
 Несмотря на то, что платформы имеют разные объектные модели для рукописных данных, совместное использование данных между платформами является очень простым. В следующих примерах сохранить рукописный ввод из приложения Windows Forms и загрузка рукописный ввод в приложение Windows Presentation Foundation.  
  
 [!code-csharp[WinFormWPFInk#UsingWinforms](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WinformWPFInk/CSharp/Program.cs#usingwinforms)]
 [!code-vb[WinFormWPFInk#UsingWinforms](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WinformWPFInk/VisualBasic/Module1.vb#usingwinforms)]  
[!code-csharp[WinFormWPFInk#SaveWinforms](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WinformWPFInk/CSharp/Program.cs#savewinforms)]
[!code-vb[WinFormWPFInk#SaveWinforms](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WinformWPFInk/VisualBasic/Module1.vb#savewinforms)]  
  
 [!code-csharp[WinFormWPFInk#UsingWPF](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WinformWPFInk/CSharp/Program.cs#usingwpf)]
 [!code-vb[WinFormWPFInk#UsingWPF](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WinformWPFInk/VisualBasic/Module1.vb#usingwpf)]  
[!code-csharp[WinFormWPFInk#LoadWPF](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WinformWPFInk/CSharp/Program.cs#loadwpf)]
[!code-vb[WinFormWPFInk#LoadWPF](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WinformWPFInk/VisualBasic/Module1.vb#loadwpf)]  
  
 В следующих примерах сохранить рукописный ввод из приложения Windows Presentation Foundation и загрузка рукописный ввод в приложении Windows Forms.  
  
 [!code-csharp[WinFormWPFInk#UsingWPF](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WinformWPFInk/CSharp/Program.cs#usingwpf)]
 [!code-vb[WinFormWPFInk#UsingWPF](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WinformWPFInk/VisualBasic/Module1.vb#usingwpf)]  
[!code-csharp[WinFormWPFInk#SaveWPF](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WinformWPFInk/CSharp/Program.cs#savewpf)]
[!code-vb[WinFormWPFInk#SaveWPF](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WinformWPFInk/VisualBasic/Module1.vb#savewpf)]  
  
 [!code-csharp[WinFormWPFInk#UsingWinforms](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WinformWPFInk/CSharp/Program.cs#usingwinforms)]
 [!code-vb[WinFormWPFInk#UsingWinforms](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WinformWPFInk/VisualBasic/Module1.vb#usingwinforms)]  
[!code-csharp[WinFormWPFInk#LoadWinforms](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WinformWPFInk/CSharp/Program.cs#loadwinforms)]
[!code-vb[WinFormWPFInk#LoadWinforms](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WinformWPFInk/VisualBasic/Module1.vb#loadwinforms)]
## <a name="events-from-the-tablet-pen"></a>События из планшетное перо  
 [Microsoft.Ink.InkOverlay](https://msdn.microsoft.com/library/ms833057.aspx), [Microsoft.Ink.InkCollector](https://msdn.microsoft.com/library/ms836493.aspx), и [Microsoft.Ink.InkPicture](https://msdn.microsoft.com/library/aa514604.aspx) в Windows Forms и COM платформ получают события при пользователя входных данных пера данных.  [Microsoft.Ink.InkOverlay](https://msdn.microsoft.com/library/ms833057.aspx) или [Microsoft.Ink.InkCollector](https://msdn.microsoft.com/library/ms836493.aspx) присоединяется к окна или элемента управления и может подписываться на события, вызываемые входными данными планшета.  Поток, на котором выполняются эти события зависит от того, вызываются ли события с помощью пера, мыши, или программно.  Дополнительные сведения о потоке в связи с этими событиями, см. в разделе [Общие соображения Threading](/windows/desktop/tablet/general-threading-considerations) и [потоков, на котором срабатывают события](/windows/desktop/tablet/threads-on-which-an-event-can-fire).  
  
 На платформе Windows Presentation Foundation <xref:System.Windows.UIElement> класс имеет события с помощью пера. Это означает, что каждый элемент управления предоставляет полный набор событий пера.  События пера имеют нисходящей и восходящей маршрутизации событий пар и всегда выполняется в потоке приложения.  Дополнительные сведения см. в разделе [Routed Events Overview](../../../../docs/framework/wpf/advanced/routed-events-overview.md).  
  
 На следующей схеме показано сравнение объектные модели для классов, которые инициируют события пера. Объектную модель Windows Presentation Foundation показывает только события восходящей маршрутизации, не им события нисходящей маршрутизации.  
  
 ![Схема событий пера в WPF и Winforms. ](../../../../docs/framework/wpf/advanced/media/ink-stylusevents.png "Ink_StylusEvents")  
  
## <a name="pen-data"></a>Данные пера  
 Все три платформы предоставляют способы перехвата и обработки данных, поступающих от планшетного пера.  На платформах COM и Windows Forms, это достигается путем создания [Microsoft.StylusInput.RealTimeStylus](https://msdn.microsoft.com/library/microsoft.stylusinput.realtimestylus(v=vs.100).aspx), присоединения к нему окна или элемента управления и создания класса, реализующего [ Microsoft.StylusInput.IStylusSyncPlugin](https://msdn.microsoft.com/library/microsoft.stylusinput.istylussyncplugin(v=vs.100).aspx) или [Microsoft.StylusInput.IStylusAsyncPlugin](https://msdn.microsoft.com/library/microsoft.stylusinput.istylusasyncplugin(v=vs.100).aspx) интерфейс. Затем пользовательский подключаемый модуль добавляется к коллекции [Microsoft.StylusInput.RealTimeStylus](https://msdn.microsoft.com/library/microsoft.stylusinput.realtimestylus(v=vs.100).aspx). Дополнительные сведения об этой объектной модели см. в разделе [архитектура потоке на платформах](/windows/desktop/tablet/architecture-of-the-stylusinput-apis).  
  
 На [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] платформы, <xref:System.Windows.UIElement> класс предоставляет доступ к коллекции подключаемых модулей, разработке похожую [Microsoft.StylusInput.RealTimeStylus](https://msdn.microsoft.com/library/microsoft.stylusinput.realtimestylus(v=vs.100).aspx).  Для перехвата данных пера, создайте класс, наследуемый от <xref:System.Windows.Input.StylusPlugIns.StylusPlugIn> и добавить объект <xref:System.Windows.UIElement.StylusPlugIns%2A> коллекцию <xref:System.Windows.UIElement>. Дополнительные сведения об этом взаимодействии см. в разделе [перехват ввода, осуществляемого пером](../../../../docs/framework/wpf/advanced/intercepting-input-from-the-stylus.md).  
  
 На всех платформах пул потоков получает данные рукописного ввода с помощью событий пера и отправляет его в потоке приложения.  Дополнительные сведения о работе с потоками на платформах Windows и COM, см. в разделе [Threading вопросы потоке на платформах](/windows/desktop/tablet/threading-considerations-for-the-stylusinput-apis).  Дополнительные сведения о потоке на программное обеспечение для презентаций Windows, см. в разделе [потоковая модель рукописного ввода](../../../../docs/framework/wpf/advanced/the-ink-threading-model.md).  
  
 На следующем рисунке сравниваются объектные модели для классов, которые получают данные пера в пуле потоков пера.  
  
 ![Схема StylusPlugin модели WPF и Winforms. ](../../../../docs/framework/wpf/advanced/media/ink-stylusplugins.png "Ink_StylusPlugins")
