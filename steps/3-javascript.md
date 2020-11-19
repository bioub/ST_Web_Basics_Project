# Etape 3 - Javascript

Créer un nouveau dossier `spa` et y recopier les dossiers `css` et `img`

Ajouter un dossier `js` avec 7 fichiers :

* `about.js`
* `home.js`
* `product-details.js`
* `products.js`
* `search.js`
* `not-found.js`
* `router.js`

## HTML

Créer un fichier index.html qui reprend la balise `header` avec les liens et la balise `main` vide.

Insérer tous les fichiers CSS dans la balise `head` dans cette ordre :

* `common.css`
* `search.css`
* `products.css`
* `product-details.css`

Insérer tous les fichiers JS en fin de balise `body` dans cette ordre :

* `about.js`
* `home.js`
* `product-details.js`
* `products.js`
* `search.js`
* `not-found.js`
* `router.js`

## About

Voici le code du fichier `about.js` :

```
function about(mainEl) {
  const template = `
<p>ST Web Basics Project v1.0</p>
  `

  mainEl.innerHTML = template;

  // selection avec querySelector et
  // ajouter les addEventListener ici
}
```

Cette fonction reçoit en paramètres une référence vers l'élément `main`, le HTML qui était présent dans la balise `main` de `about.html` se retrouve maintenant dans la variable `template` et est appliquée à l'élément `main` via la propriété `innerHTML`.

## Home

Dans le fichier `home.js` reprenant la structure de la fonction `about` créer une fonction `home` avec le même contenu que le `main` de `home.html`

## Router

Nous allons créer dans le fichier `router.js` un mécanisme qui appelera la fonction `about` si l'URL `#/about` est utilisée et `home` si l'URL `#/` est utilisée.

Créer une variable `routes` avec le contenu suivant :

```
const routes = [
  {
    hash: '#/',
    render: home,
  },
  {
    hash: '#/about',
    render: about,
  },
];
```

Dans le menu, remplacer les liens :

* `home.html` par `#/`
* `about.html` par `#/about`

Créer une fonction `matchRoute` avec le code suivant :

```
function matchRoute() {
  console.log(location.hash);
}
```

Puis appeler la fonction au chargement et sur l'événement `hashchange` de `window` :

```
matchRoute();
window.addEventListener('hashchange', matchRoute);
```

Modifier la fonction `matchRoute` :

* créer une variable `mainEl` qui contiendra la référence vers l'élément main
* rechercher dans le tableau `routes` l'objet qui match `location.hash`
* appeler la fonction render de cette objet en lui passant en paramètres `mainEl`

## Not Found

Dans le fichier `notFound` créer la fonction suivante :

```
function notFound(mainEl) {
  const template = `
<p>Page not found</p>
  `

  mainEl.innerHTML = template;

  // selection avec querySelector et
  // ajouter les addEventListener ici
}
```

Dans le menu remplacer les liens :

* `products.html` par `#/products`
* `search.html` par `#/search`

Modifier la fonction `matchRoute` de `router.js` pour qu'elle appelle `notFound(mainEl)` plutôt que `render` si aucune route ne correspond à `location.hash`.

Ajouter dans cette fonction `matchRoute` un morceau de code qui va ajouter la classe `active` au lien du menu qui contient la route courante (nous avions au préalable pris le soin de souligner les liens qui auraient la classe `active` dans le fichier `common.css`). Attention la propriété `href` ne correspond pas tout à fait à la valeur de l'attribut `href`, faites un `console.log` pour afficher son format.

## Products

Dans `products.js` créer une fonction `products` sur le principe des précédentes pages.

Ajouter la route dans `router.js`

Ajouter en début de fichiers deux variables :

```
let productsList = [];
let selectedProduct = null;
```

En utilisant l'API fetch, envoyer une requête `GET` vers l'URL : `https://6a59157b-430d-4969-b802-b9c12470dafb-bluemix.cloudantnosqldb.appdomain.cloud/phones/_all_docs?include_docs=true`

La réponse du serveur est de la forme :

