---
title: Проверка точек останова в языковой службе прежних версий | Документация Майкрософт
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- breakpoint validation
- language services [managed package framework], breakpoint validation
ms.assetid: a7e873cd-dfe1-474f-bda5-fd7532774b15
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: e7c46473610c96779d0c54e06e82cf884216b13b
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/22/2019
ms.locfileid: "72722013"
---
# <a name="validating-breakpoints-in-a-legacy-language-service"></a>Проверка точек останова в языковой службе прежних версий
Точка останова указывает, что выполнение программы должно останавливаться в определенной точке во время ее выполнения в отладчике. Пользователь может поместить точку останова в любую строку исходного файла, так как редактор не имеет сведений о том, что представляет собой допустимое расположение для точки останова. При запуске отладчика все отмеченные точки останова (называемые ожидающими точками останова) привязываются к соответствующему расположению в выполняющейся программе. В то же время проверка точек останова выполняется, чтобы убедиться, что они помечают допустимые расположения кода. Например, точка останова в комментарии является недопустимой, так как в исходном коде отсутствует код в этом месте. Отладчик отключает недопустимые точки останова.

 Поскольку языковая служба знает о отображаемом исходном коде, она может проверить точки останова перед запуском отладчика. Можно переопределить метод <xref:Microsoft.VisualStudio.Package.LanguageService.ValidateBreakpointLocation%2A>, чтобы он возвращал диапазон, указывающий допустимое расположение точки останова. Расположение точки останова по-прежнему проверяется при запуске отладчика, но пользователь получает уведомления о недопустимых точках останова, не дожидаясь загрузки отладчика.

## <a name="implementing-support-for-validating-breakpoints"></a>Реализация поддержки для проверки точек останова

- Методу <xref:Microsoft.VisualStudio.Package.LanguageService.ValidateBreakpointLocation%2A> присваивается расположение точки останова. Ваша реализация должна решить, является ли расположение допустимым, и указать это путем возвращения текстового диапазона, определяющего код, связанный с положением точки останова в строке.

- Возвращает <xref:Microsoft.VisualStudio.VSConstants.S_OK>, если расположение является допустимым, или <xref:Microsoft.VisualStudio.VSConstants.S_FALSE>, если он является недопустимым.

- Если точка останова является допустимой, то текстовый диапазон выделяется вместе с точкой останова.

- Если точка останова недопустима, в строке состояния появится сообщение об ошибке.

### <a name="example"></a>Пример
 В этом примере показана реализация метода <xref:Microsoft.VisualStudio.Package.LanguageService.ValidateBreakpointLocation%2A>, который вызывает средство синтаксического анализа для получения диапазона кода (если есть) в указанном расположении.

 В этом примере предполагается, что в класс <xref:Microsoft.VisualStudio.Package.AuthoringSink> добавлен метод `GetCodeSpan`, который проверяет текстовый диапазон и возвращает `true`, если это допустимое расположение точки останова.

```csharp
using Microsoft VisualStudio;
using Microsoft.VisualStudio.Package;
using Microsoft.VisualStudio.TextManager.Interop;

namespace TestLanguagePackage
{
    class TestLanguageService : LanguageService
    {
        public override int ValidateBreakpointLocation(IVsTextBuffer buffer,
                                                       int line,
                                                       int col,
                                                       TextSpan[] pCodeSpan)
        {
            int retval = VSConstants.S_FALSE;
            if (pCodeSpan != null)
            {
                // Initialize span to current line by default.
                pCodeSpan[0].iStartLine = line;
                pCodeSpan[0].iStartIndex = col;
                pCodeSpan[0].iEndLine = line;
                pCodeSpan[0].iEndIndex = col;
            }

            if (buffer != null)
            {
                IVsTextLines textLines = buffer as IVsTextLines;
                if (textLines != null)
                {
                    Source src = this.GetSource(textLines);
                    if (src != null)
                    {
                        TokenInfo tokenInfo = new TokenInfo();
                        string text = src.GetText();
                        ParseRequest req = CreateParseRequest(src,
                                                              line,
                                                              col,
                                                              tokenInfo,
                                                              text,
                                                              src.GetFilePath(),
                                                              ParseReason.CodeSpan,
                                                              null);
                        req.Scope = this.ParseSource(req);
                        TestAuthoringSink sink = req.Sink as TestAuthoringSink;

                        TextSpan span = new TextSpan();
                        if (sink.GetCodeSpan(out span))
                        {
                            pCodeSpan[0] = span;
                            retval = VSConstants.S_OK;
                        }
                    }
                }
            }
            return retval;
        }
    }
}
```

## <a name="see-also"></a>См. также
- [Функции языковой службы прежних версий](../../extensibility/internals/legacy-language-service-features1.md)