# SEO technique

Le SEO technique regroupe les mécanismes qui permettent aux moteurs de recherche d'explorer, comprendre et indexer un site correctement. Cette note se concentre sur les fondations : comment un moteur découvre les pages, comment il décide de les indexer, et comment on peut orienter ce comportement.

## Exploration

L'exploration (crawling) est le processus par lequel un moteur de recherche parcourt les pages d'un site via des robots (crawlers). Un crawler part d'URLs connues, suit les liens internes et externes, et découvre progressivement de nouvelles pages.

Points clés :
- Le budget de crawl correspond à la capacité qu'un moteur alloue à l'exploration d'un site. Cette notion est surtout importante pour les sites volumineux ; elle est généralement beaucoup moins critique pour les petits sites.
- Une mauvaise architecture de liens internes peut empêcher certaines pages d'être découvertes.
- Les erreurs serveur (5xx) ou les temps de réponse lents réduisent l'efficacité du crawl.

## Indexation

L'indexation est l'étape où le moteur décide d'ajouter (ou non) une page explorée à son index — la base à partir de laquelle il génère les résultats de recherche. Une page peut être explorée sans être indexée.

Points clés :
- Une page peut être explicitement exclue de l'index via `noindex`. À l'inverse, `robots.txt` contrôle principalement son exploration et ne garantit pas sa non-indexation : une page bloquée au crawl peut malgré tout apparaître dans les résultats, généralement sans description.
- La Google Search Console permet de vérifier le statut d'indexation réel d'une page.
- Un contenu dupliqué ou trop proche d'une autre page du site peut être ignoré à l'indexation, même sans blocage explicite.

## Robots.txt

Le fichier `robots.txt` est placé à la racine d'un site et donne des directives aux crawlers sur les zones à explorer ou non. Ce n'est pas un mécanisme d'accès ou de sécurité : une page listée en `Disallow` reste accessible à qui en connaît l'URL, elle n'est simplement pas censée être explorée par les robots qui respectent le fichier.

