 🧠 Sistema de Análisis de Reseñas y Sentimientos de Usuarios  
#Proyecto: 03_QuantumStack  
**Tecnologías utilizadas:** MongoDB | Python | NLP | Streamlit

---

#Descripción del proyecto
El sistema tiene como objetivo **analizar reseñas escritas por usuarios** y determinar automáticamente el **sentimiento predominante** (positivo, negativo o neutral).  
Utiliza técnicas de **Procesamiento de Lenguaje Natural (NLP)** para interpretar el texto y almacenar los resultados en una base de datos **MongoDB**, lo que permite su posterior análisis y visualización mediante un panel interactivo.

El proyecto busca facilitar la **evaluación automática de opiniones de clientes** sobre productos o servicios, reduciendo el tiempo de análisis manual y mejorando la toma de decisiones.

---
#Integrantes del equipo

| Nombre completo | GitHub / Correo |
|------------------|----------------|
| Julio César Hernández Santiago | jchersa@outlook.com |
| Keneth Chinchilla | keneth.chinchilla31@gmail.com |
| David Hernández | david.hernandezv7@gmail.com |
| José Felipe Inestroza | josefelipeinestrozabanegas@gmail.com |
| Fernando Mejía | fm_mejiap@unicah.edu |

---

#Instrucciones de ejecución

1. Creacion del Cluster en MongoDB

Como primer paso se debe realizar la creacion y configuracion en MongoDB donde se alojara la base de datos para almacenar y administrar nuestros datos.
 <img width="1771" height="803" alt="image" src="https://github.com/user-attachments/assets/d4eb746c-57bc-4fd6-bc77-f6c5d2085116" />

2. Descargar archivos CSV
Es necesario obtener los archivos CSV que contienen la información base utilizada en la base de datos. Estos archivos incluyen datos de las reviews y los usuarios. Los archivos CSV se encuentran en la ruta '/documentacion/Datasets/Datasets.zip'  y asegúrate de mantener la estructura y nombres originales de los archivos para evitar errores en los pasos posteriores de carga e importación.

3. Conexion a MongoDB, Data Wrangling e Insercion de los datos en MongoDB.
En la carpeta scripts encontrarás el notebook ProyectoBDO.ipynb, que debe abrirse con Google Colab. Este notebook guía paso a paso el flujo completo: establecer la conexión segura con la base de datos MongoDB (usando URI o variables de entorno), realizar el data wrangling necesario (limpieza, transformación y normalización de los CSV), y finalmente insertar los datos en las colecciones correspondientes de MongoDB. Sigue las celdas en orden, provee las credenciales solicitadas.

<img width="999" height="504" alt="image" src="https://github.com/user-attachments/assets/7eb715cc-1a5a-48de-aaa2-dc9063ca3016" />

4. Implementacion de Modelos con Machine Learning para el Analisis de Sentimiento.
   4.1. Modelo Regression Logistic
   4.2. Modelo Bert

5. Conexión de Power BI con MongoDB Atlas y creación del Dashboard de Experiencia Disneyland
6. Este proyecto tuvo como propósito conectar MongoDB Atlas, una base de datos NoSQL en la nube, con Power BI, para analizar más de 40,000 reseñas y datos asociados a visitantes de parques Disneyland en diferentes países. El resultado final fue un dashboard interactivo que permite explorar patrones de opinión, puntajes, hábitos de usuarios y ubicaciones geográficas.
6.1. Organización de datos en MongoDB Atlas
El proceso inició preparando las colecciones necesarias en un clúster de MongoDB Atlas:
 reviews
 users
 parks
 location

Cada colección almacenaba información clave: reseñas textuales, usuarios, detalles de parques y sus ubicaciones geográficas.

6.2. Instalación del controlador oficial ODBC de MongoDB
Para que Power BI pueda "leer" bases de datos MongoDB, es obligatorio instalar el MongoDB Atlas SQL ODBC Driver, el cual traduce documentos BSON en tablas relacionales compatibles con Power BI.
Una vez instalado, esto habilita el siguiente paso crucial: Data Federation.

