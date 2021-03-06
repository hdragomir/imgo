imgo
========
Advanced images optimizer

Оптимизатор изображений

Поддерживаемые форматы
---------------------------
* png
* jpeg, jpg
* gif

Использование
---------------------------
* "imgo ." если запустить программу c точкой, в качестве парметра, то она рекурсивно будет искать все файлы (*.png, *.gif, *.jpg, *.jpeg) в текущей директории и всех поддиректориях, лежащих ниже и попытается сжать их.
* "imgo file.png" в качестве атрибута поддерживается  имя сжимаемого файла
* "imgo file.png file2.gif" вместо одного файла можно указать несколько, через пробел

Об уровнях сжатия
---------------------------
Уровни сжатия imgo можно условно разделить на 3 степени (это справедливо для формата PNG)

* "imgo file.png" базовый уровень сжатия (используется по умолчанию), работает относительно быстро, применяет "безопасные" преобразования, рекомендуется использовать на файлах, которые будут открываться c помощью IE6;
* "imgo -b file.png" продвинутый уровень сжатия (вызывается параметром -b или -brute ), применяются весь набор преобразований, опасен тем, что некоторые файлы (с прозрачностью) могут некорректно отображаться в IE6;
* "imgo -m -b file.png" достигается за счет многократного сжатия файла (вызывается параметром -m или -multipass). Замечено, что при дополнительном проходе можно сжать файл сильнее, обычно счет идет на байты и доли процента;

Расширенное использование
---------------------------
* "imgo -h", "imgo --help",  - вывести справку
* "imgo -b", "imgo --brute" - перейти в режим продвинутого сжатия, опасен для IE6, сжимает лучше, но раза в 2-3 медленнее
* "imgo -png" - при рекурсивном обходе папки и ее поддиректорий обрабатывать только *.png файлы
* "imgo -jpg" - при рекурсивном обходе папки и ее поддиректорий обрабатывать только *.jpg, *.jpeg файлы
* "imgo -e", "imgo --emulate" - включение режима эмуляции, исходные файлы перезаписаны не будут, будет выведена только информация о том, насколько можно сжать файл\файлы
* "imgo -m", "imgo --multipass" - если файл удалось сжать, он будет обработан повторно, до тех пор пока эффективность сжатия не будет равна 0
* "imgo -q", "imgo --quiet" - скрытый режим, никакой информации выведено не будет
* "imgo -V", "imgo --version" - выведет на экран версию скрипта
* "imgo -d", "imgo --diff" - после сжатия выводит на экран информацию (различия) между оригинальным файлом и сжатым (экспериментальная функция)
* "imgo -v", "imgo --log" - выводит на экран дополнительную информацию, применяется в отладочных целях

Плюшки
---------------------------
* "imgo -s", "imgo --separate" данная команда отрабатывает на файлах PNG24+Alpha, она создает дополнительно 3 файла. Первый - содержит все непрозрачные области (filename_imgcocmp_corp.png), второй- содержит все полупрозрачные области (filename_imgcocmp_alpha.png), третий- это конвертация первого файла в PNG8, с потерей качества!!! (filename_imgcocmp_corp-nq8.png). Полученные файлы можно обработать "imgo" для получения большей степени сжатия. Как применять эти файлы можно посмотреть по адресу: http://www.artlebedev.ru/tools/technogrette/img/png-2/ 
* "imgo -bkgd#ffffff" устанавливает bKGD, после чего сжимает файл, как использовать bKGD можно узнать http://banzalik.ru/png24-ie6-bg/   
* "imgo -rt" создает рядом с PNG24+Alpha файл filename_imgcocmp_rt.png, c удаленной Alpha (показывает все содержимое, скрытое за прозрачностью)
* "imgo -png8a"  конвертирует PNG24+Alpha в PNG8+Alpha (возможны потери в качестве), более подробно - зачем это надо, http://cssing.org.ua/2008/11/07/png-8-alpha/

О преобразованиях
---------------------------
Некоторые операции, позволяющие сжать файл базируются на смене типа файла, на более "подходящий" для данного (конкретного) изображения.

Преобразования для формата PNG, все преобразования не влияют на картинку (не происходит визуального изменения изображения):

* Из индексированного в полноцветное (PNG8 -> PNG24)
* Понижение количества цветов  (например PNG8 (256 цветов) -> PNG8 (20 цветов) ) 
* tRNS в PNG+Alpha 
* Изменение глубины изображения (битности на канал)
* Из Индексированного в GrayScale + Альфа
* Из Полноцветного+alpha в Полноцветное tRNS
* Полноцветный+alpha в GrayScale+alpha
* GrayScale+alpha в GrayScale tRNS
* чистка прозрачных областей (http://www.artlebedev.ru/tools/technogrette/img/png-3/)

Преобразования для формата JPG, все преобразования не влияют на картинку (не происходит визуального изменения изображения):

* включение прогрессивного режима (progressive)
* включение режима оптимизации (optimize)

Используемые библиотеки
---------------------------
* imagemagick
* pngout
* optipng
* pngrewrite
* exiftool
* advpng
* jpegtran
* gifsicle
* pngnq
* defluff

Установка в MAC OS X
---------------------------
* [Устанавливаем](https://github.com/mxcl/homebrew/wiki/Installation "Устанавливаем") homebrew, если уже установлен - переходим дальше
* Выполняем следующие команды в терминале:

```brew install https://raw.github.com/imgo/imgo-tools/master/Formula/pngout.rb```

```brew install https://raw.github.com/imgo/imgo-tools/master/Formula/defluff.rb```

```brew install https://raw.github.com/imgo/imgo-tools/master/Formula/cryopng.rb```

```brew install https://raw.github.com/imgo/imgo-tools/master/Formula/imgo.rb```


Лицензия
---------------------------
Данное ПО распространяется по Лицензии MIT

<!-- Yandex.Metrika counter -->
<img src="//mc.yandex.ru/watch/12831025" style="position:absolute; left:-9999px;" alt="" />
<!-- /Yandex.Metrika counter -->