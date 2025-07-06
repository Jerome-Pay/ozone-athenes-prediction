# ozone-athenes-prediction
Projet de Master 2 - Modélisation et prédiction de la concentration d'ozone à Athènes à travers le temps

## Introduction  

Si l’ozone (O<sub>3</sub>) stratosphérique situé dans la haute atmosphère (aussi connu sous le nom de
couche d’ozone) nous protège des rayons ultraviolets émis par le soleil, l’ozone troposphérique
de la basse atmosphère est lui considéré comme un polluant secondaire.  
Il n’est pas émis directement dans l’atmosphère mais résulte d’une chimie complexe où interviennent d’autres
polluants primaires sous l’action du soleil [[1]](https://nap.nationalacademies.org/read/1889/chapter/1). Les principaux polluants qui contribuent à sa
formation sont :  

• les oxydes d’azote (NO(sub>x</sub>) émis par le trafic automobile, l’industrie et les centrales électriques  
• les composés organiques volatils (COV) émis par les solvants, les peintures, les vernis,
l’essence et certains produits d’hygiène ou de bricolage  

Par ailleurs, la chimie COV − NOx est complexe et le contrôle exact de l’O<sub>3</sub> reste discuté. Il
semble toutefois que la formation d’ozone soit favorisée par le soleil, la chaleur et l’absence de
vent. C’est pourquoi les pics de pollution à l’ozone sont plus fréquemment observés en été, lors
des journées ensoleillées et chaudes.  

Or, l’ozone joue un rôle central dans la formation et le devenir des produits chimiques toxiques
en suspension dans l’air, des hydrocarbures aromatiques polycycliques mutagènes et des particules fines [[2]](https://www.science.org/doi/10.1126/science.276.5315.1045). Dès lors, il pourrait être associé à une diminution de la fonction pulmonaire,
à l’aggravation des maladies respiratoires (asthme, bronchites chroniques) voire à un risque de
développer des maladies respiratoires et cardiovasculaires potentiellement mortelles selon qu’on
soit exposé à un pic de pollution ou sur le long terme [[3]](https://pubmed.ncbi.nlm.nih.gov/17435419/).  

Aussi la prévision de la concentration en ozone dans l’air relève-t-elle d’un enjeu sanitaire : on
observe en France certaines restrictions lorsque des pics de pollution sont attendus. Avoir un
aperçu à court terme (quelques jours par exemple) des concentrations en O<sub>3</sub> pourrait permettre
de mettre en place des actions préventives pour limiter sa formation (i.e. limiter la formation de
(NO<sub>x</sub>) et de (COV )). On pensera notamment aux restrictions sur la circulation des véhicules
motorisés qui ont été éprouvées et qui sont aujourd’hui bien connues mais souvent associées à
la pollution aux particules fines.

Dans le but de prévoir les futures concentrations en ozone à Athènes nous implémenterons des modèles d'apprentissage supervisée et nous évaluerons les performances de nos modèles grâces à un benchmark de référence ainsi que des métriques MAPE et RMSE. Nous allons prédire une année complète avec les données des 2 années précédentes. Dans le cas des modèles en ligne, nous faisons une prédiction de la conentration sur les prochaines 48 heures.

## Metadata

Les données sont disponibles sur [Zenodo](https://zenodo.org/records/11220965), un site internet open data.

Date (Date) : Date  
Date et heure de l’observation (AAAA-MM-JJ HH:MM:SS).  

NO2 (NO2) : quantitative continue  
Concentration de dioxyde d’azote dans l’atmosphère (µg.m−3
).  

O3 (O3) : quantitative continue  
Concentration d’ozone dans l’atmosphère (µg.m−3
).  

PM10 (PM10) : quantitative continue  
Concentration d’aérosols atmosphériques dont le diamètre maximal des particules est de 10
micromètres (µg.m−3
).  

PM2.5 (PM2.5) : quantitative continue  
Concentration d’aérosols atmosphériques d’un diamètre maximal de 2,5 micromètres (µg.m−3
).  

Latitude (Latitude) : quantitative continue / coordonnée géographique  
Coordonnée géographique (degrés).  

Longitude (Longitude) : quantitative continue / coordonnée géographique  
Coordonnée géographique (degrés)  

Nom de la station (station_name) : qualitative catégorielle  
Nom de la station de surveillance de la qualité de l’air.  

Vitesse du vent (U) (Wind-Speed (U)) : quantitative continue  
La composante U du vent est parallèle à l’axe des x (c’est-à-dire la longitude). Un vent U
positif vient de l’ouest et un vent U négatif vient de l’est (m.s−1
).  

Vitesse du vent (V) (Wind-Speed (U)) : quantitative continue  
La composante V du vent est parallèle à l’axe des y (c’est-à-dire la latitude). Un vent V positif
vient du sud et un vent V négatif vient du nord (m.s−1
).  

Point de rosée (Dewpoint Temp) : quantitative continue  
Point de température auquel l’air ne peut plus contenir d’eau (vapeur d’eau) provoquant le
phénomène de rosée (degrés Celcius).  

Température (Temp) : quantitative continue  
Température de l’air (degrés Celcius).  

Couvert végétal (Bas) (Vegitation (Low)) : quantitative continue  
Couverture végétale de haut niveau (unité de mesure inconnue : m2
, ha ; dans quel rayon
autour de la station ?).  

Couvert végétal (Haut) (Vegitation (High)) : quantitative continue  
Couverture végétale de faible niveau (unité de mesure inconnue : m2
, ha ; dans quel rayon
autour de la station ?).  

Température du sol (Soil Temp) : quantitative continue  
Température du sol (degrés Celcius).  

Précipitation totale (Total Percipitation) : quantitative continue  
Flux total équivalent eau (pluie ou neige) ayant atteint la surface du sol dans l’heure (m).  

Humidité (Relative Humidity) : quantitative continue  
Quantité réelle de vapeur d’eau dans l’air par rapport à la quantité totale de vapeur pouvant
exister dans l’air à sa température actuelle (%).  

Code (Code) : qualitative catégorielle  
Code de la station de surveillance de la qualité de l’air.  

id (id) : qualitative catégorielle  
ID de la station de surveillance de la qualité de l’air  

Afin d’étoffer notre jeu de données avec de nouvelles variables exogènes, nous avons décider
d’ajouter :  

• Hour : qualitative catégorielle  
Heure de la journée (on suspecte un effet de l’heure de la journée : chimie de l’air, activités
humaines).  

• Day : qualitative catégorielle  
Jour de la semaine (on suspecte un effet du jour de la semaine : activités humaines).  

• Month : qualitative catégorielle  
Mois de l’année (on suspecte un effet du mois de l’année : saisons, chimie de l’air, activités
humaines)  

• IsRaining : qualitative catégorielle  
1 s’il a plu au moins 0.5mm dans l’heure précédente, 0 sinon (plus qu’un effet quantité,
on suspecte des phénomènes de scavenging/washout/rainout : chimie de l’air).
On définit le rainout comme la capture des microparticules et gaz (notamment les polluants) par les gouttes de pluie à la formation des nuages (in-cloud scavenging).  
On définit le washout comme le "lessivage" de l’air par la pluie qui plaque au sol les
polluants (below-cloud scavenging) [[5]](https://www.sciencedirect.com/science/article/pii/S1352231015301850).  

• PublicHolidays : qualitative catégorielle  
1 si le jour est férié, 0 sinon (on suspecte un effet des jours fériés : activités humaines)  

• SchoolHolidays : qualitative catégorielle  
1 si le jour est une journée de vacances scolaires, 0 sinon (on suspecte un effet des vacances
scolaires : activités humaines).  

• YearPosition : quantitative continue  
Position dans l’année entre 0 et 1 (pour calculer les deux prochaines variables).  

• YearSeasonality  
Saisonnalité arbitraire sur l’année : cos(2π.Y earP osition).  

• DaySeasonality
Saisonnalité arbitraire sur la journée : cos(2π.365.Y earP osition).

• Fires
Score calculé à partir des incendies dans un rayon de 100km

## Résultats

Nous avons implémenté les modèles suivants :  
- Régression linéaire, régression liénaire Lasso, régression liénaire Ridge, régression liénaire Elastic Net, régression liénaire avec résidu XGBoost
- Arbre de décision, arbre de décision en ligne, forêt aléatoire, forêt aléatoir en ligne, XGBoost, XGBoost en ligne
- Perceptron multi-couches, RNN, LSTM, GRU, GRU en ligne
- Agrégation d'experts EG, agrégation d'experts EWA

Voici un tableau récapitulatif des performances des différents modèles :
![serie_temp_tableau_recap](https://github.com/user-attachments/assets/b4eb4a69-8bf0-408e-9afc-06666c53096f)

Enfin, un graphique comparant les prédictions de notre meilleur modèle (agrégation d'experts EG) avec les vraies données :
![serie_temp_MoE_EG_graph](https://github.com/user-attachments/assets/19b0b78a-63b9-4a82-b316-ba8266b89ade)

Force est de constater que les modèles basés sur les arbres et en particulier les modèles
d’ensemble sont les meilleurs dans notre cas.   Les mises à jour en ligne des modèles ont toujours permis d’améliorer les performances et ce de manière assez satisfaisante.  
Nous regrettons
toutefois de ne pas avoir pu exploiter les réseaux de neurones aussi bien que nous l’aurions
souhaité, notamment ceux qui sont particulièrement bien adapté aux séries temporelles (RNN,
LSTM et GRU).  Quant à l’agrégation d’expert, elle aurait sans doute gagné à avoir plus de
modèle avec des performances globales proches tout en étant diversifiés.
