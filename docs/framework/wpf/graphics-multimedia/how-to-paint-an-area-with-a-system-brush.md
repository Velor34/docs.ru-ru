---
title: Практическое руководство. Закраска области с помощью системной кисти
ms.date: 03/30/2017
helpviewer_keywords:
- system brushes [WPF], painting with
- painting [WPF], with system brushes
- brushes [WPF], painting with system brushes [WPF]
ms.assetid: 5141a763-9235-42cb-a6bb-afc75513eac7
ms.openlocfilehash: f8a66ffc283016d65a17b33e98ce28fe4cd1c242
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/04/2018
ms.locfileid: "33561151"
---
# <a name="how-to-paint-an-area-with-a-system-brush"></a>Практическое руководство. Закраска области с помощью системной кисти
<xref:System.Windows.SystemColors> Класс предоставляет доступ к системные кисти и цвета, такие как <xref:System.Windows.SystemColors.ControlBrush%2A>, <xref:System.Windows.SystemColors.ControlBrushKey%2A>, и <xref:System.Windows.SystemColors.DesktopBrush%2A>. Системная кисть является <xref:System.Windows.Media.SolidColorBrush> объект, который закрашивает область с помощью указанного системного цвета. Системная кисть всегда дает сплошную заливку; ее нельзя использовать для создания градиентной заливки.  
  
 Системные кисти можно использовать как статический или динамический ресурс. Используйте динамический ресурс, если нужно автоматическое обновление кисти при изменении пользователем кисти во время выполнения приложения; в противном случае используйте статический ресурс. Класс SystemColors содержит разнообразные статические свойства, которые следуют строгому правилу именования:  
  
-   *\<SystemColor>* Brush  
  
     Возвращает статическую ссылку на <xref:System.Windows.Media.SolidColorBrush> указанного системного цвета.  
  
-   *\<SystemColor>* BrushKey  
  
     Получает динамическую ссылку на <xref:System.Windows.Media.SolidColorBrush> указанного системного цвета.  
  
-   *\<SystemColor>* Color  
  
     Возвращает статическую ссылку на <xref:System.Windows.Media.Color> структуру указанного системного цвета.  
  
-   *\<SystemColor>* ColorKey  
  
     Получает динамическую ссылку на <xref:System.Windows.Media.Color> структуру указанного системного цвета.  
  
 Является системный цвет <xref:System.Windows.Media.Color> структуры, который может использоваться для настройки кисти. Например, можно создать градиент с помощью системных цветов, задав <xref:System.Windows.Media.GradientStop.Color%2A> свойства <xref:System.Windows.Media.LinearGradientBrush> градиента объекта с системными цветами. Пример см. в разделе [использование системных цветов в градиенте](../../../../docs/framework/wpf/graphics-multimedia/how-to-use-system-colors-in-a-gradient.md).  
  
## <a name="example"></a>Пример  
 В следующем примере используется динамическая ссылка на системную кисть для установки фона кнопки.  
  
 [!code-xaml[brushsamples_snip#GraphicsMMDynamicSystemColorDesktopBrushKeyExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/brushsamples_snip/CS/DynamicSystemBrushExample.xaml#graphicsmmdynamicsystemcolordesktopbrushkeyexamplewholepage)]  
  
 В следующем примере используется статическая ссылка на системную кисть для установки фона кнопки.  
  
 [!code-xaml[brushsamples_snip#GraphicsMMStaticSystemColorDesktopBrushExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/brushsamples_snip/CS/StaticSystemBrushExample.xaml#graphicsmmstaticsystemcolordesktopbrushexamplewholepage)]  
  
 Пример, показывающий, как использовать системный цвет в градиенте см. в разделе [использование системных цветов в градиенте](../../../../docs/framework/wpf/graphics-multimedia/how-to-use-system-colors-in-a-gradient.md).  
  
## <a name="see-also"></a>См. также  
 [Использование системных цветов в градиенте](../../../../docs/framework/wpf/graphics-multimedia/how-to-use-system-colors-in-a-gradient.md)  
 [Общие сведения о закраске сплошным цветом и градиентом](../../../../docs/framework/wpf/graphics-multimedia/painting-with-solid-colors-and-gradients-overview.md)
