# Integrantes
Jackson Leonardo Rivera Usuga 1000567660
Leonardo Araque Quintero 1152217428

# Reto 0 - Bash básico

Este README documenta el paso a paso realizado en el laboratorio 0, comprendiendo los ejercicios de comandos basicos en bash y también la parte de Git para subir el trabajo desde consola.

El trabajo se realizó en **Kali Linux** dentro de **VirtualBox**.


## shortcuts usados en la terminal

* `TAB` lo utilizamos mucho para autocompletar comandos
*  Teclas `Up` / `Down` para navegar por el historial de comandos
* `Ctrl + L` para limpiar pantalla, especialmente al tener varios errores seguidos
*  Tecla `Home` ir al inicio de la línea
* `!!` Aunque es mas facil precionar las flechitas, lo utilizamos un par de veces

---

# Desarrollo del laboratorio (Pasos 3 al 10)

## 3) Crear el directorio `lab0`

Se creó la carpeta del laboratorio dentro de la ruta solicitada para el lab0

```bash
mkdir -p ~/operating-systems-20261/laboratories/lab0
```


## 4) Entrar al directorio `lab0`

Ingresamos a la carpeta

```bash
cd ~/operating-systems-20261/laboratories/lab0
```

Validamos sí se entró a la ruta correcta

```bash
pwd
```


## 5) Imprimir la ruta absoluta y guardarla en el archivo `path.txt`

Primero imprimimos y comprobamos la ruta actual

```bash
pwd
```

Luego se guardó esa salida en `path.txt`

```bash
pwd > path.txt
```

Verificamos el contenido de `path.txt`

Este verificacion nos sirvio bastante ya que inicialmente creamos el archivo mal, lo llamamos `path.text` por error al escribir. Asi que tuvimos que realizar este paso nuevamente con la extension .txt

```bash
cat path.txt
```


## 6) Crear los directorios `example`, `music`, `photos`, `projects`

Se crearon los 4 directorios con un solo comando

```bash
mkdir example music photos projects
```

## 7) Crear 100 archivos en cada directorio

Se crearon archivos vacíos del `file1` al `file100` dentro de cada carpeta utilizando `touch` y brace expansion

```bash
touch example/file{1..100} music/file{1..100} photos/file{1..100} projects/file{1..100}
```

Para comprobar 

```bash
ls example
```

## 8) Borrar los primeros 10 y los últimos 20 archivos en cada directorio

Se eliminaron todos los archivos file1 hasta file 10 y file81 hasta file100
Utilizamos cuatro comandos. Nos apoyamos del shortcut `!!` para variar de la flecha up del teclado

```bash
rm example/file{1..10} example/file{81..100}
rm music/file{1..10} music/file{81..100}
rm photos/file{1..10} photos/file{81..100}
rm projects/file{1..10} projects/file{81..100}
```

## 9) Mover `example`, `music` y `photos` dentro de `projects`

Se movieron las tres carpetas dentro de `projects`

```bash
mv example music photos projects/
```

## 10) Eliminar archivos de `projects` en modo verbose y guardar salida en `output.txt`

Eliminamos solo los archivos que estaban directamente dentro de `projects` sin borrar las carpetas movidas, usando modo verboso:

```bash
rm -v projects/file* > output.txt
```

# Subida a GitHub desde consola

## 13) Ir a la raíz del proyecto

Para trabajar con Git primero nos posicionamos en la carpeta raiz

```bash
cd ~/operating-systems-20261
```

## Verificar config de git

Primero verificamos si git existe en la maquina virtual en la que estamos trabajando

```bash
git --version
```

Tambien configuramos el usuario de git con nuestras credenciales

```bash
git config --global user.name "JacksonRivera"
git config --global user.email "email@gmail.com"
```

## Inicializar git y commitear cambios

Como no tenemos el repo aun inicializado en la carpeta corremos

```bash
git init
git branch -M main
```
Este comando lo utilizamos varias veces durante el proceso para verificar archivos con cambios y el estado de la rama

```bash
git status
```
Pasamos a staged los cambios y commiteamos

```bash
git add .
git commit -m "laboratory files and folders"
```

## Intento de push y problema de autenticación

Se intentó subir con un push

```bash
git push -u origin main
```

Inicialmente salió error porque al momento de autenticar la cuenta de GitHub, lo intentamos con la contraseña normal. Git no permite pasar contraseñas por peticiones HTTP.
Entonces creamos un token ssh desde nuestro perfil de git para autenticarnos correctamente desde bash y pudimos correr el comando anterior


## Problema de conflictos

Nos salio un error por divergencia en las ramas. Esto debido a que no habiamos hecho git pull y en el repo ya teniamos creado un README, el cual generaba un conflicto
Luego, al hacer `pull`, Git indicó que había divergencia entre la rama local y la remota.

El comando que se usó para resolverlo fue:

```bash
git pull --no-rebase origin main --allow-unrelated-histories
```

`--allow-unrelated-histories` permite unir historiales distintos ya que local y remoto no tenían el mismo commit inicial


## Push final al repositorio

Después de resolver el conflicto de historiales, se ejecutó nuevamente

```bash
git push origin main
```

Con esto se subieron los cambios al repositorio remoto.

