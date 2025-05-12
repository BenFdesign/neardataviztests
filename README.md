# neardataviztests
Tests et architecture pour les dataviz NEAR

## Règles pour l'architecture des dataviz :
- L'app est en React, on utilise donc components/ pour stocker les dataviz en tant que composants réutilisables.
- Chaque dataviz correspond à une question ou un set de données, et a son propre dossier qui comprend 2 fichiers :
  - _data.ts_ pour le fetch ou le mock des données (séparé pour permettre d'appeler des mêmes données dans différentes dataviz répondant à une question similaire).
  - _dvidentifiant.tsx_ pour l'affichage, le tooltip et la personnalisation du style ; _identifant_ doit être remplacé par un nom unique et clair pour le type et la version de la dataviz (par exemple _dv_SUviolins2024_ ; cela permet aussi un futur enrichissement communautaire de la banque de dataviz).
  - Appels dans la BDD avec _pages/api/dataviz/QuestionsA_api.ts_, créer un appel pour chaque question (ou un fichier unique ?)

## Arborescence proposée
```
root/
├── components/
│   ├── dataviz/
|   |   ├── registry.ts               # Optionnel : créer un registre de données pour appeler enccore plus facilement les modules dv.
│   │   ├── common/
│   │   │   └── styles.ts             # Styles globaux communs à toutes les dataviz (fonts, fontsize, sets de couleur, ...)
│   │   ├── QuestionA_dv/             # Question posée (par exemple : usagesSU pour _répartition des usages_)
│   │   │   ├── dv1.tsx               # Composant principal avec SVG et tooltip
│   │   │   ├── data.ts               # Fetch ou mock des données (filtrées par `ngh`, `su`) (permet de faire différentes dv avec le même jeu de données).
│   │   └── QuestionB_dv/
│   │       ├── dv1.tsx               # Même structure pour d'autres dataviz
│   │       ├── data.ts
│   │       └── styles.ts
├── pages/
│   ├── api/
│   │   └── dataviz/
│   │       ├── QuestionA_api.ts      # (à implémenter dans le futur) Accès aux données depuis Metabase via API
│   │       └── QuestionB_api.ts      # Fonction backend TS pour interroger l'API Metabase avec SQL brut ? Vitesse en réplication ?
│   └── boards/
│       └── nomduboard.tsx            # Page dynamique affichant un tableau de dataviz, dans lequelle on peut 
├── public/
├── styles/
├── Dockerfile
├── docker-compose.yml
├── package.json
└── tsconfig.json
```

