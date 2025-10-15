## Hola a todos 👋
¡¡Descargar VSCode!! -> https://code.visualstudio.com/download

Extensiones:
   + Git Graph
   + GitLens
   + Jupiter
   + Python

# 📚 Organización de Repositorios

Este documento explica **cómo organizamos el código en esta organización**.  
Queremos que todo sea **simple, claro y fácil de usar**, incluso si es la primera vez que trabajas con GitHub.

📌 **Objetivo**: que todos podamos trabajar sin miedo a “romper nada” y que sea fácil pasar de investigación a producto.

## 🧩 Reglas comunes a todos los repos

- **No subir datos pesados** (guardar fuera de GitHub).  
- **README obligatorio** en cada repo: explica qué es, cómo ejecutar y cómo desplegar.  
- **Simplicidad ante todo**: mejor algo sencillo que nadie tenga miedo de usar.
- **Código Limpio**: Modularizado y legible.
---

## 🔬 Repositorios de Investigación

**Un repositorio por línea de investigación**.
- **Convención:** research-[nombrelinea]-[nombresublinea(opcional)]
  
  - Ejemplo: `research-qml`

Dentro de cada repo habrá **subcarpetas por sublínea** hasta que la sublinea sea autosuficiente:

>```
> research-qml/
> ├─ qlstm/
> ├─ anomaly/
> └─ qnlp/
>```

**Cada carpeta de sublinea**, con este formato:

>```
> research-qml/qlstm/
> ├─ onboarding/
> ├─ core/
> ├─ experimentos/
> └─ ...
>```

**La carpeta de onboarding**, recogera nociones básicas:

>```
> onboarding/ejemplos_básicos
> ├─ README.md # info
> ├─ notebook.ipynb 
> ├─ scripts.py 
> └─ ...
>```

**La carpeta core**, recogera las funcionalidades generalistas (abstracciones):

>```
> core/qlstm
> ├─ README.md # info
> ├─ notebook.ipynb 
> ├─ scripts.py 
> └─ ...
>```

**La carpeta de experimentos**, recoge ideas:

>```
> experimentos/YYYY-MM-DD-titulo-corto-nombre/
> ├─ README.md # explica qué haces
> ├─ notebook.ipynb # tu notebook principal
> ├─ scripts.py # tu notebook principal
> └─ ...
>```


### Reglas básicas de investigación
1. Cada persona trabaja en su propia carpeta en experimentos, sin tocar las de los demás.  
2. Todo va en la rama `main` (no usamos ramas al principio).  
3. No se suben datasets pesados; enlaza la fuente o usa un `.gitignore`.  
4. Cada experimento debe tener un `README.md` con (personalizable):
 - Objetivo  
 - Dataset usado  
 - Resultados  
 - Próximos pasos  

---

## 🚀 Repositorios de Proyectos (con despliegue en Azure)

- **Un repositorio por producto**.  
Dentro estarán el **frontend**, el **backend** y la **infraestructura**:

> ```
> app-miProducto/
> ├─ frontend/ # aplicación web
> ├─ backend/ # API
> ├─ infra/ # scripts de despliegue (Azure)
> └─ .github/workflows/ # automatización de CI/CD
> ```

### Tecnologías que usaremos en Azure
- **Frontend** → Azure Static Web Apps  
- **Backend** → Azure Container Apps  
- **Contenedores** → Azure Container Registry  

### Flujo de despliegue
- Al hacer **push a `main`** → despliegue automático en **DEV**  
- Al crear un **release con tag `v*`** → despliegue automático en **PROD**  

---

## 📝 Convenciones de commits

Los mensajes de commit deben ser **claros y breves**.  
Usamos un **prefijo** para indicar el tipo de cambio:

- `add:` → algo nuevo (archivos, features, experimentos)  
- `update:` → mejoras o cambios en algo existente  
- `fix:` → corrección de error  
- `docs:` → documentación, README, comentarios  
- `test:` → tests unitarios o de integración  
- `chore:` → mantenimiento (dependencias, configs, .gitignore…)
- `exp:` → aportaciones a experimentos.


### Ejemplos

- `add: baseline QLSTM experiment`  
- `fix: typo in anomaly detection script`  
- `docs: update project README with setup steps`  
- `update: improve backend API error handling`  
- `chore: add Python 3.11 to CI matrix`  
- `exp: QNLP intent classification run (2025-10-03)`  

### ✨ Tips

- **Un commit = un cambio lógico.**  
  Ejemplo: si arreglas un bug y además actualizas el README, mejor haz dos commits.  
- **Primera línea corta** (~50 caracteres máximo).  
- Puedes añadir más detalle después:  

> fix: handle empty dataset case in QLSTM
>
> Added a condition to avoid crash when dataset is empty.
  

## 🧬 Conda: Entorno virtual

Usaremos **Conda** para crear y gestionar los entornos virtuales, ya que librerías científicas como **NumPy**, **SciPy** o **PyTorch** utilizan código compilado en **C, C++ o Fortran** para maximizar la velocidad de ejecución. Conda gestiona este tipo de dependencias de forma más eficiente y estable que `pip`, especialmente en Windows y en entornos de investigación.

Concretamente, Conda maneja dos capas clave:

