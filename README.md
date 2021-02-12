# Configurar un proyecto de React con Eslint, Prettier y Husky

Lo primero es instalar la extensiones de Eslint y Prettier en Visual Studio Code

Luego instalamos Eslint:

npm install eslint --save-dev

Luego vamos a iniciar la configuración con:

npx eslint --init

Nos pregunta:

How would you like to use ESLint? ...

Elegimos:

To check syntax, find problems, and enforce code style

Nos pregunta:

What type of modules does your project use? .

Elegimos:

JavaScript modules (import/export)

Nos pregunta:

Which framework does your project use? ...

Elegimos:

React

Nos pregunta:

Does your project use TypeScript?

Elegimos:

No

Nos pregunta:

Where does your code run?

Elegimos:

Browser

Nos pregunta:

How would you like to define a style for your project?

Elegimos:

Use a popular style guide

Nos pregunta:

Which style guide do you want to follow?

Elegimos:

Airbnb: https://github.com/airbnb/javascript

Nos pregunta:

What format do you want your config file to be in?

Elegimos:

JavaScript

Nos pregunta:

Would you like to install them now with npm?

Elgimos:

Yes

Luego en el archivo .eslintrc.js agregamos en rules las siguientes reglas:

rules: {
'import/prefer-default-export': 'off',
'react/jsx-filename-extension': 'off',
'react/prop-types': 'off',
'linebreak-style': 'off',
'react/react-in-jsx-scope': 'off',
'react/jsx-one-expression-per-line': 'off',
},

Luego instalamos:

npm install eslint-config-prettier -D

Agremos en .eslintrc.js al final del extends a 'prittier'

extends: ['plugin:react/recommended', 'airbnb', 'prettier'],

Esto es lo que hace es desactivar todas las reglas de Eslint que van a tener conflicto con Prettier.

Ahora vamos a instalar Prettier:

npm install prettier -D

Luego creamos el archivo de configuracion de Prettier en la raíz del proyecto:

.prettierrc.js

y escribimos el el archivo la configuración:

module.exports = {
trailingComma: 'es5',
singleQuote: true,
printWidth: 80,
tabWidth: 2,
useTabs: false,
endOfLine: 'lf',
}

Ahora para que todos lo integrantes del proyecto tengan la misma configuración el Visual Studio Code, hacemos lo siguiente:

Creamos la carpeta en la raíz del proyecto:

.vscode

y dentro creamos dos archivos, uno llamado settings.json con la siguiente configuración:

{
"editor.formatOnSave": false,
"editor.codeActionsOnSave": {
"source.fixAll.eslint": true
}
}

Y luego el otro archivo llamado extensions.json con la configuración:

{
"recommendations": [
"dbaeumer.vscode-eslint",
"esbenp.prettier-vscode"
]
}

Luego para prevenir subir código con errores a GitHub instalamos Husky, esto al momento de hacer un commit va a analizar el código con Eslint y con Prettier, en caso que encuentre algun error no nos va a dejar hacer el commit o push:

npm install husky --save-dev

y luego instalar:

npx mrm lint-staged
