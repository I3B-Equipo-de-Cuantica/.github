## Hola a todos 👋

# 📚 Organización de Repositorios

Este documento explica **cómo organizamos el código en esta organización**.  
Queremos que todo sea **simple, claro y fácil de usar**, incluso si es la primera vez que trabajas con GitHub.

📌 **Objetivo**: que todos podamos trabajar sin miedo a “romper nada” y que sea fácil pasar de investigación a producto.

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

## 🧩 Reglas comunes a todos los repos

- **Commits claros**: usa mensajes como `add:`, `fix:`, `update:`.  
- **No subir datos pesados** (guardar fuera de GitHub).  
- **README obligatorio** en cada repo: explica qué es, cómo ejecutar y cómo desplegar.  
- **Simplicidad ante todo**: mejor algo sencillo que nadie tenga miedo de usar.
- **Código Limpio**: Modularizado y legible.



