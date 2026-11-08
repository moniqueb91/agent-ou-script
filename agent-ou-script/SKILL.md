---
name: agent-ou-script
description: "Aide à choisir le bon niveau d'automatisation pour une tâche : script classique, workflow IA, skill ou agent IA. À utiliser dès que l'utilisateur décrit une tâche à automatiser, un workflow (n8n, Make, Zapier, Python, Apps Script) ou un projet d'IA et hésite sur la solution, même s'il ne prononce pas le mot « agent » : « est-ce que j'ai besoin d'un agent ? », « workflow ou skill ? », « skill ou sous-agent ? », « est-ce que c'est vraiment un agent ? », « est-ce que l'IA sert à quelque chose ici ? », « un script suffit ? », « do I need an agent or a script? », « workflow vs skill vs agent », « should I build an AI agent for this? ». À utiliser aussi pour vérifier si un projet présenté comme un agent en est réellement un."
---

# Choisir le bon niveau d'automatisation : script, workflow IA, skill ou agent

## Principe

Chercher la solution la plus simple qui fonctionne, et n'ajouter de la complexité que lorsqu'elle est nécessaire. Un agent est souvent plus lent et plus cher qu'une automatisation classique, en échange de meilleurs résultats sur certaines tâches. Il faut donc vérifier que la tâche demande vraiment ce niveau de complexité.

La décision se prend en trois questions, posées dans l'ordre. On s'arrête à la première qui tranche.

## Avant tout : faut-il automatiser ?

L'IA permet d'automatiser très vite un processus qu'on n'a pas pris le temps de comprendre. Avant de choisir un outil, vérifier deux points :
- Le processus actuel est-il bien compris ? Automatiser un processus défaillant ne fait que reproduire ses défauts plus vite.
- La tâche est-elle à la fois répétitive et utile ? Une tâche répétitive mais à faible valeur ne justifie pas toujours le temps de construction.

Si l'un des deux points n'est pas clair, le signaler avant de proposer une solution. Une tâche faite une seule fois n'est pas un sujet d'automatisation : un simple échange avec un modèle suffit.

## Les quatre options

| Option | Ce que c'est | Qui décide du déroulement | Besoin d'une personne ? |
|---|---|---|---|
| Script classique | Du code sans IA (Python, SQL, Apps Script, scénario no-code sans module IA) | Le code, entièrement | Non |
| Workflow IA | Des étapes qui s'enchaînent selon un parcours prédéfini, avec un modèle d'IA inséré à des points précis : script qui appelle un modèle via une API, ou scénario Make, Zapier ou n8n avec un module IA | Le parcours prédéfini ; le modèle traite l'information à certaines étapes | Non |
| Skill | Un ensemble d'instructions enregistré dans l'outil d'IA, utilisé dans une conversation ou intégré à un agent. Il formalise des consignes métier et peut contenir des scripts | Les consignes du skill, avec la personne qui précise et corrige en cours de route | Oui, sauf s'il est utilisé par un agent |
| Agent IA | Un système qui utilise un modèle pour atteindre un objectif, en prenant ses décisions de façon autonome | Le modèle | Non |

Le workflow IA et le skill sont au même niveau : ce qui les sépare n'est pas la complexité, mais le besoin d'interaction.

## Question 1 : script classique ou IA ?

> La tâche peut-elle être entièrement exécutée avec du code classique, sans modèle de langage ?

Un script classique suffit quand :
- les étapes sont entièrement prévisibles et structurées ;
- le résultat prend toujours la même forme ;
- le travail consiste à calculer, compter, trier, parser des fichiers (JSON, CSV, XML), lancer des requêtes SQL ou appeler une API avec des paramètres fixes.

Pourquoi le préférer : il s'exécute de façon déterministe, instantanément, sans risque d'hallucination et gratuitement. Il évite aussi d'envoyer des données, parfois personnelles, à un modèle externe.

Ne pas savoir coder n'est pas une raison de passer par l'IA à chaque exécution : on peut faire générer le script une fois par une IA, puis l'exécuter soi-même les fois suivantes.

L'IA devient pertinente quand la tâche demande au moins l'une de ces choses :
- comprendre ou générer du texte ;
- manipuler du texte non structuré (emails, tickets, comptes rendus, commentaires) ;
- suivre des étapes qui ne sont pas totalement prévisibles.

## Question 2 : workflow IA ou skill ?

> La tâche a-t-elle besoin de contexte, d'interaction ou de clarification de la part de la personne pour être bien réalisée ?

