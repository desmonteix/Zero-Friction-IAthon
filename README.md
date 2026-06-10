# Pencorp: Seguros Embebidos sin Fricción

![Estado](https://img.shields.io/badge/Estado-MVP_Completado-success)
![Contexto](https://img.shields.io/badge/Evento-IAthon_Pacífico_Seguros-blue)
![Tech](https://img.shields.io/badge/Stack-n8n_%7C_Supabase_%7C_OpenAI-black)

## Descripción del Proyecto
Solución desarrollada para el Reto 3 de la IAthon de Pacífico Seguros y la Universidad del Pacífico. 

Este proyecto resuelve el dilema operativo de la venta de seguros embebidos: capturar datos del cliente sin generar fricción en la interfaz web ni comprometer la cadena de postventa. La arquitectura transforma un proceso de llenado de formularios tradicional en una experiencia conversacional asíncrona mediante WhatsApp, implementando Inteligencia Artificial (OpenAI Vision) exclusivamente en el entorno de backend para la extracción estructurada de datos (OCR de documentos de identidad).

## Características Principales
* **Punto de Venta (POS) Universal:** Interfaz HTML ligera diseñada para socios comerciales (retail, telecomunicaciones) que permite iniciar el flujo con el ingreso del DNI, eliminando la necesidad de integraciones de API complejas.
* **Máquina de Estados Asíncrona:** Orquestación automatizada que detecta la intención de compra y gestiona la comunicación proactiva hacia el cliente vía WhatsApp.
* **Extracción OCR de Alta Precisión:** El usuario proporciona una fotografía de su documento de identidad. El sistema extrae nombres, apellidos y número de documento en milisegundos mediante modelos de visión computacional.
* **Gobierno de IA y Mitigación de Riesgos:** El modelo de Inteligencia Artificial no interactúa directamente con el usuario final, mitigando el riesgo legal de alucinación de coberturas. Su uso se restringe a un motor de procesamiento de datos en el servidor.
* **Cierre de Ciclo Automatizado:** Generación de la póliza en formato PDF mediante codificación Base64 y envío automatizado de correo electrónico transaccional corporativo.

## Arquitectura de 3 Capas (Tiers)
La solución opera bajo un modelo estructurado y escalable:

1. **Tier 1 (Interfaz y Captura):** 
   * Portal HTML/CSS para el registro inicial del socio comercial.
   * Integración con WhatsApp (vía Evolution API) como canal principal de captura de datos asíncrona.
2. **Tier 2 (Orquestación Lógica):** 
   * Flujo de automatización centralizado en **n8n**. Administra la recepción de webhooks, valida el estado de la transacción y enruta la información.
3. **Tier 3 (Backend y Procesamiento):** 
   * **Supabase** (PostgreSQL) para el almacenamiento relacional de los registros.
   * **OpenAI (GPT-4o Vision)** para el procesamiento de imágenes y entrega de datos estructurados en formato JSON.

## Configuración y Despliegue
Requisitos para replicar la arquitectura en un entorno local o servidor en la nube:

### 1. Variables de Entorno y Credenciales
Se requiere la configuración de las siguientes credenciales en la instancia de n8n:
* Claves de API y URL del proyecto en Supabase.
* Clave de API de OpenAI.
* Credenciales de Evolution API conectadas a una instancia activa de WhatsApp.
* Credenciales de servidor SMTP para notificaciones por correo electrónico.

### 2. Estructura de Base de Datos
La tabla principal en PostgreSQL debe contener los siguientes campos mínimos:
* `id` (UUID)
* `dni` (Varchar)
* `nombres_completos` (Varchar)
* `celular` (Varchar)
* `email` (Varchar)
* `estado` (Varchar) - Ej. 'Esperando_Documento', 'Póliza_Emitida'.

### 3. Importación del Flujo
1. Descargar el archivo `workflow.json` disponible en este repositorio.
2. Acceder a la instancia de n8n, seleccionar la opción "Import from File" y cargar el documento.
3. Configurar los nodos con las credenciales correspondientes al entorno de desarrollo.

## Conclusiones Técnicas (IAthon)
* **Optimización de Conversión Asíncrona:** Desplazar la carga operativa hacia un canal de uso cotidiano (WhatsApp) reduce sustancialmente las tasas de abandono en procesos de contratación.
* **Gobernanza Tecnológica:** En el sector Insurtech, confinar los modelos generativos a tareas deterministas previene vulnerabilidades de cumplimiento y estandariza la calidad de los datos recopilados.

---
**Desarrollado por:**  
Matías Desmonteix
