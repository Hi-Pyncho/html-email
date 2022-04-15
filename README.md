# Заметки по вёрстке писем

## Содержание
- [Заметки по вёрстке писем](#заметки-по-вёрстке-писем)
  - [Содержание](#содержание)
  - [Полезные сервисы](#полезные-сервисы)
    - [Для тестирования вёрстки писем:](#для-тестирования-вёрстки-писем)
    - [Для помощи в вёрстке:](#для-помощи-в-вёрстке)
  - [Содержание заголовка письма](#содержание-заголовка-письма)
  - [Отображение в outlook](#отображение-в-outlook)
  - [Стили для outlook](#стили-для-outlook)
  - [Основные блоки для вёрстки](#основные-блоки-для-вёрстки)
  - [Шрифты](#шрифты)
  - [Отступы между элементами](#отступы-между-элементами)
  - [Общие правила](#общие-правила)

---

## Полезные сервисы

### Для тестирования вёрстки писем:

| Ссылка | Описание |
| ------ | -------- |
| [emailonacid](https://www.emailonacid.com/) | Из плюсов - безлимитное количество preview в тестовой и в платной версии, ничего лишнего в превью. Из минусов - не всегда отрисовываются изображения. |
| [litmus](https://www.litmus.com/) | Из плюсов - много интеграций с различными сервисами и фреймворками. Из минусов - ограниченное количество превью как для бесплатной, так и для платной версии. Также слишком много грузится, когда генерируешь превью (аналитика писем, другая информация), которая для слабого интернета слишком дорогая по времени. |

### Для помощи в вёрстке:

| Ссылка | Описание |
| ------ | -------- |
| [putsmail](https://putsmail.com/) | полностью беплатный сервис, который позволяет отправлять самому себе на почту вёрстку писем. |
| [htmlcrush](https://htmlcrush.com/dark/) | бесплатный сервис для минификации писем. |
| [bulletproof-images](https://backgrounds.cm/) | бесплатный сервис для создания __непробиваемых__ фоновых изображений. |
| [mosaico](https://mosaico.io/) | бесплатный, простой в освоении, но с ограниченным набором блоков конструктор писем. Для создания небольших и несложных текстовых шаблонов. Есть исходный код. При желании можно разобраться и делать свои конструкторы. |
| [stripo](https://stripo.email/) | полубесплатный конструктор с большими возможностями, чем в mosaico. Мало им пользовался, но вдруг, кому пригодится. |
| [buttons](https://buttons.cm/) | бесплатный сервис для генерации кнопок в письмах. |
| [css-selectors](https://tools.emailmatrix.ru/css-guide/) | Гайд по поддерживаемым css селекторам в почтовиках. |
| [can-i-email](https://www.caniemail.com/) | Узнать, поддерживается ли свойства или фича в почтовых клиентах. |
| [after-email](https://alter.email/) | Сервис для обработки email-кода (минификация, инлайн, чистка) |
| [postdrop](https://app.postdrop.io/) | Сервис для вёрстки писем с предпросмотром, используя классы + инлайн |
| [emailcomp](https://emailcomb.com/dark/) | Сервис удаления ненужного и неиспользуемого css |
| [mail-studie](https://mailstudio.app/) | Десктопное приложение-конструктор для вёрстки. Само приложение бесплатное, а фичи (вроде превью) - платные |



## Содержание заголовка письма

```html
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml" xmlns:o="urn:schemas-microsoft-com:office:office">
  <head>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
    <meta name="x-apple-disable-message-reformatting">
    <meta name="viewport" content="initial-scale=1.0">
    <meta name="format-detection" content="telephone=no">
    <meta name='format-detection' content='date=no'>
    <meta name='format-detection' content='address=no'>
    <meta name='format-detection' content='email=no'>
    <title>Title</title>
    <style type="text/css">
      html { -webkit-text-size-adjust:none; -ms-text-size-adjust: none;}
    </style>
  </head>
```

---

## Отображение в outlook
Если нужно отобразить только в Outlook, можно воспользоваться этими условиями
```html
<!--[if (gte mso 9)|(lte ie 8)]><table role="presentation" align="center" border="0" cellspacing="0" cellpadding="0" width="600"><tr><td align="center" valign="top"><![endif]-->
<!-- -->
Здесь контент
<!-- -->
<!--[if (gte mso 9)|(lte ie 8)]></td></tr></table><![endif]-->
```
---

Если наоборот, не надо отображать в Outlook (так как он не воспринимает любые другие способы скрыть конент `display: none; opacity: 0; max-height: 0; overflow: hidden;` и т.д.), то поможет такая конструкция (обёртка условий и `mso-hide: all`):
```html
<!--[if !mso]><!-->
    <table cellpadding="0" cellspacing="0" style="mso-hide: all;">
      <tbody>
        <tr>
          <td style="padding: 10px;"></td>
        </tr>
      </tbody>
    </table>
<!--<![endif]-->
```

## Стили для outlook
Если нужно прописать стили специально для Outlook и конкретной его версии, код стилей можно поместить в такую конструкцию
```html
<!--[if gt mso 11]>
    <style type="text/css">
        ... Стили  для Outlook...
    </style>
<![endif]-->
```
Как определить версию в стилях (и что значит __gt__)

| Значение | Описание |
| ------ | -------- |
| __lt__ | все версии, которые меньше указанной |
| __gt__ | все версии, которые больше указанной |
| __lte__ | все версии, которые меньше или равны указанной |
| __gte__ | все версии, которые больше или равны указанной |

Описание версий
| Значение | Версия Outlook |
| ------ | -------- |
| 9 | Outlook 2000 |
| 10 | Outlook 2002 |
| 11 | Outlook 2003 |
| 12 | Outlook 2007 |
| 14 | Outlook 2010 |
| 15 | Outlook 2013 |
| 16 | Outlook 2016 |

---

## Основные блоки для вёрстки

Обычный блок
```html
<table width="100%" cellspacing="0" cellpadding="0" border="0">
  <tbody>
    <tr>
      <td></td>
    </tr>
  </tbody>
</table>
```

C ограничением ширины
```html
<table width="100%" cellspacing="0" cellpadding="0" border="0" style="width:100%; max-width:600px; border:0;">
  <tbody>
    <tr>
      <td></td>
    </tr>
  </tbody>
</table>
```
---

## Шрифты

Свои шрифты (как и медиавыражение - не факт, что сработают). Но всегда можно использовать стандартные шрифты (Arial, Verdana и т.д.)
1) Добавляем ссылку на шрифт
```html
<link href='https://fonts.googleapis.com/css?family=Roboto:300,300italic,400,400italic,500,500italic,700,700italic' rel='stylesheet' type='text/css' /> 
```
2) Указываем инлайном шрифт для элемента
```html
<p style=”font-family: 'Roboto', sans-serif;”>текст</p>
```
3) Добавляем специальные комментарии для Outlook
```html
<!--[if mso]>
  <style type="text/css">
  p {font-family: sans-serif !important;}
  </style>
<![endif]-->
```

---

## Отступы между элементами

С помощью паддингов внутри блока
```html
<tr>
  <td style='padding: 10px;'></td>
</tr>
```

В Outlook 2013 если высота тэга `td` меньше 19px, он растянет автоматически до 19px. Поэтому можно воспользоваться таким хаком:
```html
<td height="10" style="line-height:10px;">&nbsp;</td>
```

С помощью паддингов между большими секциями или блоками
```html
<table width='100%' cellpadding="0" cellspacing="0">
  <tbody>
    <tr>
      <td style="padding: 10px;"></td>
    </tr>
  </tbody>
</table>
```
Есть мнение, что для оступов лучше не использовать ни __margin__, ни __padding__. Поэтому в проблемных случаях оступы можно задавать с помощью элемента с неразрывным пробелом:
```html
<div style="height: 10px; line-height:10px; font-size:8px;">&nbsp;</div>
```

Вертикальные отступы можно также задавать с помощью `<br>` (не предпочтительно). Меньше контроля над расстоянием и больше мусора в коде.

Горизонтальные оступы можно добавлять как обычными паддингами, так и неразрывными пробелами `&nbsp;`.

---

## Общие правила
- Прогоняем текст через [Типограф](https://www.artlebedev.ru/typograf/). Либо используем [расширение для VS Code](https://marketplace.visualstudio.com/items?itemName=svetlanakost.typograf). Все символы заменяем на спецальные коды.
- Изображениям задаем `display:block`, чтобы убрать лишние отступы и `max-width: 100%`, чтобы изображение подстравилось под ширину родителя.
- Если неудобно прописывать инлайн стили, можно прописать их отдельно и прогнать через [инлайнер](https://www.campaignmonitor.com/resources/tools/css-inliner/)
- Прописываем больше стилей для элементов (цвет текста, шрифт, размер). Иначе почтовый клиент это сделает сам.
- Всем изображением прописываем `alt` аттрибут, а также `width` и `height` (особенно важно для __outlook__ указать ширину и высоту).
- У каждого элемента должен стоять максимум один класс. 
- Не используем сокращенный синтаксис, например `font: 8px/14px Arial, sans-serif;`.
- Называем изображения короткими и значимыми фразами `email.gif` вместо `campaign_054_design_0x0_v6_email-link.gif` - для повышения доверия почтовика.
- Избегаем больших размеров изображений (меньше 100кб - отлично, меньше 250кб - нормально). Загрузка внешних ресурсов (изображений, gif) - не больше 5мб. Чем меньше, тем лучше.
- Размер письма также не должен превышать 100кб - иначе может обрезаться некоторыми почтовиками. Плюс экономим трафик пользователей. Минифицируем html код, чтобы добиться меньшего размера.
- Прописываем hex код цвета полностью (`#ffffff` вместо `#fff`).
- Используем `padding` вместо `margin` (если и используем, то для Outlook `margin` прописываем с большой буквы `Margin`).
- Для всех ссылок добавляем `target='_blank'`.
- Используем вложенные таблицы вместо `colspan` и `rowspan`.
- На IOS хорошая поддержка CSS3, можно комфортно пользоваться не инлайн стилями и медиавыражениями. В gmail также неплохая поддержка. Для остальных - изящная деградация.
