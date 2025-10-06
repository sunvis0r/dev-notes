# Apache Batik

Библиотека для рисования в векторном формате SVG (+ поддерживается перевод в PNG).

* [Все полезные ссылки](https://xmlgraphics.apache.org/batik/using/)
* [JavaDoc-документация](https://xmlgraphics.apache.org/batik/javadoc/)

## Quick Start

Подготовить SVG к рисованию:
```java
createDoc() {
    DOMImplementation impl = SVGDOMImplementation.getDOMImplementation();
    Document doc = impl.createDocument("http://www.w3.org/2000/svg", "svg", null);
    
    SVGGraphics2D svgGenerator = new SVGGraphics2D(doc);
}
```

Подготовить холст:
```java
prepare() {
    svgGenerator.setSVGCanvasSize(new Dimension(400, 300));
}
```

Рисование:
```java
createDoc();
prepare();

// Прямоугольник
svgGenerator.setPaint(Color.BLUE);
svgGenerator.drawRect(int x, int y, int width, int height); // Контур
svgGenerator.fillRect(int x, int y, int width, int height); // Заполнение

// Овал
svgGenerator.setPaint(Color.RED);
svgGenerator.drawOval(200, 50, 100, 100); // Контур
svgGenerator.fillOval(200, 50, 100, 100); // Заполнение

// Линия
svgGenerator.setPaint(Color.GREEN);
svgGenerator.drawLine(50, 200, 300, 200);
// Разделения на заполнение и контур нету

// Прямоугольник с закруглёнными краями
svgGenerator.setPaint(Color.BLACK);
svgGenerator.drawRoundRect(...); // Контур
svgGenerator.fillRoundRect(...); // Заполнение

// Сегмент овала
svgGenerator.setPaint(Color.BLACK);
svgGenerator.drawArc(int x, int y, int width, int height, int startAngle, int arcAngle); // Контур
svgGenerator.fillArc(int x, int y, int width, int height, int startAngle, int arcAngle); // Заполнение

// Текст
drawString("Hello World", int x, int y);
// Форматированный текст
drawString(AttributedCharacterIterator iterator, int x, int y);

// Кривая Безье 2-го порядка
drawCurveTo(float x1, float y1, float x2, float y2, float x3, float y3);
// Кривая Безье 3-го порядка
drawCubicTo(float x1, float y1, float x2, float y2, float x3, float y3);

// Фигура любой сложности
drawPath(GeneralPath path);

save();
```

Сохранить:
```java
save() {
    svgGenerator.stream(new File("output.svg"));
}

saveAsBytes() {
    ByteArrayOutputStream byteArrayOutputStream = new ByteArrayOutputStream();
    svgGenerator.stream(new OutputStreamWriter(byteArrayOutputStream, StandardCharsets.UTF_8));
}
```

## Cheat Sheet
