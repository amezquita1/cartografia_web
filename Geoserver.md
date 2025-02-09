# Geoserver

Descripción de la configuración de geoserver generada para la clase

- [Geoserver](#geoserver)
  - [Requerimientos](#requerimientos)
  - [Procedimiento utilizado para configurar la versión](#procedimiento-utilizado-para-configurar-la-versi%C3%B3n)
  - [Ejecutar Tomcat](#ejecutar-tomcat)
  - [Presentaciones](#presentaciones)
  - [Ejemplo estilos](#ejemplo-estilos)

## Instalador de geoserver para windows

Utilizar la versión **"Windows Installer"** disponible en http://geoserver.org/release/stable/

## Requerimientos instalación manual con tomcat

- Java 8 https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html
  - Tutorial : ¿Cómo puedo descargar e instalar Java en un equipo con Windows de forma manual? https://www.java.com/es/download/help/windows_manual_download.xml
- Instalar Apache Tomcat en Windows https://tutobasico.com/instalar-tomcat-windows/

## Procedimiento utilizado para configurar la versión

Se utilizaron las instrucciones publicadas en https://docs.geoserver.org/latest/en/user/installation/war.html

- Se descargó la versión **Web Archive** de GeoServer 2.15.1 desde la página oficial http://geoserver.org/release/stable/
- Se descargó la versión \__zip_ de de apache tomcat 9.0.20 desde la página oficial https://tomcat.apache.org/download-90.cgi
- Se descomprimió el archivo zip de apache tomcat (apache-tomcat-9.0.20.zip)
- Se descomprimió el archivo zip de geoserver (geoserver-2.15.1-war.zip)
- Se copió el archivo **geoserver.war** dentro de la carpeta **apache-tomcat-9.0.20/webapps/**
- Se inició tomcat. La aplicación descomprime el contenido del archivo **geoserver.war** en la carpeta **apache-tomcat-9.0.20/webapps/geoserver**
- Detener geoserver
- Extensiones
  - Adicionar extensiones: Para instalar las extensiones debe descargar el archivo zip de la extensión en particular, descomprimirlo y compiar los archivos **.jar** en la carpeta **apache-tomcat-9.0.20/webapps/geoserver/WEB-INF/lib**
  - Para la presente configuración se adicionaron las siguientes extensiones:
    - CSS Styling https://docs.geoserver.org/latest/en/user/styling/css/index.html
    - YSLD Styling https://docs.geoserver.org/latest/en/user/styling/ysld/index.html
    - MBStyle Styling https://docs.geoserver.org/latest/en/user/styling/mbstyle/index.html
    - Vector tiles https://docs.geoserver.org/latest/en/user/extensions/vectortiles/index.html
- Datos
  - Además de los datos que vienen de ejemplo por omisión se adicionaron los siguientes conjuntos de datos:
    - OpenStreetMap de Colombia descargado desde geofabrik (formato shp)
      - Url descarga: https://www.geofabrik.de/data/download.html
      - Diccionario de datos: http://download.geofabrik.de/osm-data-in-gis-formats-free.pdf
      - Ruta de los datos **apache-tomcat-9.0.20/webapps/geoserver/data/data/openstreetmap_colombia.shp**
  - Natural Earth (países, centros poblados)
    - Url descarga: https://www.naturalearthdata.com/downloads/110m-cultural-vectors/
    - Ruta de los datos **apache-tomcat-9.0.20/webapps/geoserver/data/data/natural_earth**

## Ejecutar Tomcat

Para iniciar el servidor apache tomcat:

- En Windows : Ejecutar el archivo **apache-tomcat-9.0.20/bin/startup.bat**
- En Linux o Mac: Ejecutar el archivo **apache-tomcat-9.0.20/bin/startup.sh**

* Luego de iniciar la aplicación debe poder acceder a tomcat a través del siguiente enlace http://localhost:8080/geoserver/
* Deberá ver una pantalla similar a la siguiente:

![tomcat_start](images/tomcat_start.png "tomcat_start")

- Contraseña de administrador default:
  - Usuario: admin
  - Clave: geoserver

Para detener tomcat:

- En Windows : Ejecutar el archivo **apache-tomcat-9.0.20/bin/shutdown.bat**
- En Linux o Mac: Ejecutar el archivo **apache-tomcat-9.0.20/bin/shutdown.sh**

## Presentaciones

- GeoServer, an introduction for beginners https://es.slideshare.net/geosolutions/geoserver-an-introduction-for-beginner
- State of GeoServer 2.14 https://es.slideshare.net/jgarnett/state-of-geoserver-214
- GeoServer in Production: we do it, here is how! https://www.slideshare.net/geosolutions/geoserver-in-production-we-do-it-here-is-how-foss4g-2016
- Advanced Security with GeoServer - FOSS4G 2015 https://www.slideshare.net/geosolutions/advanced-security-with-geoserver-foss4g-2015

## Ejemplo estilos

CSS

```css
/* @title Construccion Rural */
* {
  [@sd > 1k][@sd < 70k] {
    stroke: #e1e1e1;
    stroke-width: 1;
    fill: #ecf0f1;
    fill-opacity: 1;
  }
}
```

SLD

```xml
<?xml version="1.0" encoding="UTF-8"?><sld:StyledLayerDescriptor xmlns="http://www.opengis.net/sld" xmlns:sld="http://www.opengis.net/sld" xmlns:gml="http://www.opengis.net/gml" xmlns:ogc="http://www.opengis.net/ogc" version="1.0.0">
  <sld:NamedLayer>
    <sld:Name>Default Styler</sld:Name>
    <sld:UserStyle>
      <sld:Name>Default Styler</sld:Name>
      <sld:FeatureTypeStyle>
        <sld:Rule>
          <sld:Title>Construccion Rural</sld:Title>
          <sld:MinScaleDenominator>1000.0</sld:MinScaleDenominator>
          <sld:MaxScaleDenominator>70000.0</sld:MaxScaleDenominator>
          <sld:PolygonSymbolizer>
            <sld:Fill>
              <sld:CssParameter name="fill">#ECF0F1</sld:CssParameter>
            </sld:Fill>
            <sld:Stroke>
              <sld:CssParameter name="stroke">#E1E1E1</sld:CssParameter>
            </sld:Stroke>
          </sld:PolygonSymbolizer>
        </sld:Rule>
        <sld:VendorOption name="ruleEvaluation">first</sld:VendorOption>
      </sld:FeatureTypeStyle>
    </sld:UserStyle>
  </sld:NamedLayer>
</sld:StyledLayerDescriptor>
```
