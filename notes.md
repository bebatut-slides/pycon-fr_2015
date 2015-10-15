Notes pour la presentation
==========================

Bonjour,

Je m'appelle Bérénice et je vais vous présenter ce matin ce que j'ai appris depuis
le début de mon projet de développement d'un framework pour les biologistes.
    Le projet s'appelle ASaiM...

Avant de parler du développement du projet, je vais rapidement me présenter pour
vous mettre dans le contexte du projet.

# Présentation de moi

Formation en bioinformatique à l'INSA de Lyon

Thèse en bioinformatique à Lyon

- contribution à un projet en C/C++ : Aevol
- mais surtout développement de scripts en Python avec BioPython pour la gestion 
de fichiers, l'interface simple entre des programmes, le formattage des entrées-sorties

Actuellement, en post-doctorat à Clermont-Ferrand

- Travail sur un projet de plus grosse envergure, docn ASaiM

## Projet ASaiM

Projet de recherche porté par des équipes de biologistes mais aussi quelques 
partenaires informatiques
    Je suis la seule personne à temps plein sur ce projet et seule sur le 
    développement

Objectif : développer un environnement pour analyser les données issues du 
microbiote digestif

Microbiote digestif : ensemble des micro-organismes présent dans l'intestin
    Rôle très important dans la digestion. Considéré comme un organe à part 
    entière

Etude du microbiote : discipline récente --> métagénomique
    Principe : extraction de l'information génétique des micro-organisme, 
    séquençage et ensuite essai à partir des séquences de déterminer quels sont
    les organismes présent, ce qu'ils font et comment ils le font
    Travail bioinformatique dans le traitement des séquences

Complexité

- séquences courtes (100-500 caractères)
- forte variabilité des séquences, selon les organismes, ...
- bases de données de références incomplètes

    Besoin de nombreux traitements des séquences pour retirer l'information utile

Exemple de workflow pour trier les séquences selon leur type: seulement 1 seule
étape dans les traitements à effectuer

## Framework ASaiM

1ère étape du projet : développer un framework qui permet de générer des 
workflows pour analyser ces données en fonction des questions 

Principales contraintes :

- Generation de workflow pouvant contenir de nombreux outils
- Facilité d'utilisation par les biologistes, mais aussi pour l'automatisation
des tâches
- Flexibilité des outils, de l'enchainement des outils, des paramètres, ... pour
traiter les données spécifiques tout en conservant des sorties standardisées
- Facile à maintenir

1e approche testée : scripts Python simples pour le chainage
    Mais

    - pas flexible
    - pas facile à utiliser
    - pas facile à maintenir
    
2e approche testée : manager de workflow comme Luigi de Spotify, Airflow
de Airbnb, ...
    generation de workflows avec des dépendances entre les tâches
    Mais

    - pas toujours flexible dans le choix des outils
    - pas facile à documenter
    - SURTOUT : gros problème pour mettre en place

3e approche testée : approche maison avec 
    - un fichier de configuration pour décrire le workflow
    - des scripts Python pour exécuter le workflow

    Génération du fichier de configuration via une interface web

    Mais

    - pas flexible
    - pas facile à documenter
    - pas facile à maintenir
    --> NE PAS FAIRE du Maison

En essayant de toutes conception, remarque 1 chose : conviennent pas à mon pb
    Car 
        dépendances entre les tâches (telle tâche s'effectue après telle tâche)
    Or ca ne correspond pas au flux comme j'en ai besoin
    Lecture d'un post de Samuel Lampa sur les Workflow tool makers qui m'a permis
        de comprendre le pb de ces conceptions

Exemple précédent pour trier les séquences
    Boite coloré en fonction de l'outil
    les autres sont les données
    Boite verte peut être utilisée après la boite bleu ou après la boite bleu ici
    mais concrètement après une boite de n'importe quelle couleur
    Si on voulait utiliser des approches comme Airflow, toutes les tâches 
    pourraient être effectuées après n'importe quelle autre et on perd 
    l'avantage de Airflow
    Flux entre les données (entrées/sorties) plutôt qu'entre les tâches

Approche finalement adoptée : Galaxy
    Projet open-source basé sur Python
    Développé depuis 2005
    Communauté internationnale de développement
        Mailing-list
        Trello
    Pour rendre la bioinformatique accessible aux chercheurs n'ayant pas de 
    compétence en programmation informatique
        Interface web pour les "biologistes" avec de nombreux outils en ligne de
        commande
    Outils récupérables pour des instances locales via un store appelé Tool Shed

    Répond à la plupart des requis du framework
    Quelques réserves sur la documentation et la maintenabilité

Pour revenir à l'exemple de tri des séquences : une partie du workflow dans 
Galaxy
    Pour chaque outil, entrée en haut, sortie en bas et c'est ça qui importe

Pour framework ASaiM
    Configuration d'une instance avec tous les outils nécessaires pour le 
    traitement des données d'intérêt
    Développement de wrappers pour l'intégration des outils pas présent dans 
    le store (ou pas assez complets)
    Développement de scripts pour utiliser Galaxy et son API avec BioBlend

# Outils utilisés 

Pour beaucoup, ce sont des outils que je n'utilisais pas ou très peu

Gestion du code et à côté 
    Github + submodules

Documentation
    Sphinx + ReadTheDoc + Github
    Mise en place d'une doc facilement déployable et auquelle on peut contribuer 
    (Will)

Page web pour le projet, sa présentation, ...
    Jekyll + Github page

Gestion du projet
    Trello 
    Slack

# Appris avec ces 10 mois sur le projet 

Passer du temps à correctement définir la conception
    Besoin de temps pour mettre le doigt sur le pb dans la conception
    Pas de gestionnaire de workflow qui prenne en compte les dépendances entre 
    les entrées sorties plutôt que les dépendances entre les tâches

Ne pas préférer les solutions maisons et ne pas réinventer la roue
    Pas toujours facile dans le monde de la recherche qui n'est pas toujours
    ouvert sur les technologies utilisées dans le "privé" : besoin de faire
    cet effort là
    Peu de chance d'être le seul à avoir ce problème
    Regarder ce qui se fait
    Ouverture

S'intégration dans des communautés actives 
    Galaxy pour les développements au quotidien et l'intégration dans l'outil
    Clermont'ech, communauté Python : pour l'ouverture sur les technologies et 
    autres outils pour le développement

Passage du développement de scripts simple à un projet de cet envergure 
    Besoin de bonnes habitudes 
        Pas toujours bien inculquées en bioinformatique
    Besoin de bons outils pour faciliter la gestion et le développement
        Utilité de l'ouverture sur ce qui se fait
