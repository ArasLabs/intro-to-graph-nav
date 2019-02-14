# View Card Templates


## 1. Node Template Structure

### Sample Template
This partial template shows the top-level object for a View Card template definition.

```(JSON)
{
    "container": {
        "type": "grid",
        "style": {
            "rows": [{"height": 20}, … , {"height": 25}],
            "cols": [{"width": 50}, … , {"width": 75}],
            "cells": [{...}, … , {...}],
            // Optional style properties. See Section 2: "Node Global Styling".
        }
    }
}
```

### Node Template Properties
The following properties are supported for defining the node structure.

Name | Path | Type | Example
-----|------|------|-------------
Type | `container.type` | string | Currently only supports the "grid" type.
Style | `container.style` | object | The style object contains `rows`, `cols` and `cells` arrays defining the content structure as well as properties defining the global node style. See Section 2: "Node Global Styling" for more detail on style properties.
.... Rows | `container.style.rows` | array | The rows array contains objects each representing a row of node content.<br/>`"rows": [{"height": 20}, … , {"height": 25}]`
.... Columns | `container.style.cols` | array | The cols array contains objects each representing a column of node content.<br/>`"rows": [{"width": 50}, … , {"width": 75}]`
.... Cells | `container.style.cells` | array | The cells array contains the content and styles to be rendered inside the node. See section 2 for more detail on defining cells.

## 2. Node Global Styling

### Sample Template
This partial template highlights the global node styles.

```(JSON)
{
    "container": {
        "type": "grid",
        "style": {
            "width": 200,
            "height": 90,
            "color": "#F7F7F7",
            "padding": {
                "left": 12,
                "right": 12,
                "top": 12,
                "bottom": 12
            },
            "rows": [{"height": 20}, … , {"height": 25}],
            "cols": [{"width": 50}, … , {"width": 75}],
            "border": {
                "width": 1,
                "color": "#555555",
                "cornerRadius": 2,
                "shadow": {
                    "horizontal": 2,
                    "vertical": 3,
                    "color": "#000000",
                    "opacity": 0.5
                }
            },
            "cells": [{...}, … , {...}],
        }
    }
}
```

### Node Styling Properties
The following properties are supported for styling graph nodes.

Name | Path | Type | Example
-----|------|------|-------------
Height | `container.style.height` | integer | The height of the node in pixels.<br/>`"height": 100`
Width | `container.style.width` | integer | The width of the node in pixels.<br/>`"width": 100`
Background Color | `container.style.color` | hex/string | The color of the node background.<br/> `"color": "#F7F7F7"`<br/>`"color": "gray"`
Padding | `container.style.padding` | integer/object | The padding of content inside of the node.<br/>`"padding": 12` – same padding for all sides will be applied. <br/>`"padding": {"left": 10}` – omitted values default to 12. <br/>`"padding": {"left": 5, "right": 5, "top": 10, "bottom": 10}`
Border | `container.style.border` | object | The border property takes an object with `width`, `color`, `cornerRadius`, and `shadow` properties.
.... Border Width | `container.style.border.width` | integer | The node border width in pixels.<br/>`"border": {"width": 1}`
.... Border Color | `container.style.border.color` | hex/string | The color of the node border.<br/>`"border": {"color": "#555555"}`<br/>`"border": {"color": "gray"}`
.... Corner Radius | `container.style.border.cornerRadius` | integer | The radius in pixels for corner smoothing.<br/>`"border": {"cornerRadius": 2}`
.... Shadow | `container.style.border.shadow` | object | The shadow property takes an object with `horizontal`, `vertical`, `color`, and `opacity` properties.
........ Horizontal Size | `container.style.border.shadow.horizontal` | integer | The horizontal shadow size in pixels.<br/>`"shadow": {"horizontal": 2}`   
........ Vertical Size | `container.style.border.shadow.vertical` | integer | The vertical shadow size in pixels.<br/>`"shadow": {"vertical": 3}`     
........ Shadow Color | `container.style.border.shadow.color` | hex/string | The color of the node shadow.<br/>`"shadow": {"color": "#000000"}`   
........ Shadow Opacity | `container.style.border.shadow.opacity` | 0.0-1.0 | The opacity of the node shadow.<br/>`"shadow": {"opacity": 0.5}`   

## 3. Binding Cell Content

### Sample Template
This partial template highlights several cell definitions.

```(JSON)
{
    "container": {
        "type": "grid",
        "style": {
            "width": 200,
            "height": 90,
            "color": "#F7F7F7",
            "padding": { … },
            "rows": [{"height": 20}, … , {"height": 25}],
            "cols": [{"width": 50}, … , {"width": 75}],
            "border": { … },
            "cells": [
                {
                    "content": "image",
                    "content_binding": "icon",
                    "col": 0,
                    "row": 0
                },
                {
                    "content": "text",
                    "content_binding": "keyed_name",
                    "col": 1,
                    "row": 0
                },
                {
                    "content": "text",
                    "content_binding": "generation",
                    "col": 2,
                    "row": 0,
                    "style": {
                        "verticalAlignment": "top",
                        "horizontalAlignment": "end",
                        "font": {
                            "size": 10,
                            "family": "Tahoma",
                            "weight": "normal",
                            "color": "#777777"
                        }
                    }
                }
            ]
        }
    }
}
```

### Cell Content Properties
The following properties are supported for binding content to a node.

