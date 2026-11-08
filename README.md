# agent-ou-script

Un skill pour Claude qui aide à choisir le bon niveau d'automatisation pour une tâche : script classique, workflow IA, skill ou agent IA.

Beaucoup de projets présentés comme des « agents » seraient plus simples, moins chers et plus fiables sous la forme d'un script ou d'un workflow. À l'inverse, certaines tâches gagnent vraiment à être confiées à un agent. Ce skill pose les bonnes questions, dans le bon ordre, et donne un verdict argumenté avec une première étape concrète.

## Installation

### Sur claude.ai ou dans l'application Claude pour ordinateur

1. Téléchargez le fichier [agent-ou-script.zip](https://github.com/moniqueb91/agent-ou-script/releases/latest/download/agent-ou-script.zip). Ne le décompressez pas.
2. Ouvrez la page des skills : [claude.ai/customize/skills](https://claude.ai/customize/skills).
3. Cliquez sur **+**, puis sur **Create skill**, puis sur **Upload a skill**.
4. Sélectionnez le fichier `agent-ou-script.zip` que vous venez de télécharger.
5. Vérifiez que le skill apparaît dans la liste et qu'il est activé.

Pour que l'option d'ajout apparaisse, la création de fichiers doit être activée dans **Paramètres > Capacités** (option « Create and edit files », ou « Code execution and file creation » selon la version). Sur un compte Team ou Enterprise, l'administrateur doit aussi autoriser l'ajout de skills.

N'utilisez pas le bouton **Code > Download ZIP** de GitHub : le fichier obtenu n'a pas la structure attendue par Claude et l'ajout échouera.

### Dans Claude Code

Dans un terminal :

```
curl -L -o agent-ou-script.zip https://github.com/moniqueb91/agent-ou-script/releases/latest/download/agent-ou-script.zip
unzip agent-ou-script.zip -d ~/.claude/skills/
```

Le skill est alors disponible dans tous vos projets à partir de la prochaine session. Pour le réserver à un projet et le partager avec votre équipe, remplacez `~/.claude/skills/` par `.claude/skills/` à la racine du projet.

### Vérifier que le skill fonctionne

Dans une nouvelle conversation, posez une question comme : « Est-ce que j'ai besoin d'un agent pour répondre automatiquement à nos tickets support ? ». Claude doit passer les trois questions décrites ci-dessous et donner un verdict.

## Ce que fait le skill

Quand vous décrivez une tâche à automatiser, Claude :

1. vérifie d'abord qu'elle mérite d'être automatisée (processus bien compris, tâche répétitive et utile) ;
2. passe trois questions dans l'ordre, et s'arrête à la première qui tranche ;
3. vous pose des questions si votre description ne suffit pas pour répondre ;
4. vérifie le coût et les garde-fous si un agent est envisagé ;
5. propose une combinaison d'options quand elle convient mieux qu'une seule ;
6. répond avec un verdict, ses raisons, et une prochaine étape.

Les trois questions :

| Question | Si oui | Si non |
|---|---|---|
| 1. La tâche peut-elle être entièrement exécutée avec du code classique ? | Script classique | Passer à la question 2 |
| 2. A-t-elle besoin de contexte, d'interaction ou de clarification de votre part ? | Skill | Workflow IA |
| 3. Demande-t-elle plusieurs compétences différentes, et des décisions en cours de route qui changent son déroulement et son résultat ? | Agent IA | Rester sur le workflow IA ou le skill |

## Exemples de demandes

- « Chaque lundi j'exporte des données de ma base et je les envoie par email. Est-ce que je devrais construire un agent ? »
- « Je veux automatiser les réponses à nos tickets support. Mon scénario Make suffit, ou il me faut un agent ? »
- « Workflow ou skill pour produire mes présentations mensuelles ? »
- « Do I need an agent or a script for this? »

## Contenu du dépôt

```
README.md                 ce fichier
LICENSE                   la licence MIT
agent-ou-script/          le dossier du skill
├── SKILL.md              les instructions lues par Claude
└── evals/                quatre cas de test
```

## Tester le skill

Le dossier `evals/` contient quatre demandes réalistes, chacune avec la réponse attendue et des critères vérifiables :

- `export-sql-hebdo-script-fixe` : une tâche aux règles fixes, qui doit aboutir à un script classique ;
- `relecture-parallele-sous-agents` : une relecture sous trois angles qui demande une précision de votre part, qui doit aboutir à un skill lançant des sous-agents en parallèle ;
- `reponse-tickets-agent` : la réponse automatique à des tickets support, qui doit aboutir à un agent avec des garde-fous ;
- `veille-prospects-combinaison` : une veille de prospects, qui doit aboutir à une combinaison d'un script et d'un agent.

Avec Claude Code (version 2.1.269 ou plus récente) :

```
git clone https://github.com/moniqueb91/agent-ou-script.git
cd agent-ou-script/agent-ou-script
claude plugin eval .
```

La commande fait tourner chaque cas avec et sans le skill, puis écrit un rapport dans `evals/results/`. Ce sont de vrais appels au modèle, donc facturés.

Sans Claude Code, vous pouvez coller la demande d'un fichier `prompt.md` dans une conversation, avec puis sans le skill, et comparer les réponses aux critères du dossier `graders/`.

## Sources

- Anthropic, « Building effective agents » : https://www.anthropic.com/research/building-effective-agents
- Les points à prévoir pour un agent qui tourne seul s'inspirent de Cody Schneider, invité du podcast de Greg Isenberg, « Marketing Agents Are Too Good Now » : https://www.youtube.com/watch?v=U2hogriGmEw
- sfeir.dev, « Skills vs Agents : comprendre le modèle d'exécution de Claude Code » : https://www.sfeir.dev/data/skills-vs-agents-comprendre-le-modele-dexecution-de-claude-code/
- Developers Digest, « Claude Agents vs Skills: Which One Do You Actually Need? » : https://www.developersdigest.tech/blog/claude-agents-vs-skills
- Vishal Srivastava, « Claude Skills vs Agents: Understanding the Difference » : https://medium.com/@vishal19102/claude-skills-vs-agents-understanding-the-difference-56fb46a7f3ea
- Dépôt « claude-code-best-practice » : https://github.com/shanraisshan/claude-code-best-practice
- Niharika Batra, « AI agents explained » : https://niharikabatra.substack.com/p/week-10-day-1-ai-agents-explained

## Autrice et licence

Créé par Monique Bayama. Distribué sous licence MIT : vous pouvez réutiliser, modifier et partager ce skill librement, à condition de conserver la mention de copyright. Voir le fichier `LICENSE`.
