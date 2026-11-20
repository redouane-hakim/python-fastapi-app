# Réponses TP 6

**Q1.** Quand une step écrit dans `$GITHUB_ENV`, elle ne fait qu'écrire dans un fichier.
Le runner lit ce fichier à la fin de la step et injecte les variables dans
l'environnement des steps suivantes. Le processus de la step courante a déjà démarré
avec son propre environnement, donc la variable n'y existe pas.

**Q2.** Dans `verify-env`, `$APP_NAME` s'affiche vide. Chaque job s'exécute sur un runner
distinct et neuf : `GITHUB_ENV` a donc une portée limitée au job (aux steps suivantes
du même job).

**Q3.** Avec `>`, le fichier est écrasé à chaque écriture : seul le dernier output écrit
subsiste, le premier est perdu. Il faut `>>` pour ajouter à la suite.

**Q4.** Chaque job tourne sur une machine différente, donc les variables de `GITHUB_ENV`
ne sont pas transmises. Les outputs de step déclarés dans `outputs:` du job sont
conservés par GitHub et exposés aux jobs dépendants via `needs.<job>.outputs.<nom>`.

**Q5.** Sans `needs: build`, `deploy` ne dépend plus de `build` : les deux jobs
démarrent en parallèle et `needs.build.outputs.full_version` est vide (ou inaccessible).
`needs` crée à la fois l'ordre d'exécution et l'accès aux outputs.