# Quick Start

Режимы работы:
* [Генерирование SVG-документа](#Генерирование-SVG)
* [Парсинг SVG-документа](#Парсинг-SVG)

## Генерирование SVG

Подготовить SVG-документ:
```java
createDoc() {
    DOMImplementation impl = SVGDOMImplementation.getDOMImplementation();
    Document doc = impl.createDocument("http://www.w3.org/2000/svg", "svg", null);
    
    SVGGraphics2D svgGenerator = new SVGGraphics2D(doc);
}
```

Подготовить холст перед рисованием:
```java
prepare() {
    svgGenerator.setSVGCanvasSize(new Dimension(400, 300));
}
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

### Рисование

Геометрические примитивы:
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
svgGenerator.drawString("Hello World", int x, int y);
// Форматированный текст
svgGenerator.drawString(AttributedCharacterIterator iterator, int x, int y);

save();
```

#### Сложные фигуры

```java
createDoc();
prepare();

// Polyline — ломаная линия (незамкнутая фигура)
// Polygon — многоугольник (полигон) (замкнутая фигура)

// Ломаная линия:
svgGenerator.drawPolyline(xPoints, yPoints, 4);
// Разделения на заполнение и контур нету

// Многоугольник:
int[] xPoints = {100, 150, 200, 250, 300};
int[] yPoints = {400, 350, 400, 450, 400};
int pointsCount = 5; // Кол-во точек в xPoints и yPoints
svgGenerator.setPaint(Color.BLACK);
svgGenerator.drawPolygon(xPoints, yPoints, pointsCount);
svgGenerator.fillPolygon(xPoints, yPoints, pointsCount);

// Треугольник — тот же многоугольник, но у которого только 3 точки (3 в xPoints и 3 в yPoints).

save();
```

```java
createDoc();
prepare();

// Кривая Безье 2-го порядка
svgGenerator.drawCurveTo(float x1, float y1, float x2, float y2, float x3, float y3);
// Кривая Безье 3-го порядка
svgGenerator.drawCubicTo(float x1, float y1, float x2, float y2, float x3, float y3);

save();
```

Использование SVG-тега
[`<path>`](https://developer.mozilla.org/en-US/docs/Web/SVG/Tutorials/SVG_from_scratch/Paths):
```java
createDoc();
prepare();

GeneralPath path = new GeneralPath();

path.moveTo(50, 50);   // Начало пути
path.lineTo(150, 50);  // Линия
path.lineTo(100, 150); // Еще одна линия
path.curveTo(250, 150, 250, 200, 200, 250); // Кубическая кривая Безье
path.closePath();      // Закрытие пути (соединяет последнюю точку с начальной)

svgGenerator.setPaint(Color.BLACK);
svgGenerator.draw(path); // Контур
svgGenerator.fill(path); // Заполнение

save();
```

## Парсинг SVG
