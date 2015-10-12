Pycon-Fr
========

# Profil

Bioinformatics researcher currently working in the metagenomic field and 
pythonista, I write applications for scientists

# Abstract

## Title

ASaiM: lessons learned from developing a framework for biologists

## Description

In this talk, I am going to introduce how we created ASaiM (Auvergne Sequence 
Analysis of Intestinal Microbiota), a framework to process and analyze data from 
intestinal microbiota, designed for biologist. I will also cover what I have 
learnt developing such a software

## Abstract

With new technologies and reduced costs of DNA sequences, biological data are 
massively generated. Such data are complex and require multi-step processing. 
While numerous tools exist, most of them are only performing one task, not 
interoperable, not user-friendly, and so one... That is a big deal for biologists! 
We are building ASaiM (Auvergne Sequence Analysis of Intestinal Microbiota), a 
framework to process and analyze data from intestinal microbiota, designed for 
biologists: simple yet powerful! In this talk, I am going to introduce how we 
created ASaiM, why we chose Python, but also what I have learnt developing such 
a software

# Presentation (20 minutes)

Attention au public !!!

## Présentation de moi

Formation en bioinformatique à l'INSA de Lyon

Thèse en bioinformatique à Lyon

- contribution à un projet assez important : Aevol
- mais surtout développement de scripts en Python avec BioPython pour la gestion 
de fichiers, l'interface simple entre des programmes, le formattage des entrées-sorties

Post-doctorat à Clermont-Ferrand

- Projet de plus grosse envergure

## ASaiM project

Objectif : développer un environnement pour analyser les données issues du 
microbiote digestif

Microbiote digestif : ensemble des micro-organismes présent dans l'intestin

Pourquoi étudier le microbiote? organe à part entière

Quel type d'information pour l'étude? Des séquences ADN dont on ne connait pas à
quels organismes elles appartiennent et à quelle fonction elles correspondent

Pourquoi c'est dur?

- variabilité intra-specifique
- espèces inconnues dans les bases de données
- variabilité induite par le séquençage et autres

Besoin de nombreux traitements pour retirer l'information utile

## ASaiM framework

1ère étape du projet : développer un framework pour générer des workflows

Contraintes:

- Have standardized outputs which can be incorporated to the database 
- Be easy to use
– Be heavily documented
- Be flexible with the tools, the parameters, ... to process specific datasets 
while keeping standardized outputs
– Be executable on CRRI cluster and on local computer
– Be well written to be maintainable

Nombreux outils différents à interfacer

- SortMeRNA
- HUMAnN
- MetaPhlAn
- FastQ-Join
- PRINSEQ
- ...

Mettre un exemple de workflow

### Tested approaches

1. Scripts avec un début de formalisation
2. Airflow, luigi, [Cosmos](https://github.com/LPM-HMS/COSMOS-2.0)
3. Homemade approach
    1. un fichier de config qui décrit le workflow avec une interface Web pour
    générer ce fichier de config
    2. des scripts pour exécuter les workflows décrits dans le fichier de 
    configuration

Problème de toutes ses approches : dépendances entre les tâches (telle tâche 
s'effectue après telle tâche) (illustration de Luigi)
Or ce n'est pas le cas pour le type de workflow manager (début dans la 2e 
approche maison)

Difficile de mettre le doigt sur la difficulté jusqu'à la lecture du post
[Workflow tool makers: Allow defining data flow, not just task dependencies](http://bionics.it/posts/workflows-dataflow-not-task-deps)

4. Galaxy

Galaxy

- Création : 2005
- objectif: rendre la bioinformatique accessible aux chercheurs n'ayant pas de 
compétence en programmation informatique
- Goals
    - accessibilité
    - reproductibilité
    - transparence
- Objets : historique, workflows, datasets, pages   
- Open-source project
    - source code repositories (https://github.com/galaxyproject/ hosted by GitHub, Inc.)
- International development community
    - project management tools to track issues and feature requests (Trello) 
    - mailing lists
- Galaxy Tool Shed
    - public repository of tools and workflows
    - installation on individual Galaxy servers
- Plait aux biologistes
    - interface web 
- Divers
    - Gestion des jobs 
    - API + Cloudman

Galaxy: fonctionnement? Python derrière

### Concrétement

Développement de wrappers (scripts) pour les outils et l'intégration dans Galaxy
Développement de scripts qui appellent ces wrappers en dehors de Galaxy + API

### Utilisation de python

argparse, BioPython, gestion des fichiers, ...

### Outils utilisés 

Github + submodules

Sphinx + ReadTheDoc + Github : mise en place d'une doc facilement déployable et
auquelle on peut contribuer (Will)

Jekyll + Github page : pour la présentation du projet

### Plus généralement pour la gestion du projet

Trello 

Définition d'une roadmap (pas toujours évident en bioinfo)

## Conclusion

Appris depuis les 10 mois de ce projet

- Pas de gestionnaire de workflow qui prenne en compte les dépendances entre 
les entrées sorties plutôt que les dépendances entre les tâches
- Ne pas faire les trucs soi même et voir d'abord ce qui peut être proposé
    - Pas toujours facile dans le monde de la recherche qui n'est pas toujours
    ouvert sur les technologies utilisées dans le "privé" : besoin de faire
    cet effort là
- Intégration dans des communautés actives pour faciliter le déroulement du 
projet
    - Galaxy : pour les développements au quotidien et l'intégration dans l'outil
    - Clermont'ech, communauté Python : pour l'ouverture sur les technologies et 
    autres outils pour le développement
- Passage du développement de scripts unitaires à un projet de cet envergure 
    - Besoin de définir une roadmap (pas tjs évident en bioinfo)
    - Besoin de bons outils pour faciliter la gestion et le développement
- Pourquoi avoir choisi Python pour la base ? 
    - A bas Perl   
    - lib
    - habitudes
    - gestion des fichiers, ...
    - communauté
    - Limites?
