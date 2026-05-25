Agent Musical IA Automatisé avec Telegram + n8n + Suno AI

## Présentation du Projet

Ce projet permet de créer automatiquement des musiques IA directement depuis Telegram grâce à :

* n8n
* DeepSeek AI
* Suno API

L’utilisateur envoie simplement un prompt musical dans Telegram, et le système :

1. génère des paroles
2. crée la musique
3. récupère le fichier MP3
4. renvoie automatiquement l’audio dans Telegram.

---

# Technologies Utilisées

| Outil         | Rôle                           |
| ------------- | ------------------------------ |
| Telegram Bot  | Interface utilisateur          |
| n8n           | Automatisation du workflow     |
| DeepSeek      | Analyse intelligente du prompt |
| Suno API      | Génération musicale IA         |
| HTTP Requests | Communication API              |

---

# Fonctionnement Global

## Workflow principal

```text id="w5j3zx"
Telegram Message
↓
Generate Lyrics
↓
Wait
↓
Check Lyrics Status
↓
AI Agent (DeepSeek)
↓
Generate Music
↓
Wait
↓
Check Music Status
↓
Download MP3
↓
Send Audio to Telegram
```

---

# Étape 1 — Réception du Prompt Telegram

Le workflow démarre lorsqu’un utilisateur envoie un message au bot Telegram.

### Exemple :

```text id="9z0ffl"
Créer un son trap futuriste sur une IA qui contrôle le monde
```

Le node utilisé :

```text id="lqvwk2"
Telegram Trigger
```

---

# Étape 2 — Génération des Paroles

Le prompt utilisateur est envoyé à Suno API afin de générer automatiquement des paroles.

### Endpoint utilisé

```text id="1xg5r8"
POST /api/v1/lyrics
```

Le système récupère ensuite un :

```text id="vdr09l"
taskId
```

qui permettra de suivre la génération.

---

# Étape 3 — Boucle d’Attente

La génération prend quelques secondes.

Le workflow utilise :

* un node Wait
* un node IF

afin de vérifier régulièrement si les paroles sont prêtes.

### Condition utilisée

```javascript id="xg6w2q"
{{ $json.data.status === "SUCCESS" }}
```

---

# Étape 4 — Analyse IA avec DeepSeek

Une fois les paroles générées, DeepSeek analyse la demande utilisateur pour créer les métadonnées musicales :

* style musical
* titre
* paramètres Suno
* tags négatifs

---

# Structure JSON Générée

```json id="78o7q3"
{
  "style": "Trap",
  "title": "Neon Dominion",
  "customMode": true,
  "instrumental": false,
  "model": "V4_5ALL",
  "negativeTags": "acoustic, classical, slow, ballad",
  "callbackUrl": "https://api.example.com/callback"
}
```

---

# Étape 5 — Génération de la Musique

Le workflow envoie :

* les paroles
* le style
* le titre
* les paramètres IA

à Suno API.

### Endpoint utilisé

```text id="ejbqjl"
POST /api/v1/generate
```

---

# Étape 6 — Vérification du Statut Audio

Comme pour les paroles, la génération audio est asynchrone.

Le système :

1. attend
2. vérifie le statut
3. recommence jusqu’au succès.

### Endpoint utilisé

```text id="2y54pb"
GET /api/v1/generate/record-info
```

---

# Étape 7 — Récupération du MP3

Quand le statut devient :

```text id="oq7k61"
SUCCESS
```

le workflow récupère :

* le MP3
* le lien streaming
* l’image de couverture.

---

# Étape 8 — Envoi dans Telegram

Le MP3 est automatiquement envoyé à l’utilisateur via Telegram.

### Node utilisé

```text id="zch8fr"
Telegram → Send Audio
```

---

# Données Récupérées

Le système récupère automatiquement :

| Donnée         | Description         |
| -------------- | ------------------- |
| audioUrl       | lien MP3            |
| streamAudioUrl | lien streaming      |
| imageUrl       | cover image         |
| title          | titre de la musique |

---

# Gestion Asynchrone

Le projet utilise un système de polling :

* Wait Node
* IF Node
* Retry Loop

afin d’attendre la fin des tâches IA.

---

# Difficultés Résolues

## Erreur “Node was not executed”

Cause :

* mauvaise condition IF

Solution :

```text id="vf33cw"
SUCCESS
```

---

## Erreur “model error”

Cause :

* mauvais modèle
* payload invalide

Solution :

```text id="jlwmco"
V4_5ALL
```

---

# Optimisations Futures

Le système peut évoluer avec :

* génération de cover IA
* mémoire conversationnelle
* base de données
* gestion multi-utilisateurs
* monétisation Telegram

---

# Conclusion

Ce projet démontre comment construire un agent musical IA autonome sans backend complexe grâce à :

* Telegram
* n8n
* DeepSeek
* Suno API

Le système est capable de transformer un simple prompt texte en musique IA complète automatiquement.

Workflow complet : 
