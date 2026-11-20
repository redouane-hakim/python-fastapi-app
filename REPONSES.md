# Réponses TP 7

**Q1.** `actions/checkout` a des valeurs par défaut pour tous ses paramètres (dépôt courant,
ref courante, token automatique). `setup-node` doit savoir quelle version de Node installer :
`node-version` est un choix que l'action ne peut pas deviner.

**Q2.** Chaque job s'exécute sur un runner distinct et vierge. `report.txt` est créé dans
l'espace de travail du job `build` et n'est pas commité dans le dépôt : il n'existe donc
pas dans `verify` (observé : `No such file or directory`). L'artefact permet de transférer
le fichier d'un job à l'autre.

**Q6.** Au démarrage d'un job, l'espace de travail est vide. Une action locale est un
fichier (`action.yml`) du dépôt : sans `checkout`, ce fichier n'est pas sur le runner et
GitHub ne peut pas le trouver (observé : `Can't find 'action.yml'`).

**Q7.** Dans un workflow classique, le shell par défaut est défini par le runner. Dans une
action composite, il n'y a pas de shell par défaut : GitHub impose de préciser
explicitement `shell:` pour chaque step `run`.

## Partie 4 : comparaison composite vs Docker
- Action composite (job `build`) : ~8 s (steps exécutées directement sur le runner).
- Action Docker (job `docker-hello`) : ~6 s (construction de l'image Alpine à chaque exécution).
Conclusion : sur ce run (#8), le job `docker-hello` a pris 6 s et le job `build` 8 s ; globalement, une action composite exécute ses étapes directement sur le runner, tandis qu'une action Docker construit une image conteneur (avec un léger surcoût de build d'image et un temps variable selon le cache).