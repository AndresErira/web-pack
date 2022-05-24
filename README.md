# WEBPACK
Nos permite preparar un proyecto para optimizar su rendimiento para produccion

Es conveniente tener una carpeta /src
y dentro el archivo de index.js sera el punto de inicio de
la aplicacion.

para instalarlo usamos: 

<span style="color:green">npm install webpack-cli -D</span> 

Para ejecutarlo como no lo instalamos de forma global usamos:

<span style="color:green">npx webpack</span>

automaticamente nos detectara el archivo de arranque y generara la carpeta dist
donde se alojara nuestro codigo optimizado por webpack.

Por defecto webpack usa el modo produccion (mode production) si no se lo especificamos.

para ejecutar el modo desarrollo usamos:

    npx webpack --mode development


## Como preparar el archivo de configuración

### En este archivo iran los loaders, los plugins y las extensiones

* Creamos el archivo  <span style="color:cyan">webpack.config.js</span>

        const path = require('path');
        module.exports = {
            entry: './src/index.js',
            output: {
                path: path.resolve(__dirname, 'dist'),
                filename: 'main.js'
            },
            resolve:{
                extensions: ['.js']
            }
        }

Importamos path con require nos permite usar resolve que ya viene incluido en todo el paquete de npm y nos permite resolver las rutas de los archivos el module.exports nos permite crear el objeto con la configuracion deseada entry determina nuestro punto de entrada de nuestra aplicacion desde donde se conecta nuestra aplicacion path en el ouput por estandar ponemos dist que crea el directorio de produccion o desarrollo.

* resolve es el objeto que nos permite manejar las extensiones con las que va a trabajar el proyecto

* ahora para ejecutar webpack lo hacemos de la siguiente forma

        webpack --mode production --config webpack.config.js

* para mejor practica creamos el script en package.json

        "build" : "webpack --mode production"

* al crear el script no es necesario agregar webpack.config.js ya que lo reconoce automaticamente, podemos cambiar build por el nombre que queramos y al ejecutarlo desde la consola usamos

        npm run build


<span style="color:green"></span>
