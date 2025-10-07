# 🧠 Ejercicio Práctico: Git Avanzado con Ramas
## 🎯 Objetivo

### Practicar comandos avanzados de Git usando ramas de trabajo.
Aprender a:

- Guardar y restaurar cambios temporales.

- Reorganizar commits.

- Recuperar commits perdidos.

- Aplicar commits específicos de otras ramas.

- Detectar commits que introducen errores.

- Usar hooks de pre-commit para validación automática.

### 🚀 Paso 1: Preparar el entorno

#### 1-Crea una carpeta para el proyecto:
```sh
mkdir git-avanzado-ejercicio
cd git-avanzado-ejercicio
```

#### 2-Inicializa el repositorio:
```sh
git init
git add .
git commit -m "Agregar"
git branch -M main
git remote add origin git@github.com:kenkairon/CursoDeGithubAvanzado.git
git push -u origin main
```

#### 3-Crea un archivo inicial:
```sh
echo "# Proyecto Git Avanzado" > README.md
git add .
git commit -m "Primer commit: estructura base"
```
### 🌿 Paso 2: Crear y trabajar con ramas

### 1- Crea una nueva rama de desarrollo:
```sh
git checkout -b desarrollo
```

### 2- Crea un archivo de ejemplo:
```sh
echo "print('Versión inicial del script')" > script.py
git add script.py
git commit -m "Agregar script inicial"
```


```sh
echo "print('Nueva funcionalidad agregada')" >> script.py
git add script.py
git commit -m "Agregar nueva funcionalidad"
```

### 3 Realiza algunos cambios adicionales:
### 💾 Paso 3: Usar git stash
```sh
##Realiza un cambio sin confirmarlo:

echo "print('Cambio temporal')" >> script.py

##Guarda los cambios temporalmente:
git stash

###Verifica el estado:
git status

```
##Recupera los cambios cuando los necesites:

git stash pop

### 🧩 Paso 4: Usar git rebase -i
```sh
##Visualiza tus commits:

git log --oneline

##Ejecuta un rebase interactivo para reorganizar o unir commits:

git rebase -i HEAD~3

```
### 👉 En el editor que se abre puedes cambiar pick por:

- reword → modificar mensaje de commit

- squash → unir commits

- edit → modificar contenido del commit

- Guarda y sal del editor, sigue las instrucciones que Git te dé.

### 🧭 Paso 5: Usar git reflog
```sh
##Muestra todo el historial de movimientos (incluso los que “perdiste”):
git reflog

##Si perdiste un commit, puedes volver a él:

git checkout <id_del_commit>
```
### 🍒 Paso 6: Usar git cherry-pick

```sh
## Cambia a la rama principal:

git checkout main

##Selecciona un commit específico de otra rama:

git log desarrollo --oneline

##Copia el ID del commit que deseas traer y ejecútalo:

git cherry-pick <id_del_commit>
```
### 🕵️ Paso 7: Usar git bisect para encontrar errores

```sh
##Inicia el modo bisect:

git bisect start

##Marca la versión actual como “mala”:

git bisect bad

##Marca un commit anterior que sepas que funcionaba:

git bisect good <id_commit_bueno>


##Git te llevará a commits intermedios.
## En cada uno, prueba si el error sigue y marca como:

git bisect good

o

git bisect bad


## Cuando encuentre el commit problemático:

git bisect reset

```
### 🧩 Paso 8: Crear un pre-commit hook

#### Crea el archivo de hook:
```bash
nano .git/hooks/pre-commit
```

#### Agrega este contenido para evitar commits con la palabra “error”:
```bash
#!/bin/bash
if git diff --cached | grep -i "error" > /dev/null
then
    echo "🚫 No puedes hacer commit con la palabra 'error' en el código."
    exit 1
fi
```

#### Dale permisos de ejecución:
```bash
chmod +x .git/hooks/pre-commit
```

### Prueba hacer un commit con la palabra “error” en el código para verificar que el hook funcione.

#### ✅ Resultado esperado

- Al finalizar, habrás practicado:

- Guardar y recuperar cambios con stash.

- Reorganizar commits con rebase -i.

- Recuperar commits borrados con reflog.

- Aplicar commits específicos con cherry-pick.

- Detectar commits con errores usando bisect.

- Validar tus commits con un pre-commit hook personalizado.


