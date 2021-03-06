---
title: Практическое руководство. Задание атрибутов среды CLR для элемента
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.dsltools.EditAttributesDialog
helpviewer_keywords:
- Domain-Specific Language, custom attrributes
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f943f9713e4432f0b06242a2f66acae6b390e5cc
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/22/2019
ms.locfileid: "72748369"
---
# <a name="how-to-set-clr-attributes-on-an-element"></a>Практическое руководство. Задание атрибутов среды CLR для элемента
Настраиваемые атрибуты — это специальные атрибуты, которые могут быть добавлены к элементам домена, фигурам, соединителям и схемам. Можно добавить любой атрибут, наследующий от класса `System.Attribute`.

### <a name="to-add-a-custom-attribute"></a>Добавление настраиваемого атрибута

1. В **обозревателе DSL**выберите элемент, к которому необходимо добавить настраиваемый атрибут.

2. В окне **Свойства** рядом со свойством **настраиваемые атрибуты** щелкните значок обзора ( **...** ).

     Откроется диалоговое окно **изменение атрибутов** .

3. В столбце **имя** щелкните **\<add атрибут >** и введите имя атрибута. Нажмите клавишу ВВОД.

4. В строке под именем атрибута указаны круглые скобки. В этой строке введите тип параметра для атрибута (например, `string`) и нажмите клавишу ВВОД.

5. В столбце **имя свойства** введите соответствующее имя, например `MyString`.

6. Нажмите кнопку **ОК**.

     Свойство **настраиваемые атрибуты** теперь отображает атрибут в следующем формате:

     `[` *AttributeName* `(` *тип* `=` *ParameterName* `)]`

## <a name="see-also"></a>См. также

- [Глоссарий средств предметно-ориентированных языков](https://msdn.microsoft.com/ca5e84cb-a315-465c-be24-76aa3df276aa)