Points clés :
- Syntaxe de base : `User-agent`, `Disallow`, `Allow`.
- Utile pour économiser le budget de crawl sur des zones sans intérêt SEO (pages d'administration, filtres, recherche interne).
- Ne garantit pas la non-indexation d'une page (voir section Indexation).

## Sitemap XML

Le sitemap XML est un fichier qui liste les URLs qu'un site souhaite voir explorées et indexées, avec des métadonnées optionnelles (date de dernière modification, fréquence de mise à jour, priorité).

Points clés :
- Il facilite la découverte de pages, surtout sur les sites récents ou peu liés en interne.
- Il ne force pas l'indexation, il ne fait qu'indiquer ce qui existe.
- Certaines métadonnées comme `<priority>` et `<changefreq>` sont ignorées par Google, malgré leur présence dans le protocole. `lastmod` en revanche peut être prise en compte, à condition qu'elle reflète une date de modification réelle et fiable.
- Il doit être tenu à jour et déclaré dans `robots.txt` ou soumis directement via Search Console.

## Canonicalisation

La canonicalisation indique à un moteur de recherche quelle URL est la version de référence lorsque plusieurs URLs mènent à un contenu identique ou très similaire.

Points clés :
- La balise `<link rel="canonical">` est une suggestion, pas une directive absolue : Google peut choisir une autre URL canonique s'il estime avoir de meilleures raisons de le faire.
- Les cas fréquents de contenu dupliqué : paramètres d'URL (tri, filtres), versions HTTP/HTTPS ou avec/sans `www`, pages accessibles via plusieurs chemins.
- Une mauvaise canonicalisation peut diluer l'autorité d'une page entre plusieurs URLs au lieu de la concentrer sur une seule.

## Architecture et maillage interne

L'architecture d'un site désigne la façon dont ses pages sont organisées et reliées entre elles. Le maillage interne — les liens d'une page vers une autre au sein du même site — en est le mécanisme concret : il facilite la découverte des pages par les crawlers et contribue à la distribution des signaux d'importance entre elles.

Points clés :
- Une page profonde (accessible seulement après plusieurs clics depuis la page d'accueil) peut être plus difficile à découvrir et reçoit généralement moins de signaux internes qu'une page proche de la racine.
- Les liens internes doivent utiliser des ancres (le texte cliquable) descriptives : elles aident les moteurs à comprendre le sujet de la page cible, contrairement à des ancres génériques comme « cliquez ici ».
- Une organisation thématique cohérente, parfois appelée structure en silo, peut aider les moteurs à comprendre les relations entre les pages et les sujets traités sur le site.
- Les pages orphelines — non liées depuis aucune autre page du site — sont plus difficiles à découvrir par le maillage interne. Un sitemap peut faciliter leur découverte, mais ne remplace pas des liens internes pertinents.
- Le nombre de liens internes doit rester cohérent avec le contenu et les besoins de navigation. Google ne fixe pas de limite stricte : l'objectif est avant tout de proposer des liens utiles et pertinents aux utilisateurs et aux moteurs.

## Codes HTTP et redirections

Le code de statut HTTP renvoyé par le serveur indique aux navigateurs comme aux moteurs de recherche l'état de la ressource demandée. Une mauvaise gestion de ces codes peut perturber l'exploration et l'indexation d'un site.

Points clés :
- `200 OK` indique qu'une ressource a été trouvée et peut être correctement récupérée. C'est généralement le code attendu pour une page destinée à être indexée.
- `301` (redirection permanente) indique que l'URL a été déplacée de manière durable. Il permet aux moteurs de transférer les signaux associés à l'ancienne URL vers la nouvelle et constitue le choix approprié pour une migration ou un changement d'URL permanent.
- `302` (redirection temporaire) indique que le déplacement est provisoire. Lorsqu'une redirection est réellement temporaire, elle permet aux moteurs de conserver l'ancienne URL comme référence potentielle. Utiliser un `302` pour un déplacement permanent peut ralentir la prise en compte de la nouvelle URL.
- `404` (page non trouvée) est normal lorsqu'une ressource n'existe plus. Lorsqu'une page a été définitivement supprimée sans équivalent pertinent, un `404` peut être préférable à une redirection artificielle vers une autre page.
- Les chaînes de redirections (plusieurs redirections successives avant d'atteindre la destination finale) ajoutent des étapes inutiles et peuvent ralentir l'exploration. Il est préférable de rediriger directement l'ancienne URL vers la destination finale.
- Un code `200` renvoyé pour une page qui n'existe pas réellement ou dont le contenu est absent peut produire un « soft 404 ». Les moteurs peuvent alors considérer la page comme inexistante malgré son statut HTTP `200`.

- ## Balises HTML et structure du document

Certaines balises HTML aident les moteurs de recherche à comprendre le contenu et la structure d'une page, au-delà de son seul texte visible.

Points clés :
- La balise `<title>` est un signal important pour comprendre le sujet de la page. Elle est aussi généralement utilisée comme titre cliquable dans les résultats de recherche, bien que Google puisse la reformuler s'il estime qu'une autre formulation est plus pertinente.
- La `meta description` n'a pas d'effet direct connu sur le classement, mais peut influencer l'extrait affiché sous le titre dans les résultats. Google peut également générer cet extrait à partir du contenu de la page s'il estime qu'il est plus pertinent.
- La hiérarchie des titres (`<h1>` à `<h6>`) contribue à structurer le contenu de façon logique. Utiliser un `<h1>` principal par page reste une pratique courante, mais Google n'impose pas de règle stricte sur le nombre de balises `<h1>`.
- L'attribut `alt` d'une image fournit une description textuelle utile aux technologies d'assistance et aide également les moteurs à comprendre le contenu de l'image, notamment pour la recherche d'images.
- L'attribut `lang` (par exemple `<html lang="fr">`) indique la langue du document et améliore notamment son interprétation par les technologies d'assistance. Il fournit également un signal sur la langue du contenu, mais ne constitue pas à lui seul un mécanisme de ciblage international.
- Le contenu masqué ou rendu difficilement accessible à l'utilisateur doit être utilisé avec cohérence. Cacher du contenu dans le seul but de manipuler les moteurs de recherche peut être considéré comme une pratique abusive, tandis que certains contenus masqués pour des raisons d'interface ou d'accessibilité restent parfaitement légitimes.

- ## Pagination et gestion des paramètres d'URL

De nombreux sites génèrent des variantes d'une même page via des paramètres d'URL (tri, filtres, suivi de campagne) ou via une pagination (listes de résultats réparties sur plusieurs pages). Ces mécanismes peuvent créer un grand nombre d'URLs proches ou dupliquées s'ils ne sont pas gérés avec attention.

Points clés :
- Les paramètres d'URL utilisés pour le tri ou le filtrage (par exemple `?tri=prix`) peuvent générer des variantes très proches de la page d'origine. Selon leur utilité et leur contenu, ces URLs peuvent être indexées séparément, canonisées vers une autre URL ou rendues moins accessibles au crawl.
- Les paramètres de suivi comme `?utm_source=...` n'apportent généralement aucune valeur propre en matière de recherche. Une URL canonique sans paramètre peut indiquer la version de référence, tout en conservant les paramètres nécessaires au suivi des campagnes.
- Pour une série de pages paginées (page 1, 2, 3...), chaque page peut être explorée et indexée individuellement lorsqu'elle possède un contenu propre et une valeur suffisante. Google ne prend plus en charge les signaux `rel="next"` et `rel="prev"` pour l'indexation.
- Une page uniquement accessible après plusieurs niveaux de pagination peut être plus difficile à découvrir si elle n'est pas suffisamment reliée par des liens internes. La pagination doit donc permettre aux moteurs d'atteindre les pages importantes par des liens HTML accessibles.
- `robots.txt` peut limiter l'exploration de certaines variantes d'URL, mais il doit être utilisé avec prudence : bloquer une URL empêche principalement son exploration et ne constitue pas une méthode fiable pour empêcher son indexation.
- Google Search Console ne propose plus le traitement général des paramètres d'URL qui permettait auparavant de déclarer leur comportement. La gestion doit donc principalement reposer sur l'architecture du site, les liens internes, la canonicalisation et, lorsque c'est pertinent, les règles de crawl.

- ## Internationalisation (hreflang)

Certains sites proposent des versions d'une même page adaptées à différentes langues ou zones géographiques. L'attribut `hreflang` permet d'indiquer aux moteurs de recherche les relations entre ces différentes versions et de signaler quelle version linguistique ou régionale est destinée à quel public.

Points clés :
- `hreflang` se déclare soit dans les balises `<link>` du `<head>` de chaque page, soit dans le sitemap XML, soit via l'en-tête HTTP `Link` (utile notamment pour les fichiers non HTML comme les PDF).
- Chaque page d'un ensemble de versions linguistiques doit référencer les autres versions, y compris elle-même (référence dite auto-référentielle). Des annotations incomplètes ou incohérentes peuvent empêcher certaines relations d'être prises en compte.
- Le format attendu combine un code de langue (ISO 639-1) et, optionnellement, un code de région (ISO 3166-1 Alpha 2), par exemple `fr-FR` pour le français de France ou `fr-CA` pour le français du Canada.
- La valeur spéciale `x-default` permet de désigner la version à utiliser lorsqu'aucune autre version linguistique ou régionale ne correspond.
- `hreflang` est un signal indiquant une relation entre des pages équivalentes, mais ne garantit pas à lui seul leur classement dans chaque marché. Il doit correspondre à des versions réellement adaptées à chaque langue ou région.
- Des annotations `hreflang` incohérentes, par exemple lorsqu'une page A référence B sans que B ne référence A, peuvent empêcher Google de reconnaître correctement la relation entre les deux versions.

- ## Performance web / Core Web Vitals

Les Core Web Vitals sont un ensemble de métriques définies par Google pour mesurer des aspects essentiels de l'expérience utilisateur : performance de chargement, réactivité et stabilité visuelle. Ils constituent un ensemble de signaux utilisés dans l'évaluation de l'expérience de page.

Points clés :
- LCP (Largest Contentful Paint) mesure le temps nécessaire pour afficher le plus grand élément de contenu visible dans la fenêtre d'affichage. Un LCP inférieur ou égal à 2,5 secondes est considéré comme une bonne performance.
- INP (Interaction to Next Paint) mesure la réactivité d'une page aux interactions de l'utilisateur sur l'ensemble de sa visite. Il a remplacé le FID (First Input Delay) comme Core Web Vital en mars 2024. Un INP inférieur ou égal à 200 millisecondes est considéré comme une bonne performance.
- CLS (Cumulative Layout Shift) mesure la stabilité visuelle d'une page en quantifiant les déplacements inattendus de son contenu. Un score inférieur ou égal à 0,1 est considéré comme une bonne performance.
- Les Core Web Vitals peuvent être mesurés à partir de données réelles d'utilisateurs (« données de terrain »), notamment via le Chrome User Experience Report (CrUX). Les données de terrain et les tests en laboratoire peuvent produire des résultats différents, car ils ne mesurent pas les mêmes conditions d'utilisation.
- Les Core Web Vitals constituent un signal parmi d'autres dans l'évaluation de l'expérience de page. Une bonne performance technique ne compense pas nécessairement un contenu moins pertinent ou moins utile.
- PageSpeed Insights permet d'obtenir des données de terrain et de laboratoire pour une URL. Le rapport « Signaux Web essentiels » de Google Search Console permet quant à lui de suivre les performances des groupes de pages du site à partir des données disponibles.

