# [WEBPACK](https://ferroelectricosla29sm.com) &middot; [![license](./src/assets/images/licence.svg)](link) [![npm version](./src/assets/images/npmversion.svg)](link) 


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
```js
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
```
Importamos path con require nos permite usar resolve que ya viene incluido en todo el paquete de npm y nos permite resolver las rutas de los archivos el module.exports nos permite crear el objeto con la configuracion deseada entry determina nuestro punto de entrada de nuestra aplicacion desde donde se conecta nuestra aplicacion path en el ouput por estandar ponemos dist que crea el directorio de produccion o desarrollo.

* resolve es el objeto que nos permite manejar las extensiones con las que va a trabajar el proyecto

* ahora para ejecutar webpack lo hacemos de la siguiente forma

     ```s  
     webpack --mode production --config webpack.config.js
     ```

* para mejor practica creamos el script en package.json

        "build" : "webpack --mode production"

* al crear el script no es necesario agregar webpack.config.js ya que lo reconoce automaticamente, podemos cambiar build por el nombre que queramos y al ejecutarlo desde la consola usamos

        npm run build

# [babel loader](link)

Permite preparar el codigo js para que sea compatible con todos los navegadores

para instalar babel usamos
```s
        npm install babel-loader -D
```
loader de babel
```s
        npm install @babel/core -D
```
nucleo del recurso
```s
        npm install @babel/preset-env -D
```
permite trabajar con javascript moderno
```s
        npm install @babel/plugin-transform-runtime -D
```
Plugin que nos permite trabajar con asincronismo en caso de usar peticiones.


o tambien en una linea

```s
        npm install babel-loader @babel/core @babel/preset-env @babel/plugin-transform-runtime -D
```

* Se crea el archivo .babelrc el cual contendra las configuraciones de babel y contendrá un objeto.

```js
    {
        "presets":[
            "@babel/preset-env"
        ],
        "plugins":[
            "@babel/plugin-transform-runtime"
        ]
    }
```
Se configuró el preset para  javascript moderno y su respectivo plugin

* Ahora debemos tambien modificar webpack.config.js
* Se agrega el objeto module que contiene las reglas para usar babel, test contiene una expresión regular que declara las extensiones con las que se va a trabajar y exclude nos excluye la carpeta node_modules para que no se rompa el codigo.

```js
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

//NUEVA LINEA
,
            module:{
                rules:[
                    {
                        test: /\.m?js$/,
                        exclude: /node_modules/,
                        use:{
                            loader: 'babel-loader'
                        }
                    }
                ]
            }

 //NUEVA LINEA           

        }
```

<span style="color:green"></span>
