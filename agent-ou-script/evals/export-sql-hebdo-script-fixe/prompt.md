---
tags: [agent-ou-script]
max_turns: 10
timeout_seconds: 300
allowed_tools: [Read, Glob, Grep, Skill]
---

Chaque lundi matin j'exporte depuis notre base Postgres la liste des inscriptions de la semaine (nom, date, source), je la colle dans un Google Sheet et j'envoie le lien à mon équipe par email. Un collègue m'a dit que je devrais construire un agent IA pour ça. T'en penses quoi, ça vaut le coup ?
