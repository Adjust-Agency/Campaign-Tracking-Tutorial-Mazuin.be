# Tutoriel : Configuration du Tracking de Conversion (GA4) sur les Formulaires Drupal

**Objectif :** Permettre la remontée automatique des leads dans Google Analytics 4.

**Contexte :** Comme nous n'avons pas accès au code source du site, nous utilisons une méthode basée sur les **classes CSS**. En ajoutant deux classes spécifiques aux paramètres de vos formulaires, notre système de tracking pourra identifier automatiquement lorsqu'un formulaire est soumis et à quelle campagne il appartient.

---

### 📹 Démonstration Vidéo

https://github.com/user-attachments/assets/cb42f6b5-d782-40f9-8341-2823ad66f896

---

## ⚠️ Règles d'Or avant de commencer

1.  **Respectez la syntaxe stricte :** Les classes CSS ne supportent **aucun espace**, ni caractère spécial (accents, cédilles, etc.). Utilisez des tirets du bas (`_`) pour séparer les mots.
2.  **Ne modifiez rien d'autre :** Ce tutoriel ne concerne que l'ajout de classes dans les paramètres. Ne modifiez pas les champs ou la structure du formulaire lui-même.

---

## Guide Étape par Étape

### Étape 1 : Connexion et Préparation (L'astuce des 2 onglets)

Pour vous faciliter la tâche et accéder directement à l'édition de la bonne page, nous vous conseillons cette méthode :

1.  Ouvrez un **premier onglet** sur la page de destination (Landing Page) contenant le formulaire à traquer (ex: `/destockage-mazuin-particuliers`).
2.  Ouvrez un **nouvel onglet** et connectez-vous à l'interface d'administration Drupal (`mazuin.be/user/login`).
3.  Une fois connecté, retournez sur le **premier onglet** et **rafraîchissez la page**. La barre d'administration noire devrait apparaître en haut de la page.

### Étape 2 : Identifier le nom du formulaire

Les formulaires ont souvent des noms génériques (ex: "Action spéciale 2"). Il faut s'assurer de modifier le bon.

1.  Sur la Landing Page (avec la barre d'admin visible), cliquez sur **Modifier [Nom de la page]** (l'icône crayon).
2.  Descendez dans la page jusqu'au bloc qui contient le formulaire.
3.  Cliquez sur **Modifier** (le petit crayon) au niveau du bloc formulaire.
4.  Dans la fenêtre qui s'ouvre, regardez le champ **Formulaire**.
5.  **Notez le nom exact** de ce formulaire (ex : *Action spéciale 2*).
6.  Fermez cette fenêtre sans rien enregistrer, vous aviez juste besoin du nom.

### Étape 3 : Accéder aux paramètres du formulaire

Maintenant que nous avons le nom, nous allons éditer le formulaire lui-même.

1.  Dans le menu d'administration (en haut), allez dans **Structure** > **Webforms** (ou *Formulaires*).
2.  Dans la liste, recherchez le formulaire que vous avez identifié à l'étape précédente (ex: *Action spéciale 2*).
3.  Cliquez sur le petit bouton flèche à côté de "Modifier" et sélectionnez **Paramètres** (ou *Settings*). Si vous êtes déjà en mode édition, cliquez sur l'onglet **Paramètres du formulaire** en haut.

### Étape 4 : Ajout des classes de Tracking (CRUCIAL) 🎯

C'est ici que la magie opère. Il faut être très précis.

1.  Dans les paramètres, descendez jusqu'à la section **Attributs du formulaire**.
2.  Repérez le champ intitulé **Classes CSS de Formulaire**.
3.  Vous devez ajouter **deux classes distinctes**, séparées par un espace :

    * **La classe de déclenchement :** `campaign_action`
        *(Celle-ci indique à Google Analytics qu'il s'agit d'un formulaire à surveiller).*
    * **La classe d'identification :** `campaign_label_votre_nom_de_campagne`
        *(Celle-ci nous permet de nommer la conversion dans les rapports).*

**Exemple concret pour l'action déstockage :**

Vous devez écrire dans le champ :
`campaign_action campaign_label_destockage_particuliers`

> **Note importante :**
> * Pour la deuxième classe, remplacez `votre_nom_de_campagne` par un nom explicite (ex: `destockage_particuliers`, `action_seat_mars`, etc.).
> * **Rappel :** **Pas d'espace** DANS le nom de la classe. Utilisez des `_` (underscores). **Pas d'accents non plus** !
> * L'espace sert uniquement à séparer la première classe de la deuxième.

4.  Une fois les classes ajoutées, descendez tout en bas et cliquez sur **Enregistrer**.

### Étape 5 : Vérification (Optionnelle mais recommandée)

Pour être sûr que tout fonctionne :

1.  Déconnectez-vous de Drupal ou ouvrez la Landing Page dans une fenêtre de **navigation privée**.
2.  Faites un clic droit sur le formulaire et choisissez **Inspecter**.
3.  Dans la console qui s'ouvre, cherchez la balise `<form ...>`.
4.  Vérifiez que vous voyez bien `class="... campaign_action campaign_label_destockage_particuliers ..."` à l'intérieur de la balise.

Si les classes sont là, le tracking est opérationnel !

---

### Récapitulatif technique

| Champ à modifier | Webform Settings > Form Attributes > Form CSS Classes |
| :--- | :--- |
| **Classe 1 (Trigger)** | `campaign_action` |
| **Classe 2 (Label)** | `campaign_label_nom_de_la_campagne` |
| **Format** | Snake_case uniquement (pas d'espaces, pas de majuscules, pas d'accents) |
