# User/Personna

POC autonome pour observer ce qu’un agent découvre en utilisant un produit dans une situation de travail. Le point de départ est une recette de migration où l’agent a trouvé des écarts en prenant en main ses propres outils. Ce retour motive l’hypothèse. Sa généralisation reste à vérifier.

## Interface Tryout

Le [cadrage du POC](.travail/cadrage-poc.md) et le [brief d’intégration](.travail/brief-integration-maquette.md) décrivent l’interface React/Vite dans `frontend/` et ses commandes de lancement.

La [migration des fournisseurs et du chat](.travail/migration-providers-chat.md) décrit les connexions disponibles dans la maquette, le streaming du builder et la configuration locale.

## Première expérience

Une relève de support se fait dans un registre fictif après migration. Il faut retrouver le bon dossier, l’affecter à l’équipe Accès et y laisser la note attendue. L’agent dispose d’un compte limité à la file support, de quatre outils exécutés par le programme et d’un état qui évolue au fil de ses actions.

La mission d’usage confie la relève à l’agent. La mission de recette lui demande de contrôler les opérations de la relève. Les deux reçoivent le même dossier à traiter, les mêmes droits et le même budget. La variante défectueuse confirme une affectation qui reste inappliquée. La variante saine sert à observer les signalements erronés. Chaque exécution repart du même état initial. L’agent découvre les effets de la condition à travers ses outils.

Le parcours avec passation prolonge le travail des deux agents. La transmission aboutit si le dossier est visible dans la file du destinataire et porte une note. Une affectation confirmée sans changement d’équipe se traduit ici par un blocage dans la suite du travail.

## Exécuter

Avec Python 3.11 ou plus et une instance Ollama disposant d’un modèle capable d’appeler des outils.

```sh
python -m unittest
python experience.py --model gemma4:12b
python experience.py --model gemma4:12b --passation
```

Chaque commande d’expérience lance quatre passages, un par combinaison de mission et de condition. `--repetitions 3` relance chaque combinaison avec trois graines appariées. L’adresse vient de `OLLAMA_HOST` ou de `--host`. Le programme utilise uniquement des données fictives.

Chaque passage écrit un fichier JSON dans `runs/` avec les appels, leurs réponses, l’état final, la durée et le compte rendu. Le programme mesure si le travail a réellement produit l’affectation et la note attendues, ainsi que la transmission pour le parcours avec passation. Il relie l’accusé d’affectation à la lecture de l’état ou à la tentative de passation qui le contredit.

## Lire le résultat

Un signalement est étayé quand le compte rendu décrit un blocage observable dans la trace. Pour établir sa cause, l’agent peut consulter le dossier après l’action et constater l’équipe réellement enregistrée. Un signalement de défaut d’affectation sur un dossier correctement affecté constitue un faux positif. La lecture du récit reste humaine. Les traces donnent aussi le nombre d’appels, les modifications hors objectif et la durée de l’exécution.

## Premier essai

Huit passages avec `gemma4:12b` et la graine 42. Toutes les notes ont été enregistrées. Les quatre passages sur le registre sain ont affecté le dossier et les deux passations ont abouti.

Dans le parcours d’opérations sur le registre défectueux, les deux missions ont annoncé l’affectation. Le dossier est resté au Support général. Le mode usage a signalé la recherche infructueuse suivie d’une recherche par site. Avec la passation, les deux missions ont signalé le dossier absent de la file du destinataire. Les deux comptes rendus évoquent une synchronisation. L’examen de l’état final montre que le registre a gardé l’équipe d’origine.

La faisabilité du banc est établie sur un profil, un modèle et un parcours de travail. La valeur du mode usage sur d’autres défauts, l’effort de configuration d’un autre profil et le temps de revue restent à mesurer.