- **Non → workflow IA.** Le processus suit des étapes dans un ordre fixe, sans improvisation, mais doit comprendre ou générer du texte. Le modèle n'a pas besoin qu'on lui apporte des précisions en cours de route. Le workflow peut tourner seul, à heure fixe ou à chaque événement, et traiter du volume.
- **Oui → skill.** La personne pose des questions, fait des remarques, corrige le résultat, ou la tâche dépend de ce qui a été dit dans la conversation. Un workflow serait trop rigide. Le skill évite de répéter les mêmes consignes (charte, structure, règles métier) à chaque session.

Repères complémentaires :
- Un skill se justifie quand on recolle les mêmes instructions dans plusieurs conversations (à partir de trois fois environ) ou quand des critères doivent rester constants d'une fois sur l'autre.
- Un skill ne tourne pas seul : il lui faut une conversation ouverte, ou un agent qui l'utilise. Une tâche qui doit tourner sans personne relève d'un workflow.
- Les skills se partagent plus facilement que des prompts : une bibliothèque de skills hébergée sur GitHub permet à toute une équipe d'avoir la dernière version.

## Question 3 : workflow IA ou skill, ou agent ?

> Le processus demande-t-il de mobiliser plusieurs compétences différentes, et de prendre en cours de route des décisions qui changent son déroulement et son résultat final ?

- **Non → rester sur le workflow IA ou le skill.**
- **Oui → un agent est justifié.**

Pourquoi les options précédentes ne suffisent plus dans ce cas :
- un skill accomplit une tâche précise, alors qu'il faut ici enchaîner plusieurs tâches qui demandent des compétences différentes (savoir où chercher, comment formuler, quand passer la main à un humain) ;
- un workflow repose sur une logique « si X, alors Y » qui ne couvre pas tous les cas de figure d'un problème ouvert.

Un agent a besoin de quatre éléments : un objectif clair, un modèle qui raisonne, des outils, et du contexte. Il peut intégrer les options précédentes : des scripts pour l'exécution de code classique, des workflows pour les étapes fixes, des skills pour appliquer des règles métier au bon moment.

### Avant de conclure « agent »

Vérifier le coût :
- Quelle latence est acceptable ?
- Quel budget par exécution ? Un agent fait plusieurs appels au modèle pour une seule tâche.
- Quels garde-fous : limite d'étapes, validation humaine sur les actions sensibles, journal de ce qui a été fait ?
- Comment saura-t-on que l'agent fait mieux qu'un workflow ou un skill ? Prévoir quelques cas de test.

Si le gain n'est pas mesurable, redescendre d'un niveau.

Pour un agent qui doit tourner seul dans la durée, trois points à prévoir. Ce ne sont pas des conditions pour choisir un agent, mais ce qui le rend utile dans le temps :
- des données réunies au même endroit, pour que l'agent voie le parcours en entier ;
- un déclenchement régulier, sans intervention ;
- une mémoire de ses résultats d'une exécution à l'autre, pour refaire davantage de ce qui a marché.

En pratique, cela suppose souvent un pipeline de données, une base pour les stocker et du code hébergé dans le cloud. S'ils n'existent pas, les compter dans le coût de construction.

## Le mot « agent »

Il recouvre plusieurs choses. Préciser laquelle avant de conclure :
- **Un agent IA au sens de la question 3** : un système qui poursuit un objectif et décide lui-même de ses étapes et de ses outils.
- **Un sous-agent**, dans des outils comme Claude Code : un exécutant lancé depuis une conversation pour une tâche isolée (relecture, recherche, vérification), avec son propre contexte. Il démarre sans l'historique de la conversation et ne renvoie qu'un résumé. Il se justifie par l'isolement du contexte, le parallélisme ou des outils différents, pas par l'autonomie : la question 3 ne s'applique pas à lui.
- **Un scénario n8n, Make ou Zapier linéaire qui appelle un modèle** n'est pas un agent : c'est un workflow IA.

Quand préférer un sous-agent à un skill : la tâche n'a besoin que de ses entrées et d'une consigne, elle produirait beaucoup de matière qui encombrerait la conversation, ou elle doit être lancée en plusieurs exemplaires en parallèle. Pour traiter des centaines d'éléments, un workflow qui répartit le travail convient mieux que des sous-agents.

## Combiner les options

Les options se combinent souvent :
- un script fait la collecte et l'envoi, et un modèle ou un agent n'intervient que pour la partie qui demande du jugement ;
- un skill recueille le besoin et les précisions, puis confie des tâches autonomes à des sous-agents, en parallèle si besoin ;
- un agent s'appuie sur des skills pour appliquer des règles métier, et sur des scripts pour les calculs.

Quand une combinaison convient, la proposer et dire où passe la frontière entre les options.

## Autres briques à ne pas confondre

