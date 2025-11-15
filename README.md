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

5. Dashboard


#Clonar el repositorio
```bash
git clone https://github.com/Unicah-MGI/03_QuantumStack.git
cd 03_QuantumStack
