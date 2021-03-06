---
layout: post
title: Использование нескольких FXML файлов
---

Перевод отрывка из книги Pro JavaFX 9

 Поскольку результатом загрузки файла FXML является узел JavaFX, который может использоваться в сцене, Вы не ограничены в
использовании только одного файла FXML для любой сцены. Вы можете, например, разбить сцену на две или более частей и
представьте каждую часть своим собственным файлом FXML. Затем вы можете вызвать один из методов load() FXMLLoader на
FXML файл каждой части, и собрать результирующие узлы программно в вашей сцене.

 Формат файла FXML поддерживает другой механизм объединения отдельно подготовленных файлов FXML
вместе. Один файл FXML может включать другой с элементом fx: include. Элемент fx: include
поддерживает три атрибута: атрибут _source_ содержит расположение включенного файла FXML;
атрибут _resources_ содержит расположение пакета ресурсов, используемого включенным файлом FXML; и
атрибут _charset_ содержит кодировку для файла fxml. Если исходный атрибут начинается с символа”/", он
интерпретируется как путь в classpath; в противном случае он интерпретируется как путь относительно местоположения включающего
файл FXML. Атрибуты resource и charset являются необязательными. Если они не указаны, их значения
используется для загрузки включающего файла FXML. Фабрика постройки и фабрика контроллера используемые для
загрузки включаещего файла FXML также используются для загрузки включенного файла FXML.

  FX: id может быть указан для элемента fx: include. Если указан fx:id, соответствующее поле
в контроллере включающего файла FXML можно указать, и FXMLLoader введет это поле с
результатом загрузки включенного файла FXML. Кроме того, если включенный файл FXML имеет указанный FX: controller
в своем корневом элементе, этот контроллер включаемого FXML файла также могут быть инъектирован в том числе в контроллер включаещего FXML файла при условии, что правильно названное и типизированное поле доступно в контроллере включающего файла для получения контроллера включенного  FXML файла. В примере приложения этого раздела мы используем два FXML
файла для представления пользовательского интерфейса приложения.

Включающий FXML файл может иметь следующие строки:
{% highlight java %}

<BorderPane maxHeight="-Infinity"
            ...
            fx:controller="IncludeExampleTreeController">
        <fx:include fx:id="details"
                    source="IncludeExampleDetail.fxml" />
{% endhighlight %}

Включаемый FXML :
{% highlight java %}
<VBox maxHeight="-Infinity"
      ...
      fx:controller="IncludeExampleDetailController">
{% endhighlight %}
Следовательно,при загрузке включаемый FXML файл в результате корнеым элементом будет VBox, и контроллер типа IncludeExampleDetailController. Код контроллера IncludeExampleDetailController:
{% highlight java %}

@FXML
private VBox details;
@FXML
private IncludeExampleDetailController detailsController;

{% endhighlight %}


