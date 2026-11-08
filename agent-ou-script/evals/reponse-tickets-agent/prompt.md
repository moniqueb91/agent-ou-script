---
tags: [agent-ou-script]
max_turns: 10
timeout_seconds: 300
allowed_tools: [Read, Glob, Grep, Skill]
---

On reçoit une centaine de tickets support par jour. J'ai déjà un scénario Make qui les classe par thème avec un modèle d'IA. Maintenant j'aimerais automatiser les réponses : aller chercher l'info dans notre base de connaissances ou dans l'historique du client, répondre avec le bon ton, et passer la main à quelqu'un de l'équipe quand c'est sensible ou que l'info manque. Est-ce que je peux juste rajouter des modules à mon scénario Make, ou il me faut un agent ?