6.3. Configuración de MongoDB Atlas Data Federation

Power BI no se conecta directamente a colecciones MongoDB sin un esquema relacional.
Para solucionar esto, MongoDB proporciona Data Federation, una capa que:

Virtualiza colecciones NoSQL en tablas relacionales
Data Federation crea un Virtual Database (VirtualDatabase0) que expone colecciones como si fueran tablas SQL.

Genera un endpoint SQL
Este endpoint SQL es el que Power BI usa a través del ODBC.

Pasos realizados:
Se creó una instancia de Data Federation en MongoDB Atlas.
Se conectó el clúster principal como fuente de datos.
Se configuró un pipeline que mapea automáticamente las colecciones a tablas virtuales.
Se verificó que el VirtualDataBase generara el esquema tabular accesible desde ODBC.

Con esto, Atlas queda preparado para ser consultado desde herramientas SQL, incluyendo Power BI.

6.4. Creación del DSN (Data Source Name) en Windows

Luego, en el Administrador de ODBC de Windows:
 Se seleccionó el controlador MongoDB Atlas SQL ODBC Driver.
 Se creó un DSN llamado AtlasSQLDisney.
 Se ingresó:
  El endpoint SQL generado por Data Federation.
  El usuario de lectura de MongoDB.
  La base virtual: VirtualDatabase0.

Finalmente, se probó la conexión desde el panel ODBC y el sistema confirmó:
“Connected successfully with supplied information.”

6.5. Conectando Power BI a MongoDB Atlas con ODBC

En Power BI Desktop:
 Se abrió Obtener datos > ODBC.
 Se seleccionó el DSN “AtlasSQLDisney”.
 Se ingresaron las credenciales del usuario.
 Power BI cargó las tablas virtualizadas:
  reviews
  users
  parks
  location

Estas representaban las colecciones, pero ahora en formato tabular gracias a Data Federation.

6.6. Limpieza y transformación en Power Query
Con los datos dentro de Power BI:
 Se ajustaron tipos de dato (especialmente fechas).
 Se corrigieron errores en la conversión de la columna Year_Month.
 Se eliminaron columnas innecesarias como _id (ObjectId).
 Se crearon nuevas columnas derivadas:
   Día numérico
   Mes numérico
   Año
   Nombre del día
   Nombre del mes
Se normalizaron relaciones entre tablas usando parks_id y user_id.

6.7. Modelado de datos
 Se construyó un modelo relacional tipo estrella (star schema):
   reviews → parks (por parks_id)
   reviews → users (por user_id)
   parks → location (por location)
Esto permitió que Power BI entendiera el flujo de relaciones entre visitantes, reseñas, parques y geografías.

6.8. Construcción del Dashboard de Experiencia Disneyland
 Con el modelo final listo, se diseñaron visualizaciones clave:
   Gráficos de barras con calificaciones promedio por parque.
   Tablas con volumen de reseñas.
   Filtros por país, parque, temática y año.
   Mapa geográfico usando los campos de location.
   Tarjetas de KPI, mostrando totales y promedios.
El dashboard resultante permite explorar patrones globales de opinión, comparaciones entre parques, tendencias temporales y comportamiento de visitantes.

6.9 Conclusión
El proceso demostró cómo transformar una base de datos NoSQL compleja en una fuente analítica totalmente compatible con Power BI mediante:
   MongoDB Atlas Data Federation
   MongoDB Atlas SQL ODBC Driver
   Power BI Desktop

El resultado fue un dashboard profesional, completamente automatizado y capaz de analizar más de 40,000 opiniones de usuarios sobre Disneyland.

#Clonar el repositorio
```bash
git clone https://github.com/Unicah-MGI/03_QuantumStack.git
cd 03_QuantumStack
