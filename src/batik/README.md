# Apache Batik

Библиотека для рисования в векторном формате SVG (+ поддерживается перевод в PNG).

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

svgGenerator.setColor(Color.RED);
svgGenerator.fillRect(0, 0, 300, 200); 

svgGenerator.drawArc(30, 30, 40, 40, 90, 90);
```

## Cheat Sheet
