---
title: Практическое руководство. Перечисление хранилищ для изолированного хранилища
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- enumerating stores
- data storage using isolated storage, enumerating stores
- storing data using isolated storage, enumerating stores
- stores, enumerating
- isolated storage, enumerating stores
- data stores, enumerating
ms.assetid: 0fcf279a-f241-48f0-8034-2e3d331f1fcb
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 484ba261f8e5c88f17b3eba3a354967e2350a621
ms.sourcegitcommit: a885cc8c3e444ca6471348893d5373c6e9e49a47
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/06/2018
ms.locfileid: "43875893"
---
# <a name="how-to-enumerate-stores-for-isolated-storage"></a>Практическое руководство. Перечисление хранилищ для изолированного хранилища
Перечислить все изолированные хранилища для текущего пользователя можно с помощью статического метода <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetEnumerator%2A?displayProperty=nameWithType>. Этот метод принимает значение <xref:System.IO.IsolatedStorage.IsolatedStorageScope> и возвращает перечислитель <xref:System.IO.IsolatedStorage.IsolatedStorageFile>. Чтобы перечислить хранилища, вам нужно разрешение <xref:System.Security.Permissions.IsolatedStorageFilePermission>, которое указывает значение <xref:System.Security.Permissions.IsolatedStorageContainment.AdministerIsolatedStorageByUser>. При вызове метода <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetEnumerator%2A> со значением <xref:System.IO.IsolatedStorage.IsolatedStorageScope.User> он возвращает массив объектов <xref:System.IO.IsolatedStorage.IsolatedStorageFile>, определенных для текущего пользователя.  
  
## <a name="example"></a>Пример  
 Следующий пример кода получает хранилище, изолированное по пользователю и сборке, создает в нем несколько файлов и извлекает эти файлы с помощью метода <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetEnumerator%2A>.  
  
 [!code-csharp[Conceptual.IsolatedStorage#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.isolatedstorage/cs/source2.cs#2)]
 [!code-vb[Conceptual.IsolatedStorage#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.isolatedstorage/vb/source2.vb#2)]  
  
## <a name="see-also"></a>См. также

- <xref:System.IO.IsolatedStorage.IsolatedStorageFile>  
- [Изолированное хранилище](../../../docs/standard/io/isolated-storage.md)
