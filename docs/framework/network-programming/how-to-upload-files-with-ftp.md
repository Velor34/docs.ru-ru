---
title: Практическое руководство. Отправка файлов с использованием FTP
description: В этой статье приводится пример, в котором показано, как отправить файл на FTP-сервер.
ms.date: 06/26/2018
dev_langs:
- csharp
- vb
ms.assetid: e40f17c5-dd12-4c62-9dbf-00ab491382dc
ms.openlocfilehash: a1f067462361bb123c9d61a1d099c900a6641d6b
ms.sourcegitcommit: f9e38d31288fe5962e6be5b0cc286da633482873
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/27/2018
ms.locfileid: "37028205"
---
# <a name="how-to-upload-files-with-ftp"></a>Практическое руководство. Отправка файлов с использованием FTP

В этом примере показано, как отправить файл на FTP-сервер.

## <a name="example"></a>Пример

```csharp
using System;
using System.IO;
using System.Net;
using System.Text;

namespace Examples.System.Net
{
    public class WebRequestGetExample
    {
        public static void Main ()
        {
            // Get the object used to communicate with the server.
            FtpWebRequest request = (FtpWebRequest)WebRequest.Create("ftp://www.contoso.com/test.htm");
            request.Method = WebRequestMethods.Ftp.UploadFile;

            // This example assumes the FTP site uses anonymous logon.
            request.Credentials = new NetworkCredential("anonymous", "janeDoe@contoso.com");

            // Copy the contents of the file to the request stream.
            byte[] fileContents;
            using (StreamReader sourceStream = new StreamReader("testfile.txt"))
            {
                fileContents = Encoding.UTF8.GetBytes(sourceStream.ReadToEnd());
            }

            request.ContentLength = fileContents.Length;

            using (Stream requestStream = request.GetRequestStream())
            {
                requestStream.Write(fileContents, 0, fileContents.Length);
            }

            using (FtpWebResponse response = (FtpWebResponse)request.GetResponse())
            {
                Console.WriteLine($"Upload File Complete, status {response.StatusDescription}");
            }
        }
    }
}
```

```vb
Imports System.IO
Imports System.Net
Imports System.Text

Namespace Examples.System.Net
    Public Module WebRequestGetExample
        Public Sub Main()
            ' Get the object used to communicate with the server.
            Dim request As FtpWebRequest = CType(WebRequest.Create("ftp://www.contoso.com/test.htm"), FtpWebRequest)
            request.Method = WebRequestMethods.Ftp.UploadFile

            ' This example assumes the FTP site uses anonymous logon.
            request.Credentials = New NetworkCredential("anonymous", "janeDoe@contoso.com")

            ' Copy the contents of the file to the request stream.
            Dim fileContents As Byte()

            Using sourceStream As StreamReader = New StreamReader("testfile.txt")
                fileContents = Encoding.UTF8.GetBytes(sourceStream.ReadToEnd())
            End Using

            request.ContentLength = fileContents.Length

            Using requestStream As Stream = request.GetRequestStream()
                requestStream.Write(fileContents, 0, fileContents.Length)
            End Using

            Using response As FtpWebResponse = CType(request.GetResponse(), FtpWebResponse)
                Console.WriteLine($"Upload File Complete, status {response.StatusDescription}")
            End Using
        End Sub
    End Module
End Namespace
```