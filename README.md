# GrafiPro — déploiement Vercel (version corrigée et enrichie)

## Ce qui a changé dans cette version
- Suppression de toute référence codée en dur à "Kawsara" (titre, en-tête, valeurs par défaut).
- Écran d'accueil obligatoire au premier lancement (PC, tablette, mobile) : chaque atelier doit
  saisir son propre nom, téléphone et métier (Infographiste / Imprimeur / Sérigraphe / Autre)
  avant de pouvoir utiliser l'outil. Ces infos sont modifiables ensuite via les Paramètres (⚙).
- Les catégories de projets proposées s'adaptent désormais au métier choisi (ex. un sérigraphe
  voit "T-shirt, Broderie, DTF…", un imprimeur voit "Bâche, Calendrier, Carnet…").
- Devis et factures PDF repensés : bandeau coloré selon le métier de l'atelier, sous-titre métier,
  encart de mention automatique (validité du devis / relance de solde) si aucune note personnalisée
  n'est définie, mentions RCCM/NINEA en pied de page si renseignées.
- Messages WhatsApp réécrits dans un ton plus professionnel, différents pour un devis et pour une
  facture (avec relance de solde ou remerciement si soldée).
- **Nouveau : suivi des dépenses de production par projet** (tissu, encre DTF, sous-traitance…),
  avec calcul automatique du "Reste net en poche" (encaissé − dépenses) et de la "Marge totale
  prévue" (devis − dépenses), directement dans la fiche projet.
- **Nouveau : Bilan du jour** — un bouton sur le tableau de bord ouvre une fenêtre qui calcule tout
  ce qui a été encaissé et dépensé aujourd'hui (tous projets confondus), avec le détail ligne par
  ligne et le "reste net en poche" du jour.
- **Rappel doux intégré** : si de l'argent a été encaissé aujourd'hui mais qu'aucune dépense n'a
  encore été saisie, une bannière apparaît sur le tableau de bord pour le rappeler — voir la note
  ci-dessous sur pourquoi ce n'est pas une notification WhatsApp automatique.

## Déploiement en 2 minutes (sans CLI)
1. Va sur https://vercel.com/new
2. Choisis "Deploy without Git" / glisse-dépose le dossier contenant `index.html` et `vercel.json`
   (ou pousse ces 2 fichiers dans un repo GitHub puis "Import Project" sur Vercel)
3. Framework Preset : laisse "Other" — ne PAS choisir Next.js/React (ce n'est pas une app buildée)
4. Deploy → tu obtiens une URL `https://xxx.vercel.app`

## Déploiement via CLI
```bash
npm i -g vercel
cd grafipro
vercel --prod
```

## Important à savoir avant le test avec les ateliers
- Les données (clients, projets, paiements, paramètres de l'atelier) sont stockées **uniquement
  dans le navigateur** (localStorage) de chaque appareil. Rien n'est envoyé à un serveur.
  Deux ateliers différents, ou deux appareils différents pour le même atelier = deux bases de
  données isolées.
- Utilise les boutons **Exporter / Importer** (en haut à droite) pour sauvegarder ou transférer
  les données entre navigateurs/appareils en attendant l'intégration Supabase.
- Vider le cache / les données de navigation du navigateur = perte définitive des données non
  exportées.
- Chaque atelier qui teste le lien doit passer par l'écran d'accueil et renseigner **son propre**
  nom, téléphone et métier — c'est ce qui personnalise ses devis/factures/messages.
- Ce livrable reste un MVP de démonstration mono-poste, pas une version connectée à une base de
  données partagée.
