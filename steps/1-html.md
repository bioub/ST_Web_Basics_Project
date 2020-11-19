# Etape 1 - HTML

Créer un dossier pour le projet si ce n'est pas déjà fait.

## HTML commun

Créer un dossier `pages` avec 5 fichiers HTML :

* `home.html`
* `about.html`
* `search.html`
* `products.html`
* `product-details.html`

Le HTML de chaque fichier devra avoir la structure suivante :

```
<body>
  <header>
    <!-- menu -->
  </header>
  <main>
    <!-- page -->
  </main>
</body>
```

Le menu est le même sur toutes les pages.

Dans le menu, ajouter la classe `active` pour la page courante (le lien sera souligné).

## Home

La page home ne contient que 2 liens :
* ST.com -> https://www.st.com/
* Search Products -> la page search.html

Ces deux liens doivent avoir la classe `btn-link`.

## About

La page about contient un paragraphe avec le texte :

ST Web Basics Project v1.0

## Search

La page search contient un formulaire avec 3 champs

* name de type text
* fmRadio de type radio, 3 valeurs : Yes, No, Whatever (peu importe)
* availability de type checkbox, 2 valeurs : T-Mobile, Verizon

Elle contient également un lien `Search` vers la page `products.html` et la même classe `btn-link` utilisée dans `Home`.

## Products

Insérer le HTML suivant dans la balise `main` de `products.html` :

```
<table>
  <tr>
    <th>ID</th>
    <th>Name</th>
    <th>Additionnal Features</th>
    <th>Actions</th>
  </tr>
  <tr>
    <td>dell-streak-7</td>
    <td>Dell Streak 7</td>
    <td>Front Facing 1.3MP Camera</td>
    <td>
      <a href="product-details.html">Show</a>
    </td>
  </tr>
  <tr>
    <td>dell-venue</td>
    <td>Dell Venue</td>
    <td>
      Gorilla Glass display, Dedicated Camera Key, Ring Silence Switch,
      Swype keyboard.
    </td>
    <td>
      <a href="product-details.html">Show</a>
    </td>
  </tr>
  <tr>
    <td>droid-2-global-by-motorola</td>
    <td>DROID™ 2 Global by Motorola</td>
    <td>
      Adobe Flash Player 10, Quadband GSM Worldphone, Advance Business
      Security, Complex Password Secure, Review & Edit Documents with
      Quick Office, Personal 3G Mobile Hotspot for up to 5 WiFi enabled
      Devices, Advanced Social Networking brings all social content into a
      single homescreen widget
    </td>
    <td>
      <a href="product-details.html">Show</a>
    </td>
  </tr>
</table>
```

## Products Details

Récupére le dossier `img` de ce projet et le copier dans le dossier `pages`.

Insérer le HTML suivant dans la balise `main` de `product-details.html` :

```
<div class="phone-image">
  <img class="phone" src="img/phones/dell-streak-7.0.jpg" />
</div>
<h1>Dell Streak 7</h1>
<p>
  Introducing Dell™ Streak 7. Share photos, videos and movies together.
  It’s small enough to carry around, big enough to gather around. Android™
  2.2-based tablet with over-the-air upgrade capability for future OS
  releases. A vibrant 7-inch, multitouch display with full Adobe® Flash
  10.1 pre-installed. Includes a 1.3 MP front-facing camera for
  face-to-face chats on popular services such as Qik or Skype. 16 GB of
  internal storage, plus Wi-Fi, Bluetooth and built-in GPS keeps you in
  touch with the world around you. Connect on your terms. Save with 2-year
  contract or flexibility with prepaid pay-as-you-go plans
</p>
<ul class="phone-thumbs">
  <li>
    <img src="img/phones/dell-streak-7.0.jpg" />
  </li>
  <li>
    <img src="img/phones/dell-streak-7.1.jpg" />
  </li>
  <li>
    <img src="img/phones/dell-streak-7.2.jpg" />
  </li>
  <li>
    <img src="img/phones/dell-streak-7.3.jpg" />
  </li>
  <li>
    <img src="img/phones/dell-streak-7.4.jpg" />
  </li>
</ul>
```
