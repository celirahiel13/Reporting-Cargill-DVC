# Reporting Cargill

Appli de comptes rendus d'intervention pour Dimitri Van Calster (Cargill).
Elle remplace le fichier Excel « Reporting_Cargill » : une saisie par intervention,
regroupée par semaine et par jour, avec export PDF et envoi par mail au n+1.

## Contenu du dossier

| Fichier | Rôle |
|---|---|
| `index.html` | L'appli entière (écrans, calculs, PDF) |
| `manifest.webmanifest` | Permet de l'installer sur l'écran d'accueil du téléphone |
| `sw.js` | Garde l'appli disponible sans réseau |
| `icons/` | Icônes de l'appli |

## 1. Mettre l'appli en ligne (GitHub Pages)

1. Sur GitHub, crée un nouveau dépôt (par exemple `reporting-cargill`), en public.
2. « Add file » → « Upload files » : glisse **tout le contenu** du dossier (y compris le dossier `icons`), puis « Commit changes ».
3. « Settings » → « Pages » → Source : « Deploy from a branch », branche `main`, dossier `/ (root)` → « Save ».
4. Au bout d'une minute, l'adresse apparaît en haut de la page Pages : `https://TON-PSEUDO.github.io/reporting-cargill/`.

Le dépôt ne contient aucune donnée : les comptes rendus restent sur le téléphone de Dimitri.

## 2. L'installer sur le téléphone de Dimitri

- **iPhone (Safari)** : ouvrir l'adresse → bouton Partager → « Sur l'écran d'accueil ».
- **Android (Chrome)** : ouvrir l'adresse → menu ⋮ → « Installer l'application » (ou « Ajouter à l'écran d'accueil »).

Ensuite, dans l'appli : **Réglages** → renseigner le nom et l'adresse mail du n+1.

## 3. Utilisation au quotidien

