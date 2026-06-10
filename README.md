# 🛡️ Pencorp: Seguros Embebidos sin Fricción

![Estado](https://img.shields.io/badge/Estado-MVP_Completado-success)
![Contexto](https://img.shields.io/badge/Evento-IAthon_Pacífico_Seguros-blue)
![Tech](https://img.shields.io/badge/Stack-n8n_%7C_Supabase_%7C_OpenAI-black)

## 📌 Descripción del Proyecto
Solución desarrollada para el **Reto 3 de la IAthon de Pacífico Seguros y la Universidad del Pacífico**. 

Este proyecto resuelve el dilema de la venta de seguros embebidos: capturar datos del cliente sin generar fricción web ni romper la cadena de postventa. Transformamos un formulario web tedioso en una experiencia conversacional asíncrona mediante WhatsApp, utilizando Inteligencia Artificial (OpenAI Vision) exclusivamente en el backend para la extracción estructurada de datos (OCR de documentos de identidad).

## 🚀 Características Principales (Features)
* **Punto de Venta (POS) Universal:** Interfaz HTML ultraligera para socios comerciales (retails, telcos) que inicia el flujo con solo ingresar el DNI, sin necesidad de integraciones API complejas.
* **Máquina de Estados Asíncrona:** Orquestación inteligente que detecta el abandono y gestiona la comunicación proactiva por WhatsApp.
* **Extracción OCR Cero-Fricción:** El cliente solo envía una foto de su DNI. El sistema extrae `nombres`, `apellidos` y `número de documento` en milisegundos usando modelos de visión.
* **Gobierno de IA y Mitigación de Riesgos:** La IA no interactúa con el usuario final (evitando alucinaciones de coberturas). Se utiliza estrictamente como un motor de extracción en el *backend*.
* **Cierre de Journey Automatizado:** Generación e inyección de póliza PDF vía Base64 y envío de correo transaccional en formato HTML corporativo.

## 🏗️ Arquitectura de 3 Capas (Tiers)
Nuestra solución opera bajo un modelo robusto y escalable:

1. **Tier 1 (Interfaz):** 
   * Portal HTML/CSS para el inicio rápido de la venta por parte del socio comercial.
   * WhatsApp (Evolution API) como canal de interacción asíncrona con el cliente.
2. **Tier 2 (Orquestador):** 
   * Flujo de automatización construido en **n8n**. Actúa como el cerebro que gestiona los webhooks, valida los estados y enruta la información.
3. **Tier 3 (Backend e IA):** 
   * **Supabase** (PostgreSQL) para el almacenamiento estructurado y en tiempo real.
   * **OpenAI (GPT-4o Vision)** para el procesamiento asíncrono de imágenes y extracción de datos en formato JSON nativo.

## ⚙️ Configuración e Instalación
Para replicar este flujo en un entorno local o de servidor (ej. Easypanel):

### 1. Variables de Entorno y Credenciales
Necesitarás configurar las siguientes credenciales en n8n:
* `Supabase API Key` y `URL` de tu proyecto.
* `OpenAI API Key`.
* `Evolution API Key` y credenciales de instancia conectada a WhatsApp.
* Credenciales SMTP / Gmail para el envío de correos.

### 2. Base de Datos (Supabase)
La tabla principal debe contener la siguiente estructura básica:
* `id` (UUID)
* `dni` (Varchar)
* `nombres_completos` (Varchar)
* `celular` (Varchar)
* `email` (Varchar)
* `estado` (Varchar) - *Ej: Esperando_Foto, Emitido.*

### 3. Importar el Flujo de n8n
1. Descarga el archivo `workflow.json` de este repositorio.
2. En tu instancia de n8n, selecciona **Import from File** y carga el archivo.
3. Reconecta tus credenciales en los nodos correspondientes.

## 📝 Lecciones Aprendidas (IAthon)
* **El diseño asíncrono salva conversiones:** Permitir que el cliente complete el proceso a su propio ritmo por WhatsApp reduce drásticamente el abandono.
* **El Gobierno de IA es un requisito, no un extra:** En la industria *insurtech*, limitar la IA a tareas deterministas (como lectura de datos) previene riesgos legales asociados a alucinaciones.

---
**Desarrollado por Matías**  
*Fundador de Pencorp | Estudiante de Ingeniería Empresarial*
