---
title: Histoire de France — Parcours complet
description: Un quiz transversal assemblé depuis trois modules indépendants (Clovis & les Francs, Révolution française, Napoléon). Démontre la fonctionnalité d'import de sous-quiz.
lang: fr
tags: [histoire, france, compilation, import]
domain: academic
passing_score: 0.6
scoring:
  correct: 1
  incorrect: 0
---

# Histoire de France — Parcours complet

Ce quiz agrège trois modules indépendants pour former un parcours chronologique sur l'histoire de France. Chaque section provient d'un fichier `.quiz.md` distinct importé via la directive `!import`.

!import ./clovis.quiz.md

!import ./revolution-francaise.quiz.md

!import ./napoleon.quiz.md
