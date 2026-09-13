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
