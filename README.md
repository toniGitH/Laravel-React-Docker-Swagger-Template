<h1 align="center"><strong>Plantilla Laravel + React en Docker</strong></h1>
<h2 align="center">Documentación con SwaggerUI</h2>

<details>
<summary style="cursor: pointer;" id="index">
    <h1>🔎 Índice de contenidos</h1>
  </summary>
  
<br>

🎯 [Descripción de la plantilla](#-descripción-de-la-plantilla)

🚀 [Tecnologías utilizadas](#-tecnologías-utilizadas)

📋 [Requisitos previos](#-requisitos-previos)

🔌 [Puertos del proyecto](#-puertos-del-proyecto)

📖 [Documentación API](#-documentación-api)

🧩 [Servicios principales (Docker)](#-servicios-principales-docker)

🐋 [Docker: instalación y requisitos previos](#-docker-instalación-y-requisitos-previos)

🐧 [Cómo levantar el proyecto en Linux](#-cómo-levantar-el-proyecto-en-linux)

🪟 [Cómo levantar el proyecto en Windows](#-cómo-levantar-el-proyecto-en-windows)

🍎 [Cómo levantar el proyecto en Mac](#-cómo-levantar-el-proyecto-en-mac)

🧪 [Testing](#-testing)

</details>

---

## 🎯 Descripción de la plantilla

Plantilla base para crear un proyecto con Laravel y React en un entorno Docker.

---

## 🚀 Tecnologías utilizadas

- Backend: **Laravel**
- Frontend: **React**
- Entorno de desarrollo: **Docker**
- Testing: **PHPUnit**
- Documentación API: **SwaggerUI**

🔝 [Volver al índice](#index)

---

## 📋 Requisitos previos

- Docker Engine/Daemon y Docker Compose Plugin (o Docker Desktop que los incluye)
- 4 GB de RAM disponible y ~2 GB de espacio en disco

🔝 [Volver al índice](#index)

---

## 🔌 Puertos del proyecto

##### 👉 Backend: Nginx + Laravel (public/) ➡️ [http://localhost:8988](http://localhost:8988)

##### 👉 Frontend: React (Vite dev server) ➡️ [http://localhost:8989](http://localhost:8989)

##### 👉 MySQL de desarrollo: host localhost puerto 3700 (3306 en contenedor)

##### 👉 MySQL de tests: host localhost puerto 3701 (3306 en contenedor)

###### 🔑 Credenciales base de datos por defecto (si usas .env.example) ➡️ usuario: *app* / pass: *app* / base: *app*

🔝 [Volver al índice](#index)

---

## 📖 Documentación API

La información sobre los endpoints de la API se genera con SwaggerUI.

##### 👉 SwaggerUI ➡️ [http://localhost:8081](http://localhost:8081) 

🔝 [Volver al índice](#index)

---

## 🧩 Servicios principales (Docker)

Este proyecto incluye un entorno Docker completo con **8 servicios**:

📌 **Nginx** – Servidor web que expone la aplicación **Laravel** al puerto **8988**. Recibe las peticiones HTTP y las pasa a PHP-FPM para procesar la lógica de Laravel.

📌 **PHP-FPM 8.2** – Motor PHP que ejecuta el código de Laravel dentro del contenedor PHP. No expone puertos, solo procesa peticiones enviadas por Nginx.  

📌 **Laravel** – Contenedor utilitario encargado de instalar dependencias, generar la clave de aplicación, ejecutar migraciones y procesar colas. No expone puertos.  

📌 **MySQL (desarrollo)** – Base de datos principal para la aplicación. Puerto interno **3306**, expuesto en el host como **3700**.

📌 **MySQL (tests)** – Base de datos separada para pruebas automáticas. Puerto interno **3306**, expuesto en el host como **3701**.

📌 **React (Vite)** – Interfaz frontend de la aplicación. Incluye su propio servidor de desarrollo y expone el puerto **8989**. No depende de Nginx. 

📌 **Swagger Builder (Redocly)** – Contenedor utilitario que compila la documentación OpenAPI a partir de los archivos fuente YAML en `docs/`. No expone puertos.  

📌 **Swagger UI** – Servidor web que sirve la documentación generada. Escucha en su propio puerto interno y lo mapea al host como 8081.

🔝 [Volver al índice](#index)

---

## 🐋 Docker: instalación y requisitos previos

Para ejecutar el proyecto necesitarás utilizar **Docker**.
  
A continuación se detallan las diferencias según tu sistema operativo.

### 🐧 Ubuntu/Debian (ejemplo para Ubuntu 22.04+)

##### 1) Desinstalar versiones antiguas (opcional)

🔹 Eimina instalaciones previas de Docker para evitar conflictos.

``` bash
sudo apt-get remove -y docker docker-engine docker.io containerd runc || true
```

##### 2) Preparar paquetes previos

🔹 Actualiza repositorios e instala utilidades necesarias para añadir repositorios seguros.

``` bash
sudo apt-get update
sudo apt-get install -y ca-certificates curl gnupg lsb-release
```

##### 3) Crear directorio de claves APT

🔹 Crea la carpeta recomendada por Debian/Ubuntu para almacenar claves GPG de  repositorios.

``` bash
sudo install -m 0755 -d /etc/apt/keyrings
```

##### 4) Descargar la clave GPG oficial de Docker

🔹 Permite verificar la autenticidad de los paquetes del repositorio de Docker.

``` bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg   | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```

##### 5) Registrar el repositorio oficial de Docker en APT

🔹 Añade la fuente oficial de Docker para instalar versiones actualizadas.

``` bash
echo   "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg]   https://download.docker.com/linux/ubuntu   $(. /etc/os-release && echo $UBUNTU_CODENAME) stable"   | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```
##### 6) Instalar Docker Engine + plugins

🔹 Instala el motor de Docker, CLI, containerd, Buildx y Compose plugin.

``` bash
sudo apt-get update
sudo apt-get install -y docker-ce docker-ce-cli containerd.io   docker-buildx-plugin docker-compose-plugin
```

##### 7) Recomendado: Usar Docker sin sudo

🔹 Permite ejecutar comandos Docker sin necesidad de sudo.

``` bash
sudo usermod -aG docker $USER
```

⚠️ Cierra sesión y vuelve a entrar para aplicar los cambios.


##### 8) Verificar instalación

🔹 Comprueba que Docker y Compose funcionan correctamente.

``` bash
docker --version
docker compose version
docker run --rm hello-world
```

🔝 [Volver al índice](#index)

### 🪟 Windows 10/11
##### 1) Asegurate de tener la virtualización activada en BIOS/UEFI.
##### 2) Instala Docker Desktop para Windows desde el sitio oficial.
##### 3) Habilita WSL 2 si Docker Desktop lo solicita.
##### 4) Reinicia y verifica:
🔹 Abre la consola (PowerShell, CMD o Ubuntu/WSL2 si la tienes) y ejecuta:

``` bash
docker --version
docker compose version
```

##### 5) Inicia la aplicación Docker Desktop y déjala corriendo en segundo plano (no la necesitas para nada más, aunque puedes utilizar sus funciones, que pueden ser interesantes)
##### 6) En la consola (Ubuntu/WSL2 si la tienes, o CMD o PowerShell) ya podrás ejecutar todos los comandos habituales de Docker.

🔝 [Volver al índice](#index)
<br>

### 🍎 macOS (Intel / Apple Silicon)

##### 1) Comprueba compatibilidad del procesador.
Docker Desktop funciona tanto en Apple Silicon (M1/M2/M3) como en Intel, pero usa tecnologías distintas internamente (HyperKit vs Apple Virtualization Framework).
No tienes que configurar nada, solo asegurarte de que tu versión de macOS es compatible (macOS 12+ normalmente).

##### 2) Instala Docker Desktop para macOS desde el sitio oficial.
Descarga la versión correspondiente a tu chip y arrastra el icono a *Aplicaciones*.

##### 3) Autoriza Docker Desktop si macOS te lo solicita.
macOS puede mostrar un aviso para permitir extensiones o controladores del sistema.
Ve a: *Preferencias del Sistema → Seguridad y privacidad* y permite las extensiones si aparece el aviso.

##### 4)  Inicia Docker Desktop y espera a que esté "*Running*".
Igual que en Windows: una vez está ejecutándose, ya no necesitas abrir la app salvo que quieras gestionar contenedores visualmente.

##### 5)  Verifica la instalación desde Terminal:

``` bash
docker --version
docker compose version
```

##### 6)  Usa Docker normalmente desde Terminal.
No hay diferencias relevantes frente a Linux/WSL: puedes ejecutar *docker*, *docker compose*, etc.

##### 7) Opcional: justa recursos asignados a Docker Desktop.

CPU, memoria RAM, disco usados para las máquinas virtuales.
Se controla desde: *Docker Desktop → Settings → Resources*

##### 8) Opcional: habilita Docker Buildx y otras extensiones.
Docker Desktop en macOS lo trae activado por defecto, pero puedes ajustarlo en:
*Settings → Features in development / Extensions*

🔝 [Volver al índice](#index)
<br>

---

## 🐧 Cómo levantar la plantilla/proyecto en Linux

>###### 🚨 IMPORTANTE:
>- En el archivo `docker-compose.yml`, sustituye "my_app" por el nombre de tu aplicación.
>- En el archivo `openapi.source.yml`, sustituye "my_app" por el nombre de tu aplicación.
>- En la ejecución de los comandos que verás en estas instrucciones, sustituye `my_app` por el nombre de tu aplicación.

>###### 🗒️ NOTA PREVIA SOBRE DOCKER EN LINUX:
>- Docker es nativo en Linux, por lo que no necesita Docker Desktop.
>- En Linux el Docker Engine se ejecuta directamente sobre el kernel, sin capas intermedias ni virtualización.
>- Por eso no necesita Docker Desktop, ya que el motor corre directamente en el sistema.
>- En Linux no se necesita WSL2, porque WSL2 es solo para Windows y Linux ya ejecuta contenedores de forma real y nativa.

>###### 💡 RECOMENDADO:
>- Permitir usar docker sin sudo: `sudo usermod -aG docker $USER` (Es a nivel global, para cualquier proyecto).

#### PASO A PASO DE INSTALACIÓN

##### 1. CLONAR REPOSITORIO:

En la terminal, ejecuta:

```
git clone https://github.com/toniGitH/Echo.git
```

O si prefieres crearlo en una carpeta con el nombre que tú prefieras, como *MiProyecto*:

```
git clone https://github.com/toniGitH/Echo.git MiProyecto
```

Si no lo puedes clonar, puedes hacer un Fork o, directamente, descargarlo.

##### 2. REASIGNAR LA PROPIEDAD DE LOS ARCHIVOS:

Nada más clonar el proyecto, sin levantar aún los contenedores:

```
cd /home/TU_USUARIO/Proyectos/CARPETA_RAÍZ_DE_TU_PROYECTO
sudo chown -R $USER:$USER ./laravel
```

Esto asegura que todos los archivos son tuyos, no del root del contenedor anterior.

Este paso SIEMPRE antes de levantar Docker por primera vez.

##### 3. CREAR ARCHIVO .ENV DE LA CARPETA LARAVEL

Dentro de la carpeta `laravel` del proyecto, crea un archivo `.env`:

```
cp laravel/.env.example laravel/.env
```

Asegúrate de que, al menos, exista esto en tu archivo `.env`:

```
APP_KEY=
APP_URL=http://localhost:8988
```

**NO ES NECESARIO** tener estas variables definidas en tu archivo `.env`:

```
APP_ENV: local
APP_DEBUG: true
DB_CONNECTION: mysql
DB_HOST: mysql
DB_PORT: 3306
DB_DATABASE: app
DB_USERNAME: app
DB_PASSWORD: app
```

De hecho, es totalmente inútil y nunca van a ser leídas, porque según la configuración actual del proyecto, sus valores son establecidos en el archivo `docker-compose.yml` y dicho archivo tiene prioridad sobre el archivo `.env`.

##### 4. LEVANTAR LA PILA (construye imágenes si es la primera vez)

Asegúrate de que tienes Docker en ejecución en tu sistema.

En una terminal, ejecuta:

```
docker compose up -d --build
```

##### 5. DAR PERMISOS A LAS CARPETAS QUE LARAVEL NECESITA ESCRIBIR:

Teclear, en la raíz del proyecto, y cuando estén levantados todos los contenedores, esto:

```
docker exec my_app-php sh -lc 'cd /var/www/html && chown -R www-data:www-data storage bootstrap/cache && chmod -R ug+rwX storage bootstrap/cache'
```

Este comando deja `storage/` y `bootstrap/cache/` listos para que Laravel pueda escribir desde el contenedor sin errores de permisos.

##### 6. OPCIONAL

Si en algún momento ves que un archivo vuelve a ser de root, ejecuta esto desde tu máquina, sin parar los contenedores:

```
sudo chown -R $USER:$USER ./laravel
```

Esto restablece los permisos de todo el proyecto por si algún comando dentro del contenedor (como `php artisan make:model`) creó archivos

🔝 [Volver al índice](#index)

---

## 🪟 Cómo levantar la plantilla/proyecto en Windows 10/11

>###### 🚨 IMPORTANTE:
>- En el archivo `docker-compose.yml`, sustituye "my_app" por el nombre de tu aplicación.
>- En el archivo `openapi.source.yml`, sustituye "my_app" por el nombre de tu aplicación.
>- En la ejecución de los comandos de estas instrucciones, sustituye `my_app` por el nombre de tu aplicación.

>###### 🗒️ NOTA PREVIA SOBRE DOCKER EN WINDOWS:
>- Windows no puede ejecutar Docker de forma nativa, por lo que Docker Desktop es obligatorio tenerlo instalado y en ejecución.
>- Docker Engine no puede ejecutarse directamente sobre Windows.
>- En Windows, Docker funciona gracias a WSL2, donde se ejecuta realmente el Docker Engine.
>- Docker Desktop crea un entorno Linux dentro de WSL2, y es ahí donde se ejecuta realmente Docker Engine.
>- Sin Docker Desktop + WSL2, ningún comando `docker` o `docker compose` funcionará.
>- Todos los comandos Docker funcionan mientras Docker Desktop esté activo.

>###### 🔒 AJUSTES DE PERMISOS:
>- En Windows NO existe un equivalente al comando `sudo usermod -aG docker $USER`.
>- Por tanto: no es necesario realizar ningún ajuste de permisos para usar docker sin sudo.

#### PASO A PASO DE INSTALACIÓN

##### 1. CLONAR REPOSITORIO

En PowerShell, CMD o Git Bash:
```
git clone https://github.com/toniGitH/Echo.git
```

O si prefieres crearlo en una carpeta con el nombre que tú prefieras, como *MiProyecto*:

```
git clone https://github.com/toniGitH/Echo.git MiProyecto
```

Si no puedes clonarlo, puedes hacer un Fork o descargar el ZIP del repositorio.

##### 2. REASIGNAR LA PROPIEDAD DE LOS ARCHIVOS

En Windows **NO es necesario este paso**.

El comando:

```
sudo chown -R $USER:$USER ./laravel
```
no existe en Windows y no es necesario, ya que Windows no gestiona permisos como Linux.

##### 3. CREAR ARCHIVO .ENV DE LA CARPETA LARAVEL

Dentro de la carpeta `laravel` del proyecto, crea un archivo `.env`:

```
cp laravel/.env.example laravel/.env
```

Asegúrate de que, al menos, exista esto en tu archivo `.env`:

```
APP_KEY=
APP_URL=http://localhost:8988
```

**NO ES NECESARIO** tener estas variables definidas en tu archivo `.env`:

```
APP_ENV: local
APP_DEBUG: true
DB_CONNECTION: mysql
DB_HOST: mysql
DB_PORT: 3306
DB_DATABASE: app
DB_USERNAME: app
DB_PASSWORD: app
```

De hecho, es totalmente inútil y nunca van a ser leídas, porque según la configuración actual del proyecto, sus valores son establecidos en el archivo `docker-compose.yml` y dicho archivo tiene prioridad sobre el archivo `.env`.

##### 4. LEVANTAR LA PILA (construye imágenes si es la primera vez)

Asegúrate de tener iniciada y en ejecución la aplicación Docker Desktop.

En PowerShell, Git Bash o CMD:

```
docker compose up -d --build
```

Docker Desktop gestionará las imágenes y contenedores.

##### 5. DAR PERMISOS A LAS CARPETAS QUE LARAVEL NECESITA

En Windows, aunque el sistema de archivos del host no usa permisos UNIX, dentro del contenedor sí es necesario ejecutar el mismo comando que en Linux:

```
docker exec my_app-php sh -lc 'cd /var/www/html && chown -R www-data:www-data storage bootstrap/cache && chmod -R ug+rwX storage bootstrap/cache'
```

Esto prepara `storage/` y `bootstrap/cache/` para que Laravel pueda escribir.

##### 6. OPCIONAL

En Windows este comando no existe y no debe ejecutarse:

```
sudo chown -R $USER:$USER ./laravel
```

Este paso se aplica únicamente en Linux y macOS.

🔝 [Volver al índice](#index)

---

## 🍎 Cómo levantar la plantilla/proyecto en Mac

>###### 🚨 IMPORTANTE:
>- En el archivo `docker-compose.yml`, sustituye "my_app" por el nombre de tu aplicación.
>- En el archivo `openapi.source.yml`, sustituye "my_app" por el nombre de tu aplicación.
>- En la ejecución de los comandos de estas instrucciones, sustituye `my_app` por el nombre de tu aplicación.

>###### 🗒️ NOTA PREVIA SOBRE DOCKER EN MAC:
>- macOS no puede ejecutar Docker de forma nativa, por lo que Docker Desktop es obligatorio tenerlo instalado y en ejecución.
>- Docker Engine no puede ejecutarse directamente sobre macOS.
>- Docker Desktop utiliza una máquina virtual interna (HyperKit / Apple HVF / Lima) donde se ejecuta Docker Engine.
>- Todos los comandos Docker funcionan mientras Docker Desktop esté activo.

>###### 🔒 AJUSTES DE PERMISOS:
>- No es necesario ningún "docker sin sudo", ya que macOS no necesita ese ajuste.
>- macOS funciona como Linux a nivel de permisos, por lo que `chown` SÍ es necesario.

---

#### PASO A PASO DE INSTALACIÓN

##### 1. CLONAR REPOSITORIO

En Terminal, ejecuta:

```
git clone https://github.com/toniGitH/Echo.git
```

O si prefieres crearlo en una carpeta con el nombre que tú prefieras, como *MiProyecto*:

```
git clone https://github.com/toniGitH/Echo.git MiProyecto
```

Si no lo puedes clonar, puedes hacer un Fork o, directamente, descargarlo.

##### 2. REASIGNAR LA PROPIEDAD DE LOS ARCHIVOS

Justo después de clonar, y antes de levantar contenedores:

```
cd /Users/TU_USUARIO/Proyectos/CARPETA_RAIZ_DE_TU_PROYECTO
sudo chown -R $USER:$USER ./laravel
```

Este paso sí es necesario, igual que en Linux, para evitar que archivos heredados del contenedor queden como root.

Este paso SIEMPRE antes de levantar Docker por primera vez.

##### 3. CREAR ARCHIVO .ENV DE LA CARPETA LARAVEL

Dentro de la carpeta `laravel` del proyecto, crea un archivo `.env`:

```
cp laravel/.env.example laravel/.env
```

Asegúrate de que, al menos, exista esto en tu archivo `.env`:

```
APP_KEY=
APP_URL=http://localhost:8988
```

**NO ES NECESARIO** tener estas variables definidas en tu archivo `.env`:

```
APP_ENV: local
APP_DEBUG: true
DB_CONNECTION: mysql
DB_HOST: mysql
DB_PORT: 3306
DB_DATABASE: app
DB_USERNAME: app
DB_PASSWORD: app
```

De hecho, es totalmente inútil y nunca van a ser leídas, porque según la configuración actual del proyecto, sus valores son establecidos en el archivo `docker-compose.yml` y dicho archivo tiene prioridad sobre el archivo `.env`.

##### 4. LEVANTAR LA PILA (construye imágenes si es la primera vez)

Asegúrate de tener iniciada y en ejecución la aplicación Docker Desktop.

En Terminal, ejecuta:

```
docker compose up -d --build
```

##### 5. DAR PERMISOS A LAS CARPETAS QUE LARAVEL NECESITA

Igual que Linux:

```
docker exec my_app-php sh -lc 'cd /var/www/html && chown -R www-data:www-data storage bootstrap/cache && chmod -R ug+rwX storage bootstrap/cache'
```

##### 6. OPCIONAL

Si alguna vez se generan archivos como root dentro del host:

```
sudo chown -R $USER:$USER ./laravel
```

Esto solo es necesario en macOS y Linux.

🔝 [Volver al índice](#index)

---

## 🧪 Testing

### Información previa

#### Cuando vayas a crear los tests, ten en cuenta la siguiente información.

> ##### 🐋 Contenedor de ejecución
> ✅ Ejecuta los tests desde el **contenedor de PHP** y no desde el contenedor de Laravel.
>
> ✅ El contenedor PHP es un contenedor "limpio" que no setea ninguna variable de entorno en el archivo `docker-compose.yml`, por lo que podrás establecer los valores deseados dentro del archivo `phpunit.xml`, y éstos serán los que se aplicarán realmente para el testing.
>
> ❎ El contenedor Laravel está seteando en el archivo `docker-compose.yml` determinadas variables como la base de datos, por lo que si ejecutas los tests desde este contenedor, esos valores tendrán preferencia sobre los que establezcas en el archivo `phpunit.xml` y éstos últimos nunca serán utilizados.

> ##### 💾 Base de datos de testing
> - El proyecto monta dos bases de datos independientes: una para **desarrollo** y otra para **tests**.
> - Puedes elegir, a la hora de lanzar los tests, qué base de datos utilizar: **SQLite** en memoria o **MySQL**
> - En el archivo `phpunit.xml` tienes las dos configuraciones a elegir para establecer si los tests se ejecutarán en una u otra base de datos.
> - Algunos métodos de tests se omiten automáticamente si la base de datos es SQLite, puesto que están pensados para una base de datos case-insensitive como MySQL. Es decir, se omiten porque en SQLite fallarían, pero en MySQL deben pasar correctamente.

### Cómo ejecutar los tests

#### 1) Elige el entorno de testing (SQLite o MySQL)

Abre el archivo `phpunit.xml` y:
- mantén descomentado el bloque que corresponda a la configuración que quieras usar
- comenta el bloque que corresponda a la otra configuración

#### 1) Levanta contenedores

```
docker compose up -d
```

#### 2) Entra dentro del contenedor PHP

```
docker compose exec php bash
```
#### 3) DENTRO del contenedor PHP, ejecuta los tests que necesites

Para ejecutar todos los tests:
```
php artisan test
```
Para ejecutar los tests unitarios:
```
php artisan test --testsuite=unit
```
Etc...


🔝 [Volver al índice](#index)

---

