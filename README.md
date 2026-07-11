# Visualisation 3D d'un Projecteur — CPGE

Outil interactif en 3D pour visualiser un **projecteur vectoriel** $p$ sur $E = \mathbb{R}^3$, dans le cadre du programme d'algèbre linéaire de CPGE (PCSI/PSI).

Un fichier HTML unique, sans build ni installation — tout tourne dans le navigateur.

## Contexte mathématique

Soit $E = G \oplus H$ une décomposition en somme directe, avec :
- $G$ : le plan horizontal $\{z = 0\}$ (image du projecteur)
- $H$ : une droite, éventuellement inclinée (noyau du projecteur)

Tout vecteur $x \in E$ se décompose de façon **unique** :

$$x = x_G + x_H, \quad x_G \in G, \; x_H \in H$$

Le projecteur $p$ associé à cette décomposition envoie $x$ sur sa composante dans $G$ :

$$p(x) = x_G, \qquad \ker(p) = H, \qquad \operatorname{Im}(p) = G$$

L'outil permet de faire varier $x$ et l'inclinaison de $H$ pour observer en temps réel comment $x_G$ et $x_H$ évoluent — y compris le cas dégénéré $p(x_H) = 0$ quand $x$ est pris directement sur $H$.

## Fonctionnalités

- **3 sliders** pour les coordonnées de $x = (x, y, z)$
- **1 slider** pour l'angle de $H$ par rapport au plan $G$ (30° à 150°, hors positions dégénérées)
- Caméra orbitale (clic-glisser pour tourner, molette pour zoomer)
- Affichage live des trois vecteurs : $x$ (cyan), $p(x) = x_G$ (rouge), $x_H$ (vert)
- Lignes pointillées reliant $x$ à ses deux composantes, pour visualiser le parallélogramme de décomposition
- Labels 3D sur les axes ($x$, $y$, $z$, $O$) pour s'orienter sans dépendre uniquement de la couleur
- Bouton de réinitialisation (valeurs + caméra)

## Utilisation

Ouvrir `visualisation_projecteur_3d.html` directement dans un navigateur (Chrome/Firefox/Edge récents). Une connexion internet est nécessaire au premier chargement pour récupérer les librairies via CDN.

Aucune installation, aucun serveur local requis.

## Stack technique

| Librairie | Rôle |
|---|---|
| [Three.js](https://threejs.org/) r128 + OrbitControls | Rendu 3D et contrôle caméra |
| [Tailwind CSS](https://tailwindcss.com/) (CDN) | Mise en page et thème sombre |
| [MathJax 3](https://www.mathjax.org/) | Rendu des formules $\LaTeX$ |
| [Font Awesome 6](https://fontawesome.com/) | Icônes |

Tout est chargé via CDN — pas de `node_modules`, pas de bundler.

## Structure

Fichier unique : `visualisation_projecteur_3d.html`
- `<head>` : imports CDN + config Tailwind/MathJax
- Panneau de contrôle (sidebar) : sliders, explication mathématique
- Zone de rendu 3D : canvas Three.js + overlays (légende, HUD des valeurs)
- Script d'initialisation : scène, caméra, géométries, boucle d'animation, gestion des sliders

## Limites connues

- Nécessite le WebGL (désactivé → écran de chargement bloqué)
- Angle de $H$ borné à [30°, 150°] pour éviter la division par une valeur proche de 0 dans le calcul de $\lambda$