1. Onglet **Semaines** (du lundi au vendredi) : la semaine en cours en surbrillance, suivie des 13 semaines à venir (environ 3 mois) ; les semaines passées s'affichent avec le bouton « Voir les semaines passées » au-dessus. Toucher un jour pour l'ouvrir (un seul jour ouvert à la fois).
2. « Créer nouveau compte rendu d'intervention » :
   - **Work order** : photographier le WO ou choisir le PDF → le n° de WO, le bâtiment, la localisation et le travail demandé se remplissent automatiquement (modifiables si la lecture s'est trompée). Photo bien à plat, nette et éclairée pour un meilleur résultat.
   - **Date** au calendrier, **horaires** début/fin (ou raccourcis Journée / Matin / Après-midi). La pause déjeuner est déduite.
   - **Commentaires** : à la voix avec le bouton micro. Si la dictée n'est pas disponible, le micro du clavier du téléphone fonctionne aussi.
   - **Temps passé** : calculé d'après les horaires, modifiable dans la liste.
   - **Cumul sur ce WO** : additionne automatiquement toutes les interventions qui portent le même n° de WO. Modifiable si une partie du travail a été faite avant d'utiliser l'appli.
   - **Photos** : appareil photo ou galerie.
   - « Enregistrer + nouveau » enchaîne directement sur l'intervention suivante du même jour.
   - **Prévoir une autre intervention** : à cocher si le travail n'est pas fini ; le WO reste alors dans « Work Orders à traiter ou à terminer ».
3. Envoi au n+1 : chaque jour (bouton « Envoyer » sur la journée) ou chaque semaine (« Envoyer le reporting de la semaine »), au choix dans Réglages.
4. Onglet **Mes WO** :
   - **Anciens work orders → Work Orders à traiter ou à terminer** : les WO importés pas encore faits, et tous les WO où « Prévoir une autre intervention » a été coché. **Bleu = à traiter** (pas commencé), **orange = à terminer** (commencé ou en attente) ; la légende en haut sert aussi de filtre. Depuis un WO : créer le compte rendu, l'envoyer directement, modifier ses infos ou le marquer comme réalisé.
   - **Anciens work orders → Work Orders réalisés** : les WO terminés (dont les anciens marqués « ok fait »). Chaque WO peut être modifié et envoyé seul ; « Choisir » ou « Tout envoyer » envoie plusieurs WO dans un seul PDF.
   - Les deux listes sont triées par ordre alphabétique, avec recherche par mot clé et filtres (priorité, bâtiment, type de demande, date, envoyé ou non, anciens ou nouveaux).
   - **Historique → WO envoyés** : tous les WO déjà envoyés au n+1.
   - « Importer un fichier de work orders » : pour charger un lot de WO préparé à part (fichier .json).

Le PDF reprend la présentation du reporting Excel actuel (date, horaires, WO, intervention, observations, temps, cumul WO, total jour et total semaine), avec les photos en annexe et **les work orders joints en fin de PDF** (désactivable dans Réglages).

Si le téléphone se met en veille pendant la saisie, le brouillon est gardé et proposé à la réouverture.

## 4. Envoi par mail

**Par défaut (rien à configurer)** : « Envoyer par mail » ouvre la liste de partage du téléphone. On choisit Gmail (ou Outlook) : le PDF, l'objet et le message sont déjà remplis, il reste à mettre l'adresse du n+1 et à envoyer.

**Envoi direct depuis Gmail (optionnel, environ 15 minutes de réglage, une seule fois)** : l'appli envoie elle-même le mail avec le PDF depuis la boîte Gmail de Dimitri, destinataire déjà rempli, en un seul bouton.

1. Aller sur https://console.cloud.google.com avec un compte Google, et créer un projet (« Reporting Cargill »).
2. **Activer l'API Gmail** : menu ☰ → « API et services » → « Bibliothèque » → chercher **Gmail API** → « Activer ».
3. **Écran de consentement** : chercher « OAuth » dans la barre du haut → « Google Auth Platform » → « Commencer » :
   - Informations sur l'application : nom « Reporting Cargill », ton adresse mail ;
   - Audience : **Externe** ;
   - Coordonnées : ton adresse mail ;
   - accepter et « Créer ».
4. Onglet **Audience** → « Utilisateurs test » → « Add users » : ajouter **l'adresse Gmail de Dimitri**. Laisser l'appli en mode « Test ».
5. Onglet **Accès aux données** (Data access) → « Ajouter ou supprimer des champs d'application » → ajouter `https://www.googleapis.com/auth/gmail.send` → « Mettre à jour » → « Enregistrer ».
6. Onglet **Clients** → « Créer un client » → type **Application Web**.
   Dans « Origines JavaScript autorisées », ajouter `https://TON-PSEUDO.github.io` (sans le nom du dépôt, sans `/` à la fin). Rien à mettre dans les URI de redirection. « Créer ».
7. Copier l'**ID client** (il finit par `.apps.googleusercontent.com`). Le code secret n'est pas utile.
8. Dans `index.html`, tout en haut du script, coller l'ID entre les guillemets :
   `googleClientId: '1234-abcd.apps.googleusercontent.com'`
   puis renvoyer `index.html` sur GitHub (« Add file » → « Upload files » → « Commit changes »).

Au premier envoi, Google affiche « Google n'a pas validé cette application » : c'est normal pour une appli personnelle en mode test. Toucher « Continuer », puis autoriser l'envoi de mails. L'appli ne demande que le droit d'**envoyer** des mails, pas de les lire.

## 5. Sauvegarde

Les données sont stockées dans le navigateur du téléphone. Si on efface les données de Safari/Chrome ou qu'on change de téléphone, elles disparaissent.
Réglages → « Sauvegarder mes données » crée un fichier (photos comprises) à garder dans Drive ou par mail ; « Restaurer une sauvegarde » le recharge.

## 6. Bon à savoir

- La première ouverture, le premier PDF et la première lecture de WO par photo ont besoin de réseau (chargement des outils). Ensuite tout fonctionne hors ligne, sauf l'envoi du mail.
- La lecture d'un WO en PDF est quasi instantanée. Par photo, compter 10 à 30 secondes selon le téléphone ; une photo nette, à plat et bien éclairée donne les meilleurs résultats.
- La lecture automatique repère les intitulés courants d'un ordre de travail (« Ordre », « Avis », « Poste technique », « Équipement », « Description », « Bât. »…). Si le format Cargill utilise d'autres intitulés, quelques lignes de `parseWO` dans `index.html` sont à ajuster.

## 7. Importer les anciens work orders (une seule fois)

1. Envoyer le fichier `anciens-work-orders.json` à Dimitri (mail ou WhatsApp) et l'enregistrer dans « Fichiers » sur son téléphone.
2. Dans l'appli : onglet **Mes WO** → en bas, « Importer un fichier de work orders » → choisir le fichier → « Importer ».
3. Les WO arrivent classés dans « à traiter ou à terminer » et « réalisés », avec la photo de chaque WO.

Ce fichier contient des documents Cargill : il ne doit pas être mis sur GitHub.
