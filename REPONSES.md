# Réponses

## Q1

6 jobs (2 systèmes × 3 versions de Python). Les combinaisons sont :
- ubuntu-latest + 3.11
- ubuntu-latest + 3.12
- ubuntu-latest + 3.13
- windows-latest + 3.11
- windows-latest + 3.12
- windows-latest + 3.13

## Q2

6 jobs au total : on part de 6 jobs, on enlève windows-latest + 3.11 avec exclude (ça fait 5), puis on ajoute ubuntu-latest + 3.14 avec include (ça refait 6).

## Q3

Rien, le job 3.14 serait quand même exécuté. exclude est appliqué avant include et ne filtre que les combinaisons de la matrice de base. Comme 3.14 n'existe que dans include, l'exclusion ne correspond à rien et include l'ajoute ensuite normalement.

## Q4

Avec fail-fast: true, dès qu'un job échoue (ici les jobs Windows à cause du test cassé), GitHub annule les jobs encore en cours ou en attente. Certains jobs Ubuntu ont réussi, les jobs Windows ont échoué et les autres ont été annulés.

Avec fail-fast: false, tous les jobs vont jusqu'au bout : les jobs Ubuntu réussissent, les jobs Windows échouent et aucun n'est annulé.

Je choisirais true pour avoir un retour rapide et économiser des minutes de CI (par exemple sur une pull request). Je choisirais false quand je veux voir toutes les combinaisons qui échouent (par exemple pour tester la compatibilité avant une release).

## Q5

1. Limiter les coûts et le nombre de runners utilisés : sans limite, une grosse matrice peut utiliser tous les runners disponibles et bloquer les pipelines des autres équipes.
2. Protéger les ressources partagées (base de données, environnement de staging, API externe avec limite de requêtes) pour éviter les conflits et les tests instables.