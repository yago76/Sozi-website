Title: Preguntas Frecuentes (FAQ) y Resolución de Problemas
Slug: faq
Lang: ee
Author: Santiago Rodríguez
Status: hidden

¿Cómo establezco un color de fondo?
-----------------------------------

Inkscape permite establecer un color de fondo en la ventana de *propiedades del documento*.
Desafortunadamente, el color elegido sólo se puede ver en Inkscape y en imágenes exportadas desde el documento.
El color de fondo es ignorado por los exploradores web.

Para establecer un color de fondo visible en un explorador web, se puede usar
el editor XML proporcionado con Inkscape.
Selecionando el elemento raíz `<svg:svg>`, añade un elemento hijo `<svg:style>` y un nodo de texto dentro de él como en la siguiente captura de pantalla:

![Establecer un color de fondo en Inkscape](|filename|/images/faq/background.png)

> Cambia `rgb(255, 200, 255)` por el color que elijas [CSS color](https://developer.mozilla.org/en/docs/Web/CSS/color_value).

Si prefieres usar un editor de texto, abre el documento SVG
y añade el siguiente elemento como un hijo del elemento ráiz `<svg>`:

    :::xml
    <style>
        svg {
            background: rgb(255, 200, 255);
        }
    </style>


Algunos gráficos no se renderizan correctamente cuando se ejecuta mi presentación de Sozi
-----------------------------------------------------------------------------------------

Bastantes usuarios han informado acerca de problemas cuando sus documentos SVG continen 
*texto fluido*, por ejemplo, texto que se ajusta automáticamente dentro de una forma (un rectángulo en Inkscape).
Esta característica, actualmente, no es estable en los estándares de SVG.
La wiki de Inkscape aporta [explicaciones acerca de este tema](http://wiki.inkscape.org/wiki/index.php/FAQ#What_about_flowed_text.3F) con el siguiente aviso:

> [...] no debes usar texto fluido en documentos que están destinados a usarse fuera de Inkscape.

De un modo general, Sozi no es lo que renderiza el documento en pantalla.
Eso lo hace el explorador de internet.
Sozi sólo gestiona la lógica de *presentación*: aplicar transformaciones geométricas a
las capas del documento, controlar la animación, reaccionar a las acciones del usuario.

Si algunos gráficos no se renderizan correctamente,
es más probable que el problema venga del editor SVG o del explorador de inernet.
Por favor, no nos envíes informes de fallos de este tipo a no se que estés realmente convencido de que el problema viene de Sozi.
Si tienes dudas al respecto, puedes pedir consejo en [grupo de discusion de usuarios de Sozi](http://groups.google.com/group/sozi-users).


Inkscape muestra un error de sintaxis al utilizar Sozi 13
---------------------------------------------------------

Este problema ha sido notificado principalmente por usuarios de Windows.
Cuando se ejecuta Sozi desde el menú de extensiones de Inkscape, una ventana muestra el siguiente error:

    :::pytb
    Traceback (most recent call last):
      File "sozi.py", line 30, in from sozi.document import *
      File "C:\Program Files (x86)\Inkscape\share\extensions\sozi\document.py", line 96
        self.layers = { l.attrib[group_attr] : SoziLayer(self, l) for l in self.xml.xpath("sozi:layer", namespaces=inkex.NSS) if group_attr in l.attrib }
    SyntaxError: invalid syntax

Este error ocurre cuando Inkscape intenta ejecutar Sozi usando Python 2.6 en vez de Python 2.7.
Habitualmente, suele ser porque Python 2.7 no ha sido instalado, o no está en la ruta adecuada.
Verifica que has seguido correctamente las [instrucciones de instalación](http://sozi.baierouge.fr/pages/install-windows.html).

Aunque está por confirmar, parece que algunos usuarios obtienen este error cuando instalan la versión 
*portable* de Inkscape. Por favor, utiliza el *instalador* en vez de la versión *portable*.