Ce ne sont pas des niveaux de décision : elles s'ajoutent à n'importe quelle option.
- **Instructions permanentes** : un fait ou une préférence stable (« on utilise tel outil ») se met dans les instructions ou les préférences de l'outil, pas dans un skill.
- **Connecteurs (MCP)** : ils donnent accès à un système en direct, pour lire des données ou agir.
- **Déclencheurs (hooks) et tâches planifiées** : ils lancent une action à un événement précis ou à heure fixe.

## Déroulé

1. Vérifier rapidement s'il faut automatiser (section « Avant tout »). Ne le signaler qu'en cas de doute.
2. Poser les trois questions dans l'ordre et y répondre à partir de la description de la tâche. S'arrêter à la première qui tranche.
3. Si la description ne permet pas de répondre à une question, la poser à la personne, avec au plus trois questions à la fois. Questions utiles : à quelle fréquence la tâche revient, si une personne doit intervenir en cours de route, d'où viennent les données, ce qui se passe quand le résultat est mauvais.
4. Si la réponse est « agent », vérifier le coût et ce qu'il faut prévoir.

## Format de la réponse

1. **Verdict** en une ligne : script classique, workflow IA, skill, agent, ou une combinaison.
2. **Les questions** : pour chaque question passée, la réponse et sa raison en une ou deux phrases.
3. **Pourquoi pas l'option plus simple, et pourquoi pas l'option plus complexe** : une phrase chacune, quand elles existent.
4. **Si agent ou combinaison** : ce qui manque avant de construire (données, hébergement, mémoire, garde-fous).
5. **Prochaine étape** : la plus petite version testable.

Rester sur la tâche décrite, sans liste de conseils génériques.

## Exemples

Un même sujet, les tickets d'un service client, selon le besoin :
- Résumer chaque semaine l'activité (tags les plus fréquents, opérateurs les plus actifs) : **script classique**. Le rapport a toujours la même forme et l'analyse se limite à compter.
- Analyser le contenu des tickets pour comprendre plus finement les problèmes récurrents : **workflow IA**. Il faut comprendre du texte, mais le parcours reste fixe.
- Faire une présentation à partir de ce rapport, en discutant le contenu et en corrigeant les diapositives : **skill**. La tâche est interactive, et le skill garde la charte et la structure d'une fois sur l'autre.
- Répondre aux tickets : **agent**. Il faut savoir où chercher la réponse, quel ton employer et quand passer la main à un humain, et chaque ticket peut mener à un déroulement différent.

Autres repères :
- Envoyer chaque lundi un export de base de données par email : script classique.
- Trier des emails entrants par catégorie, toutes les heures : workflow IA.
- Rédiger chaque semaine un compte rendu dans le même format, après quelques questions sur ce qui s'est passé : skill.
- Enquêter sur une panne dont on ignore la cause, en choisissant les journaux à lire et les tests à lancer selon ce qu'on trouve : agent.
- Surveiller des sources publiques pour repérer des opportunités : script pour la collecte, agent seulement pour la partie où le choix de ce qu'il faut creuser dépend des résultats.

## Pièges à signaler

- Automatiser un processus qu'on n'a pas compris, ou une tâche répétitive mais sans valeur.
- Utiliser l'IA pour un calcul ou un rapport de forme fixe, qu'un script ferait gratuitement et sans erreur.
- Appeler « agent » un enchaînement linéaire parce qu'il contient un modèle.
- Construire un workflow rigide pour une tâche où l'on précise et corrige sans cesse : c'est un skill.
- Écrire un skill pour une tâche qui doit tourner sans personne : c'est un workflow.
- Choisir un agent sans avoir vérifié que les décisions prises en cours de route changent vraiment le déroulement.
- Choisir un framework avant d'avoir choisi l'option.

## Sources

- Anthropic, « Building effective agents » : https://www.anthropic.com/research/building-effective-agents
- Les points à prévoir pour un agent qui tourne seul (données réunies, déclenchement régulier, mémoire des résultats) s'inspirent de Cody Schneider, invité du podcast de Greg Isenberg, « Marketing Agents Are Too Good Now » : https://www.youtube.com/watch?v=U2hogriGmEw
- sfeir.dev, « Skills vs Agents : comprendre le modèle d'exécution de Claude Code » : https://www.sfeir.dev/data/skills-vs-agents-comprendre-le-modele-dexecution-de-claude-code/
- Developers Digest, « Claude Agents vs Skills: Which One Do You Actually Need? » : https://www.developersdigest.tech/blog/claude-agents-vs-skills
- Vishal Srivastava, « Claude Skills vs Agents: Understanding the Difference » : https://medium.com/@vishal19102/claude-skills-vs-agents-understanding-the-difference-56fb46a7f3ea
- Dépôt « claude-code-best-practice » : https://github.com/shanraisshan/claude-code-best-practice
- Niharika Batra, « AI agents explained » : https://niharikabatra.substack.com/p/week-10-day-1-ai-agents-explained
