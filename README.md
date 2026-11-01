# Agente Recursos: Sistema de Desarrollo de Software Multiagente

## Descripción general

Este repositorio contiene el código fuente de **Agente Recursos**, un sistema automatizado basado en agentes de inteligencia artificial (IA) diseñado para gestionar y ejecutar el ciclo de vida completo del desarrollo de software.

El proyecto orquesta un conjunto de agentes especializados que simulan los roles de un equipo de desarrollo tecnológico. Mediante modelos de lenguaje de gran escala (LLM), integrados a través de la API de Groq, el sistema es capaz de analizar requisitos, diseñar la arquitectura, escribir código, realizar pruebas y preparar el entorno de despliegue de forma autónoma.

## Demostración en línea

El proyecto generado se encuentra desplegado en Render y puede probarse sin necesidad de instalación local:

* **URL base de la API:** https://talentcore-api-idkardo.onrender.com
* **Documentación interactiva (Swagger UI):** https://talentcore-api-idkardo.onrender.com/docs
* **Documentación alternativa (ReDoc):** https://talentcore-api-idkardo.onrender.com/redoc

> **Nota:** el servicio se aloja en el plan gratuito de Render, por lo que puede entrar en suspensión tras un periodo de inactividad. La primera solicitud podría tardar entre 30 y 60 segundos en responder mientras el servicio se reactiva.

## Arquitectura del sistema

El flujo de trabajo se divide en etapas secuenciales, cada una dirigida por un agente especializado:

1. **Product Owner** (`01_agente_product_owner.py`): interpreta las necesidades del usuario, define los requisitos funcionales y establece la visión del producto.
2. **Arquitecto de Software** (`02_agente_arquitecto.py`): diseña la estructura del sistema, selecciona las tecnologías adecuadas (por ejemplo, FastAPI) y define las interfaces de comunicación.
3. **Desarrollador** (`03_agente_developer.py`): implementa el código fuente de la aplicación conforme a las especificaciones del Arquitecto.
4. **Ingeniero de QA (Quality Assurance)** (`04_agente_qa.py`): desarrolla y ejecuta pruebas automatizadas para garantizar el correcto funcionamiento del código.
5. **Revisor de Código (Reviewer)** (`05_agente_reviewer.py`): analiza el código generado con el fin de detectar vulnerabilidades, verificar el cumplimiento de las buenas prácticas y proponer optimizaciones.
6. **Ingeniero DevOps** (`06_agente_devops.py`): configura los contenedores mediante Docker y Docker Compose, y establece los flujos de integración y despliegue continuos (CI/CD) a través de GitHub Actions.

## Tecnologías utilizadas

* **Lenguaje principal:** Python 3.x
* **Framework web (proyecto generado):** FastAPI
* **Inteligencia artificial:** API de Groq
* **Contenerización:** Docker y Docker Compose
* **CI/CD:** GitHub Actions
* **Despliegue:** Render
* **Gestión de entornos:** `venv` y `python-dotenv`

## Estructura del directorio

```text
taller_agentes_sdlc/
├── 01_agente_product_owner.py
├── 02_agente_arquitecto.py
├── 03_agente_developer.py
├── 04_agente_qa.py
├── 05_agente_reviewer.py
├── 06_agente_devops.py
├── generated_project/
│   ├── app/
│   │   ├── main.py
│   │   └── models.py
│   ├── tests/
│   ├── Dockerfile
│   ├── docker-compose.yml
│   ├── probar_api.py
│   └── .github/workflows/
├── requirements.txt
└── README.md

Requisitos previos
Para ejecutar este proyecto en un entorno local, se requiere lo siguiente:

Python 3.11 o superior.

Docker y Docker Compose instalados en el sistema.

Una clave de API válida proporcionada por Groq.

Instalación y configuración local
Clonar el repositorio:

Bash
git clone https://github.com/Emiliano-zap/talentcore-api.git
cd generated_project
Crear y activar el entorno virtual:

Bash
python -m venv venv

# En Windows:
venv\Scripts\activate

# En macOS/Linux:
source venv/bin/activate
Instalar las dependencias:

Bash
pip install -r requirements.txt
Iniciar el servidor Uvicorn:

Bash
uvicorn app.main:app --reload
Ejecutar la suite de pruebas automatizadas:

Bash
python probar_api.py
🐳 Ejecución con Docker
Para levantar el microservicio en un contenedor aislado:

Bash
docker-compose up --build
La documentación interactiva estará accesible localmente en http://localhost:8000/docs.

☁️ Configuración de Despliegue en Render
El servicio está configurado en Render con los siguientes parámetros de ejecución:

Build Command: pip install --no-cache-dir -r requirements.txt

Start Command: uvicorn app.main:app --host 0.0.0.0 --port $PORT

🛡️ Auditoría de Ciberseguridad (SAST / OWASP)
El análisis de seguridad determinó la mitigación de los siguientes riesgos principales:

API5 (Broken Function Level Authorization): Control de acceso mediante verificación del encabezado X-User-Id y jerarquía de roles (ADMIN_RRHH, MANAGER, EMPLEADO).

API1 (BOLA / IDOR): Validación estricta de asignación directa (manager_id) para impedir que un usuario apruebe solicitudes de otros departamentos.