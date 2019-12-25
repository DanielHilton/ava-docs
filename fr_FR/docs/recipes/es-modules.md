___
**Note du traducteur**

C'est la traduction du fichier [es-modules.md](https://github.com/avajs/ava/blob/master/docs/recipes/es-modules.md). Voici un [lien](https://github.com/avajs/ava/compare/b4ea43529a6d058a96055735cfa6e7056c009112...master#diff-1da5d6bfe1c97b416498e18caafe90fc) vers les différences avec le master de AVA (Si en cliquant sur le lien, vous ne trouvez pas le fichier `es-modules.md` parmi les fichiers modifiés, vous pouvez donc en déduire que la traduction est à jour).
___
# Utilisation des ES modules dans AVA

Traductions : [English](https://github.com/avajs/ava/blob/master/docs/recipes/es-modules.md)

À partir de Node.js 8.5.0, les [ES modules](http://2ality.com/2017/09/native-esm-node.html) sont nativement pris en charge, mais en utilisant le flag de la ligne de commande `--experimental-modules`. Ça marche en utilisant l'extension de fichier `.mjs`. AVA ne prend actuellement pas en charge l'option de ligne de commande ou la nouvelle extension de fichier, mais vous *pouvez* utiliser le module [`esm`](https://github.com/standard-things/esm) pour utiliser la nouvelle syntaxe.

Voici comment vous devez travailler avec AVA.

D'abord, installez [`esm`](https://github.com/standard-things/esm):

```
$ npm install esm
```

Configurez-le dans votre fichier `package.json` ou `ava.config.js` et ajoutez-le à l'option `"require"` de AVA. Assurez-vous de l'ajouter en tant que premier élément.

**`package.json` :**

```json
{
	"ava": {
		"require": [
			"esm"
		]
	}
}
```

Vous pouvez maintenant utiliser les modules ES natifs avec AVA :

```js
// sum.mjs
export default function sum(a, b) {
	return a + b;
};
```

```js
// test.js
import test from 'ava';
import sum from './sum.mjs';

test('2 + 2 = 4', t => {
	t.is(sum(2, 2), 4);
});
```

Vous devez configurer AVA pour reconnaître les extensions `.mjs` :

**`package.json`:**

```json
{
	"ava": {
		"extensions": [
			"js",
			"mjs"
		]
	}
}
```
