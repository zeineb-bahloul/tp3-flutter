# 🤖 Rapport d'utilisation d'un Agent IA — TP Flutter

**Étudiante :** Zeineb Bahloul  
**Date :** 06 Octobre 2026  
**Projet :** Waiting Room App (Flutter)  
**Outil IA utilisé :** ChatGPT (chat.openai.com)  
**Modèle IA :** GPT-4o (OpenAI)

---

## 1. Présentation de l'outil

J'ai utilisé **ChatGPT**, un assistant conversationnel développé par **OpenAI**, accessible via le navigateur à l'adresse `chat.openai.com`. Le modèle utilisé est **GPT-4o**.

ChatGPT permet de poser des questions en langage naturel et d'obtenir des réponses sous forme de texte, d'explications ou de suggestions de code.

---

## 2. Contexte du TP

Le TP consistait à faire évoluer une application Flutter de gestion de salle d'attente (Waiting Room App) en appliquant les concepts suivants :
- **TDD (Test-Driven Development)** — écrire les tests avant le code
- **State Management avec Provider** — remplacer le `setState()` par le pattern `ChangeNotifier` + `Provider`
- **Ajout d'une nouvelle fonctionnalité** — la méthode `nextClient()` pour appeler le client suivant

---

## 3. Comment j'ai utilisé ChatGPT

J'ai utilisé ChatGPT comme **outil d'assistance** pour m'aider à comprendre certains concepts et me débloquer quand j'avais des doutes. Voici les questions principales que j'ai posées :

### 💬 Question 1 — Comprendre Provider

> **Moi :** « Comment utiliser le package Provider en Flutter pour gérer l'état d'une liste ? »

> **ChatGPT :** Il m'a expliqué le concept de `ChangeNotifier` et comment utiliser `notifyListeners()` pour informer l'UI des changements. Il m'a aussi montré la différence entre `context.watch()` et `context.read()`.

Grâce à cette explication, j'ai pu créer ma classe `QueueProvider` qui étend `ChangeNotifier`.

---

### 💬 Question 2 — Approche TDD

> **Moi :** « Comment appliquer le TDD en Flutter ? Je dois ajouter une méthode nextClient() qui retire le premier client de la liste. »

> **ChatGPT :** Il m'a guidée sur l'approche Red → Green :
> 1. D'abord écrire un test qui appelle `nextClient()` (le test échoue car la méthode n'existe pas encore)
> 2. Ensuite implémenter la méthode pour que le test passe

J'ai suivi cette approche pour écrire mon test, puis j'ai implémenté la méthode `nextClient()` dans `QueueProvider`.

---

### 💬 Question 3 — Refactoring avec Provider

> **Moi :** « Comment transformer un StatefulWidget en StatelessWidget en utilisant Provider ? »

> **ChatGPT :** Il m'a expliqué qu'il faut :
> - Envelopper l'application avec `ChangeNotifierProvider` dans `main()`
> - Utiliser `context.watch<QueueProvider>()` pour écouter les changements d'état
> - Utiliser `context.read<QueueProvider>()` pour déclencher des actions sans écouter

J'ai appliqué ces conseils pour refactorer mon fichier `main.dart`.

---

### 💬 Question 4 — Tests widget avec Provider

> **Moi :** « Mes tests widget échouent après la migration vers Provider. Comment corriger ça ? »

> **ChatGPT :** Il m'a indiqué qu'il fallait envelopper le widget testé avec `ChangeNotifierProvider` dans chaque test, comme ceci :
> ```dart
> await tester.pumpWidget(
>   ChangeNotifierProvider(
>     create: (context) => QueueProvider(),
>     child: const WaitingRoomApp(),
>   ),
> );
> ```

J'ai corrigé mes tests et ils sont tous passés.

---

## 4. Résumé des fichiers modifiés/créés

| Fichier | Action | Description |
|---------|--------|-------------|
| `pubspec.yaml` | Modifié | Ajout de `provider: ^6.0.0` |
| `lib/queue_provider.dart` | **Créé** | Nouveau modèle `QueueProvider` avec `ChangeNotifier` |
| `lib/main.dart` | Modifié | Refactoring avec Provider, ajout bouton Next Client |
| `lib/waiting_room_manager.dart` | Supprimé | Remplacé par `queue_provider.dart` |
| `test/waiting_room_manager_test.dart` | Modifié | Mis à jour pour `QueueProvider` + test `nextClient()` |
| `test/waiting_room_widget_test.dart` | Modifié | Ajout Provider dans les tests + test Next Client |

---

## 5. Ce que j'ai appris

Grâce à ce TP et à l'aide de ChatGPT pour les explications, j'ai pu comprendre :
- ✅ Le **pattern Provider** et `ChangeNotifier` pour la gestion d'état en Flutter
- ✅ La différence entre `context.watch()` (écouter les changements) et `context.read()` (lire sans écouter)
- ✅ L'approche **TDD** (Red → Green → Refactor)
- ✅ Comment structurer les tests unitaires et les tests widget avec Provider
- ✅ L'injection de dépendances avec `ChangeNotifierProvider`

---

## 6. Conclusion

ChatGPT m'a été utile principalement pour **comprendre les concepts** (Provider, TDD, ChangeNotifier) et pour **me débloquer** quand je rencontrais des erreurs. J'ai ensuite écrit le code moi-même en m'appuyant sur ces explications.

---

> *Ce rapport a été rédigé pour documenter l'utilisation d'un outil IA dans le cadre d'un TP Flutter.*
