---
title: "Оптимизация изображений для эффективной работы сайта"
description: "Изображения часто добавляют вес загруженным файлам, а также занимают значительную площадь визуального пространства страницы."
updated_on: 2014-04-30
key-takeaways:
  use-right-image:
    - "Используйте изображение, которое оптимально подходит под парамеры устройства: размер экрана, разрешение и шаблон страниц."
    - "Замените свойство CSS <code>background-image</code> для экранов с высоким разрешением и применением медиазапросов на <code>min-resolution</code> и <code>-webkit-min-device-pixel-ratio</code>."
    - "Для изображений в высоком разрешении используйте атрибут srcset (наряду с изображениями 1x в разметке)."
    - "Учитывайте эффективность затрат при использовании техники замещения текста изображением в JavaScript или сжатии изображений высокого разрешения для устройств с низким разрешением экрана."
  avoid-images:
    - "Старайтесь не использовать изображения: применяйте возможности браузера, замещайте изображения символами Unicode, а комплексные значки - иконочными шрифтами."
  optimize-images:
    - "Внимательно отнеситесь к формату изображения. Изучите доступные вам форматы и выберите наиболее подходящий."
    - "Чтобы уменьшить размер файла, воспользуйтесь инструментами для оптимизации и сжатия изображений."
    - "Сократите число HTTP-запросов. Для этого объедините часто запрашиваемые изображения в спрайты."
    - "Загрузка изображений должна начинаться, когда они попадают в область просмотра. Так вы ускорите загрузку базовой страницы и уменьшите ее вес."
notes:
  compressive:
    - "С осторожностью используйте техники сжатия, так как они занимают больше памяти и требуют затрат на декодирование.  Адаптация крупных изображений для небольших экранов - ресурсоемкий процесс. Он может вызвать проблемы в работе низкопроизводительных устройств с небольшим объемом памяти и ограниченными возможностями обработки данных."
related-guides:
  optimize:
  -
      title: "Как оптимизировать изображения"
      href: fundamentals/performance/optimizing-content-efficiency/optimize-encoding-and-transfer.html#image-optimization
      section:
        id: optimizing-content-efficiency
        title: "Оптимизация эффективности контента"
        href: performance/optimizing-content-efficiency/
---

<p class="intro">
  Изображения часто добавляют вес загруженным файлам, а также занимают значительную площадь визуального пространства страницы. Оптимизировав изображения, вы сможете сэкономить байты и повысить производительность вашего веб-сайта. Чем меньше байтов требуется загрузить браузеру, тем меньше нагрузка на пропускную способность сети клиента и тем быстрее браузер скачивает и отображает все цифровые объекты.
</p>



{% include shared/takeaway.liquid list=page.key-takeaways.optimize-images %}

## Выбирайте подходящий формат

Мы имеем дело с изображениями двух типов: [векторными](http://ru.wikipedia.org/wiki/Векторная_графика) и [растровыми](http://ru.wikipedia.org/wiki/Растровая_графика). При работе с растровой графикой вам потребуется выбрать корректный формат сжатия, например GIF, PNG или JPG.

**Растровые изображения** - это, как правило, фотографии и другие изображения, которые представляют собой сетку пикселей или точек. Обычно они создаются с помощью фотоаппаратов, сканеров, а также в браузере (элемент canvas).  Поскольку размер изображения становится больше, размер файла также увеличивается.  Если размер масштабированного изображения больше исходного, растровые изображения становятся размытыми, так как браузер не может правильно заполнить недостающие пиксели.

**Векторная графика** - это, как правило, логотипы и штриховые рисунки. Представляет собой серию кривых, линий, фигур и цветов закраски. Векторные изображения создаются с помощью таких программ, как Adobe Illustrator или Inkscape, и сохраняются в формате [SVG](http://css-tricks.com/using-svg/).  Они состоят из простых элементов, поэтому их можно масштабировать без потери качества. Размер файла также остается прежним.

При выборе формата важно учитывать как тип изображения (растровое или векторное), так и его контент (цвета, анимация, текст и т. д.). Не существует универсальных решений, которые можно использовать для всех типов изображений с одинаковой эффективностью. У всех форматов есть свои сильные и слабые стороны.

Ниже мы расскажем о том, как выбрать наиболее подходящий формат в каждом конкретном случае.

* Для фото используйте формат JPG.
* Для создания векторной графики и сплошной заливки (например, логотипов и штриховых рисунков) подходит SVG.
  Если векторные изображения недоступны, попробуйте WebP или PNG.
* Чтобы отобразить больше цветов и добиться лучшего коэффициента сжатия, выбирайте PNG вместо GIF.
* Для роликов используйте тег <video>. В результате вы получите более качественное изображение, а пользователь сможет управлять воспроизведением.

## Уменьшите размер файла

Вы можете значительно уменьшить размер файла, если обработаете его после сохранения. Существует множество инструментов сжатия изображений: для форматов lossy и lossless, веб-страниц, графических интерфейсов, командной строки и т. д.  По возможности применяйте автоматическую оптимизацию изображений, это очень поможет вам в работе.

Некоторые инструменты преобразуют файлы JPG и PNG в формат lossless без потери качества изображения. Для работы с файлами JPG мы рекомендуем утилиты [jpegtran](http://jpegclub.org/) и [jpegoptim](http://freshmeat.net/projects/jpegoptim/) (только для Linux, запускается с функцией --strip-all). Для оптимизации файлов PNG воспользуйтесь [OptiPNG](http://optipng.sourceforge.net/) или [PNGOUT](http://www.advsys.net/ken/util/pngout.htm).

## Используйте CSS-спрайты

CSS-спрайтинг представляет собой технику объединения нескольких изображений в одно - так называемый лист спрайта. Вот как отдельные изображения выводятся на экран: фоновое изображение настраивается только для одного элемента (листа спрайта), а затем корректируется таким образом, чтобы на экране отображалась только нужная часть фона.

{% link_sample _code/image-sprite.html %}
<img src="img/sprite-sheet.png" class="center" alt="Пример листа спрайта">
{% endlink_sample %}
{% include_code src=_code/image-sprite.html snippet=sprite lang=css %}

Благодаря спрайтингу сокращается число загрузок изображений при включенном сохранении в кеше.

## Применяйте отложенную загрузку

Отложенная загрузка может значительно ускорить работу длинных веб-страниц с большим количеством изображений в свернутых вкладках. Загрузка изображений происходит по мере необходимости или после загрузки и вывода на экран базового контента.  Эта техника не только повышает эффективность работы веб-сайта, но и может быть использована для создания страниц с неограниченной постраничной прокруткой.

Обратите внимание, что в последнем случае контент загружается только при попадании в область просмотра и, соответственно, может быть недоступен для поисковых систем.  Кроме того, пользователи не смогут добраться до нижнего колонтитула страницы из-за постоянной подгрузки контента.

{% include shared/related_guides.liquid inline=true list=page.related-guides.optimize %}



