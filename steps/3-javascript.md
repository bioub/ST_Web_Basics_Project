# Etape 3 - Javascript

Après avoir créé un dossier `pages` qui était une application HTML/CSS statique, nous allons créer un équivalent plus dynamique où il n'y aura qu'un seul fichier HTML (`index.html`), le passage d'une "page" à une autre se fera en appelant une fonction JavaScript qui remplira la balise `main` via le DOM.

On parle alors de *Single Page Application*.

Créer un nouveau dossier `spa` à la racine du projet (à côté du dossier `pages`) et y recopier les dossiers `css` et `img`

Ajouter un dossier `js` avec 7 fichiers :

* `about.js`
* `home.js`
* `product-details.js`
* `products.js`
* `search.js`
* `not-found.js`
* `router.js`

## HTML

Créer un fichier `index.html` qui reprend la balise `header` avec les liens et la balise `main` vide.

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
  `;

  mainEl.innerHTML = template;

  // si besoin on pourra sélectionner les éléments insérés
  // dans le main ici, par exemple pour ajouter les produits
  // reçus du serveur sur la page products ou pour
  // écouter des événements UI.
  // ex :
  // const pEl = mailEl.querySelector('p');
}
```

Cette fonction reçoit en paramètre une référence vers l'élément `main`, le HTML qui était présent dans la balise `main` de `about.html` se retrouve maintenant dans la variable `template` et est appliquée à l'élément `main` via la propriété du DOM `innerHTML`.

## Home

Dans le fichier `home.js` reprenant la structure de la fonction `about` créer une fonction `home` avec le même contenu que le `main` de `home.html`

## Routeur

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

Dans le menu du fichier `index.html`, remplacer les liens :

* `home.html` par `#/`
* `about.html` par `#/about`

Créer dans `router.js` une fonction  `matchRoute` avec le code suivant :

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

Vous devriez voir qu'en cliquant alternativement sur `Home` et `About` la fonction `matchRoute` est appelée et que `location.hash` contient `#/` ou `#/about`.

Nous allons ensuite éditer la fonction `matchRoute` pour quelle recherche dans le tableau `routes` un objet qui correspond à `location.hash` si c'est le cas, on appelera la fonction render de cet objet en lui passant en paramètre la référence sur l'élément `main` et la fonction devrait alors remplir la balise `main`.

Modifier la fonction `matchRoute` :

* créer une variable `mainEl` qui contiendra la référence vers l'élément `main`
* rechercher dans le tableau `routes` l'objet qui correspond à `location.hash`
* appeler la méthode `render` de cet objet (celle définie dans `routes` donc) en lui passant en paramètre `mainEl`

## Not Found

Dans le fichier `notFound` créer la fonction suivante :

```
function notFound(mainEl) {
  const template = `
<p>Page not found</p>
  `;

  mainEl.innerHTML = template;
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

En utilisant la méthode `map` sur la propriété `rows` de la réponse, transformer chaque object du tableau en sa clé `doc`, écrire ce nouveau tableau dans `productsList`.

Editer ensuite la fonction `products`, retirer les `tr` d'exemple du template (on gardera le premier `tr` qui affiche le nom des colonnes).

Après la ligne `mainEl.innerHTML = template`, boucler sur la variable `productsList` et insérer dans le DOM un `tr` (en utilisant `document.createElement`, `appendChild()`...) par produit.

Ecouter le clic du lien Show, remplir la variable `selectedProduct` avec l'objet du tableau correspondant.

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