Name | Path | Type | Example
-----|------|------|-------------
Cell Content | `cells[i].content` | string | The type of content displayed in the cell.<br/>`"content": "text"`<br/>Also supports `"image"`.
Cell Content Binding | `cells[i].content_binding` | string | Contains the property name corresponding to the defined Node Type.<br/>`"content_binding": "name"`
Cell Column Index | `cells[i].col` | integer | The index of the column where the cell is located.<br/>`"col": 0`
Cell Row Index | `cells[i].row` | integer | The index of the row where the cell is located.<br/>`"row": 0`
Cell Style | `cells[i].style` | object | The style object contains properties for styling this cell. See Section 4: "Node Cell Styling" for more detail about styling cell content.

## 4. Node Cell Styling

### Cell Style Properties
The following properties are supported for styling graph node content cells.

Name | Path | Type | Example
-----|------|------|-------------
Font | `cells[i].style.font` | object | The font property takes an object with `family`, `size`, `weight`, and `color` properties.
.... Font Family | `cells[i].style.font.family` | string | The font family.<br/>`"font": {"family": "Tahoma"}`
.... Font Size | `cells[i].style.font.size` | integer | The font size in pixels.<br/>`"font": {"size": 10}`
.... Font Weight | `cells[i].style.font.weight` | string | The font weight.<br/>`"font": {"weight": "normal"}`<br/>Also supported: `"bold"`, `"bolder"`, `"lighter"`, `"inherit"`
.... Font Color | `cells[i].style.font.color` | hex/string | The font color.<br/>`"font": {"color": "#777777"}`<br>`"font": {"color": "gray"}`
Text Decoration | `cells[i].style.textDecoration` | string | The text decoration.<br/>`"textDecoration": "underline"`<br/>Also supported: `"none"`, `"overline"`, `"line-through"`, `"inherit"`
Horizontal Alignment | `cells[i].style.horizontalAlignment` | string | The horizontal alignment of the content.<br/>`"horizontalAlignment": "start"`<br/>Also supported: `"middle"`, `"end"`
Vertical Alignment | `cells[i].style.verticalAlignment` | string | The vertical alignment of the content.<br/>`"verticalAlignment": "hanging"`<br/>Also supported: `"middle"`, `"baseline"`
Background Color | `cells[i].style.backgroundColor` | hex/string | The background color of the content.<br/>`"backgroundColor": "#F7F7F7"`<br/>`"backgroundColor": "gray"`

## 5. Simple Connector Styling

### Sample Template
This partial template highlights a simple connector style.

```(JSON)
{
    "style": {
        "color": "black",
        "weight": 2,
        "arrowhead": {
            "color": "black",
            "height": 17,
            "width": 7
        }
    }
}
```

### Cell Connector Properties
The following properties are supported for styling simple connectors.

Name | Path | Type | Example
-----|------|------|-------------
Color | `style.color` | hex/string | The color of the connector line.<br/>`"color": "#000000"`<br/>`"color": "black"`
Weight | `style.weight` | integer | The weight of the connector line.<br/>`"weight": 2`
Arrowhead | `style.arrowhead` | object | The size and color of arrowhead which will be located near target node.
.... Arrowhead Color | `style.arrowhead.color` | hex/string | The arrowhead color.<br/>`"arrowhead": {"color": "#000000"}`<br/>`"arrowhead": {"color": "black"}`
.... Arrowhead Height | `style.arrowhead.height` | integer | The arrowhead height.<br/>`"arrowhead": {"height": 17}`
.... Arrowhead Width | `style.arrowhead.width` | integer | The arrowhead width.<br/>`"arrowhead": {"width": 7}`

## 6. Sample Template

The following sample template can be used as a starting point for a View Card.

```(JSON)
{
    "container": {
        "type": "grid",
        "style": {
            "width": 200,
            "height": 90,
            "color": "#F7F7F7",
            "padding": {
                "left": 12,
                "right": 12,
                "top": 12,
                "bottom": 12
            },
            "rows": [
                {
                    "height": 20
                },
                {
                    "height": 16
                },
                {
                    "height": 16
                },
                {
                    "height": 16
                }
            ],
            "cols": [
                {
                    "width": 22
                },
                {
                    "width": 120
                },
                {
                    "width": 35
                }
            ],
            "border": {
                "width": 1,
                "color": "#555555",
                "cornerRadius": 2,
                "shadow": {
                    "horizontal": 2,
                    "vertical": 3,
                    "color": "#000000",
                    "opacity": 0.5
                }
            },
            "cells": [
                {
                    "content": "image",
                    "content_binding": "icon",
                    "col": 0,
                    "row": 0
                },
                {
                    "content": "text",
                    "content_binding": "keyed_name",
                    "col": 1,
                    "row": 0
                },
                {
                    "content": "text",
                    "content_binding": "generation",
                    "col": 2,
                    "row": 0,
                    "style": {
                        "verticalAlignment": "top",
                        "horizontalAlignment": "end",
                        "font": {
                            "size": 10,
                            "family": "Tahoma",
                            "weight": "normal",
                            "color": "#777777"
                        }
                    }
                },
                {
                    "content": "text",
                    "content_binding": "name",
                    "col": 1,
                    "row": 1,
                    "style": {
                        "font": {
                            "size": 12,
                            "family": "Tahoma",
                            "weight": "normal",
                            "color": "#333333"
                        }
                    }
                },
                {
                    "content": "text",
                    "content_binding": "classification",
                    "col": 1,
                    "row": 2,
                    "style": {
                        "font": {
                            "size": 10,
                            "family": "Tahoma",
                            "weight": "normal",
                            "color": "#333333"
                        }
                    }
                },
                {
                    "content": "text",
                    "content_binding": "state",
                    "col": 1,
                    "row": 3,
                    "style": {
                        "font": {
                            "size": 10,
                            "family": "Tahoma",
                            "weight": "normal",
                            "color": "#777777"
                        }
                    }
                }
            ]
        }
    },
    "style": {
        "arrowhead": {
            "height": 17,
            "width": 7
        }
    }
}
```