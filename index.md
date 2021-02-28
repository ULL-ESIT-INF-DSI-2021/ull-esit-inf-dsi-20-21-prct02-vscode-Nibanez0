# Informe práctica 2: Instalación y configuración de Visual Studio Code

```
Noelia Ibáñez Silvestre
Práctica 2- Desarrollo de Sistemas Informáticos
Universidad de La Laguna
```

## Objetivo
Esta práctica consiste, principalmente, en la instalación y configuración del entorno de desarrollo Visual Studio Code. Además, se creará el primer proyecto en TypeScript.

## Pasos previos
1. Aceptar la asignación de GitHub Classroom asociada a esta práctica y proporcionada por el profesor.

2. Conectarse a la VPN de la ULL.

## Instalación y funcionalidad de Visual Studio Code
En mi caso, ya tenía instalado Visual Studio Code (VSCode). Para ello utilicé:

```bash
noelia@noelia-IdeaPad-Gaming-3-15IMH05:~$ sudo apt install code
```
También  se pueden seguir las instrucciones proporcionadas por [VSCode](https://code.visualstudio.com/docs/setup/setup-overview).


## Configuración de Visual Studio Code para conectarse a una máquina remota por SSH

Para este paso, lo primero que hice fue instalar **Remote-SSH** y configurar la conexión. Para ello, utilicé la paleta de comandos (F1) y busqué **Remote-SSH: Connect to Host...**. Una vez instalada la extensión, configuré la conexión del host. Para ello, pulsé sobre F1, abrí **Remote-SSH: Connect to Host...** y pulsé sobre **Configure SSH Host...**, elegí **~/.ssh/config** y modifiqué el archivo poniendo los nombres adecuados como se muestra:

```
Host iaas-dsi2
    HostName iaas-dsi2
    User usuario
```

Una vez configurada la conexión, me conecté pulsando sobre el nombre de la máquina (**iaas-dsi2**) en **Connect to Host...** y comprobé la conexión en la máquina virtual con:

```
[~()]$hostname
iaas-dsi2
```

## Sesiones colaborativas con Visual Studio Live Share

Para poder utilizar Visual Studio Share, lo que hice fue instalar la extensión **Live Share Extension Pack** en la máquina virtual y local.
Además, instalé todas las extensiones recomendadas que aparecen al final de la página web [Live Share Extension Pack](https://marketplace.visualstudio.com/items?itemName=MS-vsliveshare.vsliveshare-pack).

## Primer proyecto en TypeScript: "Hola Mundo"

En primer lugar, instalé ESLint que permite comprobar el estilo sobre ficheros que incluyan código en JavaScript y TypeScript.

Seguidamente, instalé el compilador de TypeScript. Para ello, utilicé npm con --global, esta opción me permite instalar el paquete de manera global.

```bash
[~()]$npm install --global typescript
...
added 1 package, and audited 2 packages in 2s

found 0 vulnerabilities
[~()]$tsc --version
Version 4.1.3
```

A continuación, ejecuté los siguientes comandos desde una terminal de VSCode de la máquina virtual.

```bash
[~()]$pwd
/home/usuario
[~()]$mkdir hello-world
[~()]$cd hello-world/
[~/hello-world()]$npm init --yes
```

El comando **npm init --yes** permite crear un fichero denominado **package.json**, el cual se utiliza, entre otras cosas, para establecer las dependenciasde desarrollo y ejecución.

```bash
Wrote to /home/usuario/hello-world/package.json:

{
  "name": "hello-world",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC"
}
```

A continuación, abrí el directorio **~/hello-world** en el explorador de VSCode. Para ello, elegí la opción **Open Folder** en el menú **File** y seleccioné **hello-world**.

Una vez añadido el directorio al espacio de trabajo, creé un nuevo fichero selecionando **New File** dentro del directorio, denominado **tsconfig.json** e incluí las siguientes líneas:

```bash
{
  "compilerOptions": {
    "target": "ES2018",
    "outDir": "./dist",
    "rootDir": "./src",
    "module": "CommonJS"
  }
}
```

Estas opciones de configuración le indican al configurador de TypeScript que, en primer lugar, quiero generar código compatible con uno de los últimos estándares de JavaScript. En segundo lugar, que el código JavaScript producto de la compilación se almacenará en un directorio **dist**. En tercer lugar, especifico que el código fuente escrito en TypeScript se encuentra en el directorio **src**. Por último, indico un estándar para cargar código desde ficheros independientes.

Después, añadí un fichero con código TypeScript:

```bash
[~/hello-world()]$pwd
/home/usuario/hello-world
[~/hello-world()]$mkdir src
[~/hello-world()]$cd src
[~/hello-world/src()]$touch index.ts
```

Y añadí en **index.ts**:

```bash
let myString: string = "Hola Mundo";
console.log(myString);
```

Seguidamente, compilé el código desde VSCode ejecutando:

```bash
[~/hello-world()]$tsc
```

Lo anterior queda guardado en el directorio **dist** y el fichero **index.js** en su interior. A continuación, comprobé si existe alguna diferencia entre **./src/index.ts** y **./dist/index.js** y se puede observar que la principal diferencia es la declaración de **myString**:

```bash
[~/hello-world()]$diff src/index.ts dist/index.js 
1c1
< let myString: string = "Hola Mundo";
---
> let myString = "Hola Mundo";
```

Por último, ejecuté el código JavaScript generado a partir del código TypeScript:

```bash
[~/hello-world()]$node dist/index.js
Hola Mundo
```

## Conclusión

Una vez finalizados todos los pasos anteriores y sin ninguna dificultad, conseguí intalar y configurar Visual Studio Code junto a Visual Studio Live Share. Además de crear el primer proyecto en TypeScript.