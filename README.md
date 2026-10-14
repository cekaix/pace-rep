# PACE / REP — Lot 0

Double-cliquer Lancer-PC.cmd ou PACE-REP-PC.html. L’aperçu compilé fonctionne sans serveur. Pour le développement : npm run web. Pour recréer l’aperçu après modification : npx expo export --platform web puis node package-pc.cjs.

Expo + TypeScript, trois onglets, séances de musculation persistantes : catalogue de 15 exercices, recherche sans accents, filtre musculaire, charges/répétitions, échauffement/travail, préremplissage, validation, reprise de brouillon et historique. SQLite sur iPhone, stockage navigateur séparé sur PC. L’accueil peut afficher une démonstration explicitement fictive ; elle n’ajoute aucune séance au carnet. GPS, ActivityKit et iCloud automatique non intégrés.

Le prototype s’ouvre dans Expo Go sur l’iPhone de l’utilisateur. La nouvelle persistance SQLite et les capacités natives doivent encore être vérifiées sur cet appareil. Installation native autonome gratuite non encore validée. Le renouvellement de signature gratuit est limité à sept jours ; les capacités iCloud intégrées sont indisponibles avec la signature gratuite. Ne pas présenter Expo Go ou le bundle JavaScript exporté comme un .ipa autonome.

## Vérifications

`node tests/domain.test.cjs` : validations, calculs de volume, haltères, assistance et limites de semaine.
`node tests/persistence.test.cjs` : rechargement du stockage web, finalisation, doublons, échec quota et préservation de données corrompues.
`node tests/sqlite.test.cjs` : requêtes du repository sur une vraie base SQLite locale, fermeture/réouverture, dédoublonnage et rejet d’écriture invalide. Le test utilise SQLite de Node, pas le bridge Expo iPhone.
`node node_modules/typescript/bin/tsc --noEmit` et exports web/iOS réussis.

Limites du carnet : pas encore de timer, export/restauration utilisateur, suppression, catalogue personnalisé, réorganisation ou correction des séances terminées. Les charges validées sont des décimaux positifs ou nuls ; modifier une valeur dévalide la série. Les brouillons et séries invalides ne sont pas comptés dans les volumes hebdomadaires.

## Expo Go sur iPhone

Navigation mobile : onglets fixes en bas, zones sûres iOS respectées, marges et titres adaptés aux petits écrans. Le PC conserve la navigation latérale.

À partir du prochain lancement de Lancer-iPhone.cmd, la sortie Metro/console est enregistrée dans work/expo-runtime.log. Le flux de connexion n’est pas enregistré. Pour activer ce journal sur un serveur déjà ouvert, le fermer puis relancer le script une fois. Les anciennes erreurs non enregistrées ne peuvent pas être récupérées rétroactivement.

Lancer-iPhone.cmd connecte le PC au même compte Expo que l’iPhone, puis démarre Metro sur le réseau local. Le lanceur utilise expo-cli.cjs pour ouvrir le lien OAuth complet sans interpréter les esperluettes comme des commandes Windows. Aucune modification de la vérification OAuth ni des permissions Expo.

Vérifications du 14 octobre : TypeScript sans erreur, serveur Metro démarré, bundle iOS Hermes généré (582 modules). Ce bundle n’est pas une preuve de lancement sur l’iPhone. L’environnement de l’agent isole les serveurs locaux : le navigateur hôte ne peut pas atteindre leur retour OAuth. La connexion dans la session Windows de l’utilisateur reste à vérifier.
