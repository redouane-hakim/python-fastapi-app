## Relevés sur actions/setup-node
- Créateur vérifié : oui
- Étoiles : 5K
- Dossier du code source : `src/`

**Q3.** `@main` pointe vers la dernière version de la branche : le code peut changer à tout
moment sans que je le sache (nouveau bug, rupture de compatibilité, ou code malveillant
en cas de compromission). `@v4` fige une version majeure, ce qui rend le workflow
reproductible et plus sûr. Encore mieux : épingler un SHA de commit complet, car un tag
peut lui aussi être déplacé.

**Q4.** Non. Le badge indique seulement que l'identité de l'éditeur a été vérifiée par
GitHub. Il ne garantit pas que le code est audité ni exempt de vulnérabilités, et un
compte vérifié peut être compromis.

**Q5.** (1) Lire le code source (action.yml, scripts, dépendances) pour vérifier qu'il ne
fait rien de suspect (envoi de secrets, appels réseau inattendus).
(2) Vérifier la réputation du projet (mainteneurs, activité, étoiles, issues ouvertes) et
épingler l'action sur un SHA de commit précis, avec des permissions minimales pour le
GITHUB_TOKEN.