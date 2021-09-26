# Análisis de datos de delitos CABA

Se realiza un proceso etl utilizando los datos publicos de delitos de CABA brindado por el gobierno de la ciudad autonoma de buenos aires.

&nbsp;

## Fuente de datos

Los datos utilizados son de los años 2019 y 2020 para nuestro análisis.

Delitos 2020:
```url
https://cdn.buenosaires.gob.ar/datosabiertos/datasets/ministerio-de-justicia-y-seguridad/delitos/delitos_2020.csv
```

Delitos 2019:
```url
https://cdn.buenosaires.gob.ar/datosabiertos/datasets/ministerio-de-justicia-y-seguridad/delitos/delitos_2019.csv
```

&nbsp;

## Proceso

El proceso de tranformación se realizó con la app Talent Open Studio.  

&nbsp;

## Visualización

Requisitos:

* Power BI desktop
```url
https://powerbi.microsoft.com/es-es/
```

El archivo del tablero es ***"Analisis delitos CABA .pbix"***


&nbsp;

## Base de datos

Los datos de la base de datos son:  
- **Tipo:** MySQL  
- **Server:** 127.0.0.1  
- **Port:** 3306  
- **Base de datos:** db_caba  
- **Usuario:** db_user  
- **Password:** ver archivos secrets  
- **Tablas:**
  * delitos_2019
  * delitos_2020
  * delitos_historicos
  * talend_stats

*Se utilizo MySQL pero podria reemplazarse con cualquier otro tipo de base de datos.*

&nbsp;

## Instalación

Requisitos:

* Docker

```url
https://www.docker.com/get-started
```

* Java 8

```url
https://www.oracle.com/java/technologies/downloads/#java8
```

```url
https://java.tutorials24x7.com/blog/how-to-install-java-8-on-windows-10
```

```url
https://medium.com/@devkosal/switching-java-jdk-versions-on-macos-80bc868e686a
```

&nbsp;

1. Clonar repositorio

```url
https://github.com/ezeparziale/analisis-data-delitos
```

2. Descargar Talend Open Studio

```
https://www.talend.com/products/talend-open-studio/
```

3. Pasos de instalación
```
https://help.talend.com/r/Je8asIdye4c8h1JTL~NcVQ/7ujZ9bjh8IA~zh8LJjsRPw
```

Recomendado en windows dejarlo en ***C:\talend***

&nbsp;

## Ejecución

1. Ejecutar Talend e importar el workspace que se encuentra dentro de la carpeta ***"talend"*** dentro del repositorio.

2. Ejecutar el archivo ***docker-compose.yaml***

```terminal
docker-compose -f "docker-compose.yaml" up -d
```

3. Ejecutar procesos en talend:

Dentro del workspace se encuentran los siguientes jobs:

&nbsp;

* Delitos_2019
  
Descarga el archivo CSV y lo guarda en la base de datos MySQL, tabla "delitos_2019"

&nbsp;
* Delitos_2020
 
Descarga el archivo CSV y lo guarda en la base de datos MySQL, tabla "delitos_2020"

&nbsp;
* Delitos_historicos

Se procesan las tablas "delitos_2019" y "delitos_2020", se normalizan campos y se vincula la info del csv llamado "./extras/franja_horaria.csv"

&nbsp;
* Job_Recarga_Delitos_CABA

Es el job principal que ejecuta los job de transformaciones en el siguiente orden: "delitos_2019" >> "delitos_2020" >> "Delitos_historicos"

&nbsp;

## Estructura de carpetas

```
analisis-data-delitos
│   Readme.md
│   docker-compose.yaml    
│   Analisis delitos CABA.pbix
|
└───csv
|   │   delitos_2019.csv
|   │   delitos_2020.csv
|   | 
└───db_data
|   │   ...
|   |
└───extras
|   │   franja_horaria.csv
|   |
└───img
|   │   portada.jpg
|   |
└───map
|   │   map_barrios.topojson
|   │   map_comunas.topojson
|   |
└───secrets
|   │   db_password
|   │   db_root_password
|   |
└───talend
|   └───WORKSPACE_TALEND_DELITOS_CABA
|       |   ...
```



## Bibliografia

Datos publicos del gobierno de la ciudad:
```url
https://data.buenosaires.gob.ar/dataset/delitos
```