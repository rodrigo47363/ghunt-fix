# 🔍 GHunt Hotfix — Google People API Parser Patch

[![Python](https://img.shields.io/badge/Python-3.10%2B-blue?logo=python&logoColor=white)](https://python.org)
[![Tool](https://img.shields.io/badge/Tool-GHunt%20v2.x-orange)](https://github.com/mxrch/GHunt)
[![Category](https://img.shields.io/badge/Category-OSINT-success)](https://github.com/rodrigo47363)
[![License](https://img.shields.io/badge/License-GPL%20v3-lightgrey)](LICENSE)

> **Parche crítico y hotfix para el parser `people.py` de GHunt, corrigiendo excepciones no controladas causadas por cambios recientes en el esquema de la Google People API y atributos corporativos de Google Workspace.**

---

## 📌 Contexto del Problema

En versiones de GHunt al auditar correos vinculados a cuentas corporativas o con restricciones de perfil, la API de Google People retorna atributos no definidos o estructuras vacías en `PersonGplusExtendedData`, desencadenando errores de tipo:
- `KeyError: 'contentRestriction'`
- Incompatibilidad en el cálculo heurístico del hash de imagen de perfil predeterminada (`is_default_profile_pic`).
- Fallos de serialización de atributos de usuario empresarial (`isEntrepriseUser`).

Este archivo `people.py` refactoriza el scraper interno asegurando validación defensiva de claves (`dict.get()`), tipado estricto con `typing`, y captura segura de excepciones.

---

## 🛠️ Cómo Aplicar el Parche en tu Instalación de GHunt

### Paso 1: Clonar el Repositorio
```bash
git clone https://github.com/rodrigo47363/ghunt-fix.git
cd ghunt-fix
```

### Paso 2: Identificar la Ruta de GHunt en tu Sistema
Ejecuta en tu terminal para obtener la ubicación exacta del paquete instalado en tu entorno o virtualenv:
```bash
python3 -c "import ghunt.objects.apis.people as p; print(p.__file__)"
```

### Paso 3: Reemplazar el Archivo Vulnerable
```bash
TARGET_PATH=$(python3 -c "import ghunt.objects.apis.people as p; print(p.__file__)")
sudo cp people.py "$TARGET_PATH"
```

### Paso 4: Verificar Ejecución de GHunt
```bash
ghunt email target@gmail.com
```

---

## ⚖️ Responsabilidad Ética
Este parche está destinado a investigadores de seguridad, analistas OSINT y profesionales de Red Team con autorización legal previa.
