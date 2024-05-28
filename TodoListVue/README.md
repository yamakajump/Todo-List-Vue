# TodoListVue

Cette application de gestion des tâches a été réalisée avec Vue.js. Elle permet aux utilisateurs d'ajouter, supprimer et filtrer des tâches en fonction de différents critères comme l'état, la priorité et les dates. Les données sont stockées dans le local storage du navigateur pour une persistance locale.

## Fonctionnalités

- Ajouter une tâche via un formulaire
- Supprimer une tâche
- Afficher la liste des tâches
- Filtrer les tâches par état (à faire, en cours, terminé)
- Filtrer les tâches par priorité (haute, moyenne, basse)
- Filtrer les tâches par date de début
- Filtrer les tâches par date de fin

## Technologies utilisés

- [Vue.js](https://vuejs.org/) : Framework JavaScript pour construire l'interface utilisateur
- [Bootstrap](https://getbootstrap.com/) : Framework CSS pour le design et la mise en page
- [Local Storage](https://developer.mozilla.org/fr/docs/Web/API/Window/localStorage) : API Web pour le stockage des données sur le navigateur

## Project Setup

### **Naviguez dans le dossier du projet**

```sh
cd TodoListVue
```

### Installez les dépendances

```sh
npm install
```

### Démarrez le serveur de développement

```sh
npm run dev
```

Ouvrez votre navigateur et accédez à l'URL indiquée (généralement `http://localhost:3000`).

## Structure du projet

TodoListVue/
├── index.html
├── jsconfig.json
├── package.json
├── package-lock.json
├── public
│   └── favicon.ico
├── README.md
├── src
│   ├── App.vue
│   ├── assets
│   │   ├── base.css
│   │   ├── logo.svg
│   │   └── main.css
│   ├── components
│   │   ├── AddTaskForm.vue
│   │   ├── TaskList.vue
│   │   └── TaskItem.vue
│   └── main.js
└── vite.config.js

## Composants principaux

* `App.vue` : Composant racine de l'application.
* `AddTaskForm.vue` : Composant pour le formulaire d'ajout de tâche.
* `TaskList.vue` : Composant pour afficher la liste des tâches.
* `TaskItem.vue` : Composant pour afficher une tâche individuelle.

## Auteur

* **BATARD Corentin**
* **BASOL Nathan**

## License

Ce projet est sous licence MIT - voir le fichier [LICENSE]() pour plus de détails.