```
{
  "total_rows": 20,
  "offset": 0,
  "rows": [
    {
      "id": "dell-streak-7",
      "key": "dell-streak-7",
      "value": {
        "rev": "1-2cc4eb0bec0f50055f9b13b74e0e293f"
      },
      "doc": {
        "_id": "dell-streak-7",
        "_rev": "1-2cc4eb0bec0f50055f9b13b74e0e293f",
        "additionalFeatures": "Front Facing 1.3MP Camera",
        "availability": ["T-Mobile"],
        "hardware": {
          "fmRadio": false
        },
        "images": [
          "img/phones/dell-streak-7.0.jpg",
          "img/phones/dell-streak-7.1.jpg",
          "img/phones/dell-streak-7.2.jpg",
          "img/phones/dell-streak-7.3.jpg",
          "img/phones/dell-streak-7.4.jpg"
        ],
        "name": "Dell Streak 7"
      }
    },
    {
      "id": "dell-venue",
      "key": "dell-venue",
      "value": {
        "rev": "1-ea6226c888ab3de72e1a7f719e2a1bba"
      },
      "doc": {
        "_id": "dell-venue",
        "_rev": "1-ea6226c888ab3de72e1a7f719e2a1bba",
        "additionalFeatures": "Gorilla Glass display, Dedicated Camera Key, Ring Silence Switch, Swype keyboard.",
        "availability": ["AT&T,", "KT,", "T-Mobile"],
        "hardware": {
          "fmRadio": false
        },
        "images": [
          "img/phones/dell-venue.0.jpg",
          "img/phones/dell-venue.1.jpg",
          "img/phones/dell-venue.2.jpg",
          "img/phones/dell-venue.3.jpg",
          "img/phones/dell-venue.4.jpg",
          "img/phones/dell-venue.5.jpg"
        ],
        "name": "Dell Venue"
      }
    },
    {
      "id": "droid-2-global-by-motorola",
      "key": "droid-2-global-by-motorola",
      "value": {
        "rev": "1-b969ea2356dd64566b7757bd56b0d3a9"
      },
      "doc": {
        "_id": "droid-2-global-by-motorola",
        "_rev": "1-b969ea2356dd64566b7757bd56b0d3a9",
        "additionalFeatures": "Adobe Flash Player 10, Quadband GSM Worldphone, Advance Business Security, Complex Password Secure, Review & Edit Documents with Quick Office, Personal 3G Mobile Hotspot for up to 5 WiFi enabled Devices, Advanced Social Networking brings all social content into a single homescreen widget",
        "availability": ["Verizon"],
        "hardware": {
          "fmRadio": false
        },
        "images": [
          "img/phones/droid-2-global-by-motorola.0.jpg",
          "img/phones/droid-2-global-by-motorola.1.jpg",
          "img/phones/droid-2-global-by-motorola.2.jpg"
        ],
        "name": "DROID™ 2 Global by Motorola"
      }
    }
  ]
}
```

En utilisant la méthode `map` sur `rows` transformer chaque object du tableau en sa clé `"doc"`, les ajouters à la variable `productsList`.

Editer ensuite la fonction `products`, retirer les `tr` d'exemple du template.

Boucler sur la variable `productsList` et insérer dans le DOM un `tr` (en utilisant `document.createElement`) par produit.

Ecouter le click du lien, remplir la variable `selectedProduct` avec l'objet du tableau correspondant.

## Product Details

Dans `product-details.js` créer une fonction `productDetails` sur le principe des précédentes pages.

Ajouter la route dans `router.js`

Remplacer le texte et les images d'exemple avec celle contenues dans `selectedProduct`.

Au clic d'une vignette, remplacer l'attribut `src` de l'image `<img class="phone" src="...">`

## Search

Dans `search.js` créer une fonction `search` sur le principe des précédentes pages.

Ajouter la route dans `router.js`.

Ajouter en début de fichier `search.js` le code suivant :

```
const filters = {
  name: '',
  fmRadio: 'whatever',
  availability: [],
};
```

Il faudra écouter les événements `input` de tous les champs et mettre à jour l'objet `filters` en fonction.

Dans `products.js` créer une fonction `applyFilters` :

```
applyFilters(products) {
  let results = products;

  if (filters.name) {
    // results =
  }

  if (filters.fmRadio !== 'whatever') {
    // results =
  }

  if (filters.availability.length) {
    // results =
  }

  return results;
}
```

Compléter la fonction pour appliquer les filters à results.

Appeler cette fonction au moment de boucler sur les produits.

Au chargement de la page `search` afficher les valeurs de `filters` dans les champs correspondants
