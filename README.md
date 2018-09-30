# Fizz Docdash
[![npm version](https://badge.fury.io/js/docdash.svg)](https://badge.fury.io/js/docdash) [![license](https://img.shields.io/npm/l/docdash.svg)](LICENSE.md)

Template para [JSDoc 3](http://usejsdoc.org/) basado en [Docdash](http://clenemt.github.io/docdash/) para [Fizzmod](http://new.fizzmod.com/)

## Instalación

```bash
$ npm install jsdoc fizz-docdash
```

## Uso

#### jsdoc.conf.json
Crear y configurar `jsdoc.conf.json` en base al siguiente ejemplo

```json
{
	"plugins": [ "plugins/markdown.js" ],// pluging utilizado para renderizar README.md
	"markdown": {
		"idInHeadings": true // Genera anclas en los titulos para luego referenciar en un indice
	},
	"recurseDepth": 50,
	"source": {
		"include": [
			"./src/js/global.js", // agregar todos los archivos *.js que tengan comentarios jsdoc
			"./README.md" // Solo se puede agregar un archivo *.md
		],
		"includePattern": ".+\\.js(doc|x)?$",
		"excludePattern": "((^|\\/|\\\\)_|node_modules)"
	},
	"sourceType": "module",
	"tags": {
		"allowUnknownTags": true,
		"dictionaries": [
			"jsdoc",
			"closure"
		]
	},
	"templates": {
		"cleverLinks": false,
		"monospaceLinks": false
	},
	"opts": {
		"template": "node_modules/fizz-docdash", // Template utilizado. Ver package.json
		"private": false // mostra/ocultar las funciones privadas documentadas
	}
}
```

#### package.json
Configurar scripts de `package.json` con la linea correspondiente a jsdoc.

```json
{
	"scripts": {
		"jsdoc": "jsdoc -c ./jsdoc.conf.json -r && google-chrome ./out/index.html"
	}
}
```

#### .gitignore
Editar `.gitignore` para no subi la carpeta `/out` generada por `jsdoc` en cada render.

#### bash

```bash
$ npm run jsdoc
```

## Opciones
Docdash soporta las siguientes opciones:

```
{
	"docdash": {
		"static": [false|true],         // Display the static members inside the navbar
		"sort": [false|true],           // Sort the methods in the navbar
		"sectionOrder": [        // Order the main section in the navbar (default order shown here)
			 "Classes",
			 "Modules",
			 "Externals",
			 "Events",
			 "Namespaces",
			 "Mixins",
			 "Tutorials",
			 "Interfaces"
		]
		"disqus": "",                   // Shortname for your disqus (subdomain during site creation)
		"openGraph": {                  // Open Graph options (mostly for Facebook and other sites to easily extract meta information)
			"title": "",                // Title of the website
			"type": "website",          // Type of the website
			"image": "",                // Main image/logo
			"site_name": "",            // Site name
			"url": ""                   // Main canonical URL for the main page of the site
		},
		"meta": {                       // Meta information options (mostly for search engines that have not indexed your site yet)
			"title": "",                // Also will be used as postfix to actualy page title, prefixed with object/document name
			"description": "",          // Description of overal contents of your website
			"keyword": ""               // Keywords for search engines
		},
		"search": [false|true],         // Display seach box above navigation which allows to search/filter navigation items
		"collapse": [false|true],       // Collapse navigation by default except current object's navigation of the current page
		"typedefs": [false|true],       // Include typedefs in menu
		"removeQuotes": [none|all|trim],// Remove single and double quotes, trim removes only surrounding ones
		"scripts": []                   // Array of external (or relative local copied using templates.default.staticFiles.include) scripts to inject into HTML,
		"menu":{                        // Adding additional menu items after Home
			"Project Website":{         // Menu item name
				"href":"https://myproject.com", //the rest of HTML properties to add to manu item
				"target":"_blank",
				"class":"menu-item",
				"id":"website_link"
			},
			"Forum":{
				"href":"https://myproject.com.forum",
				"target":"_blank",
				"class":"menu-item",
				"id":"forum_link"
			}
		}
	}
}
```