- **🔹 Librerías del sistema:** Son componentes *no escritos en Python* que las librerías científicas utilizan internamente para realizar operaciones de bajo nivel (álgebra lineal, gestión de memoria, uso de GPU, comunicación con el sistema operativo…). Ejemplos: `BLAS`, `LAPACK`, `MKL`, `OpenBLAS`, `OpenSSL`, `CUDA`, `zlib`. Conda instala versiones precompiladas y compatibles entre sí, evitando conflictos entre dependencias.

- **🔹 Dependencias del sistema:** Son los *requisitos técnicos* necesarios para compilar o ejecutar esas librerías del sistema, como compiladores, toolchains, cabeceras (`headers`) o bibliotecas dinámicas (`.dll`, `.so`, `.dylib`). Conda se encarga de resolverlas automáticamente — sin necesidad de instalar manualmente **Visual Studio Build Tools**, **CUDA Toolkit**, o similares.

Al instalar **Miniconda**, se incluye su propio **Python interno**, independiente del Python que pueda existir en el sistema. Este Python se encuentra en `C:\Users\<usuario>\miniconda3\python.exe` y es completamente funcional por sí mismo, incluso si no tienes ningún Python global instalado (por ejemplo, el de [python.org](https://www.python.org) o el de Microsoft Store). Por eso, durante la instalación de Miniconda se recomienda marcar las siguientes opciones:

- ✅ **Add Miniconda3 to my PATH environment variable:** permite ejecutar `conda` y `python` directamente desde PowerShell sin rutas completas.
- ✅ **Register Miniconda3 as the system Python 3.11:** asocia los archivos `.py` a este Python y lo registra como intérprete por defecto.

Esto **no sustituye** al Python global del sistema, simplemente lo añade al PATH y lo registra como intérprete predeterminado. Si no existe un Python global, Conda lo cubre completamente: su Python “base” actúa como Python del sistema.

Cada entorno Conda contiene su **propio ejecutable de Python**, totalmente independiente del resto. Por ejemplo, `C:\Users\<usuario>\miniconda3\envs\<nombre_entorno>\python.exe`. Cuando en el archivo `environment.yml` se especifica una versión concreta, por ejemplo `python=3.11`, Conda crea un entorno con esa versión exacta de Python. Si ya dispone del binario 3.11 en caché, lo reutiliza; si no, descarga el binario precompilado correspondiente para tu sistema operativo y arquitectura.

De este modo, puedes tener varios entornos con versiones diferentes de Python coexistiendo sin conflictos, como por ejemplo: `(base) → Python 3.11`, `(circuitos_cuanticos) → Python 3.10`, `(algoritmos_variacionales) → Python 3.12`, cada uno completamente aislado y con sus dependencias específicas.

### 🧭 Pasos a seguir para crear un entorno Conda

1. **Descargar e instalar Miniconda (solo la primera vez):**  
   Miniconda es una versión ligera de Anaconda que incluye Conda y un Python interno, sin librerías adicionales.  
   Descarga la versión de Windows desde el siguiente enlace oficial:  
   👉 [https://docs.conda.io/en/latest/miniconda.html](https://docs.conda.io/en/latest/miniconda.html)

   Durante la instalación, marca las dos opciones recomendadas:
   - ✅ **Add Miniconda3 to my PATH environment variable** → permite usar `conda` y `python` desde PowerShell sin rutas absolutas.
   - ✅ **Register Miniconda3 as the system Python 3.11** → asocia los archivos `.py` a este Python y lo registra como intérprete por defecto.

2. **Quitar politicas de seguridad de PowerShell para ejecutar scripts (solo la primera vez):**
   ```powershell
   Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned

3. **Verificar que conda esta instalado correctamente**
```
   conda --version
```

4. **Revisar o definir el archivo `environment.yml`:**  
   Este archivo describe las dependencias del entorno.  
   Ejemplo:
   ```yaml
   name: circuitos_cuanticos
   channels:
     - conda-forge
   dependencies:
     - python=3.11
     - numpy
     - scipy
     - matplotlib
     - pytorch
     - qiskit
     - ipykernel
     - pip
     - pip:
         - pyqubo==1.4.0
> Si existe un **environment_base.yml** con dependencias comunes, usa las mismas versiones para mantener coherencia entre sublíneas.

**Channels:** Repositorios de paquetes desde donde Conda descarga las librerías que instalas. Conda busca en uno o varios canales (repositorios) dónde está el paquete y descarga una versión compatible con tu sistema operativo y tu versión de Python.
> 
5. **Crear entorno desde conda (solo la primera vez)**
```
conda env create -f environment.yml
```
Conda descargará todas las librerías de Python y del sistema necesarias, generando un entorno aislado en:
> C:\Users\<usuario>\miniconda3\envs\<nombre_entorno>

6. **Activar el entorno**
```
conda activate <nombre_entorno>
```
El prompt cambiará para reflejar el entorno activo:
> (nombre_entorno) PS C:\Users\<usuario>\Documents\research\<nombre_entorno>

7. **Registrar el entorno para usarlo en Jupyter**
```
python -m ipykernel install --user --name <nombre_entorno> --display-name "Python (nombre_entorno)"
```
8. **Uso diario**
```
conda activate circuitos_cuanticos
```
9. **Para integrar cambios de dependencias**
```
conda env update -f environment.yml --prune
```
10. **Eliminar o recrear entorno**
```
conda deactivate
conda env remove -n circuitos_cuanticos
conda env create -f environment.yml
```
11. **Verificar entornos disponibles**
```
conda env list
conda list <nombre_libreria> -> paquete(s) instalados desde conda
```













