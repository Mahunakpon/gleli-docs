---
title: "Politique de confidentialité — Gléli"
lang: fr
---

# Politique de confidentialité — Gléli

**Dernière mise à jour : 5 août 2026**

---

## 1. Introduction

La présente politique de confidentialité décrit comment l'application mobile **Gléli**, dédiée à la gestion agricole (filière ananas/maraîchage) au Bénin, collecte, utilise, stocke et partage vos données personnelles.

**Responsable du traitement :** Biogaz Bénin Sarl, Maison GNANGA, en face de la Mosquée, Rue 115, Cotonou, Bénin, RB/COT/19B2460 — ci-après « Gléli », « nous ».

**Champ d'application :** cette politique couvre l'application mobile Gléli (Android/iOS), le backend serveur associé, et l'ensemble des services tiers utilisés pour faire fonctionner l'application (listés en détail à la section 7). Elle s'applique à tout utilisateur créant un compte sur Gléli, quel que soit son rôle (propriétaire d'exploitation, gestionnaire, technicien, commercial, membre invité).

Gléli est une application **hors ligne d'abord** : la plupart de vos données sont stockées localement sur votre appareil, puis synchronisées avec notre serveur lorsque vous disposez d'une connexion Internet, afin de permettre le travail entre plusieurs membres d'une même exploitation et la sauvegarde de vos données en cas de perte de l'appareil.

---

## 2. Données collectées

Nous décrivons ci-dessous, catégorie par catégorie, quelles données sont collectées, dans quel but, où elles sont stockées, et avec qui elles sont partagées.

### 2.1 Identité et contact

**Quoi :** nom, numéro de téléphone, adresse email, pays, date de naissance (facultative), intitulé de poste (facultatif), mot de passe, code PIN de déverrouillage.

**Finalité :** création et gestion de votre compte, authentification, communication avec vous (support, notifications).

**Stockage :** localement sur votre appareil (base de données chiffrée par le système d'exploitation) et sur notre serveur (base de données PostgreSQL), à l'exception du code PIN qui reste **exclusivement local à votre appareil** et n'est jamais transmis à notre serveur.

**Protection du mot de passe et du PIN :** votre mot de passe est protégé par une fonction de hachage cryptographique côté serveur (norme du secteur, bcrypt) ; il n'est jamais stocké ni transmis en clair. Votre code PIN est également haché avant stockage local et ne quitte jamais votre appareil.

**Partage :**
- Les autres membres de votre exploitation (collègues ayant un rôle de gestion) peuvent voir votre nom, téléphone et email dans l'outil de gestion des membres — ce n'est pas un partage avec un tiers externe, mais un partage fonctionnel interne à votre équipe.
- **EmailJS** (service tiers d'envoi d'emails) reçoit votre nom, téléphone et email lorsque : vous contactez le support, vous envoyez (avec votre confirmation explicite) un rapport de bug technique, ou vous recevez un code de vérification par email à l'inscription. Voir section 7.

### 2.2 Biométrie (empreinte digitale / reconnaissance faciale)

**Quoi :** utilisation de votre empreinte digitale ou de la reconnaissance faciale pour déverrouiller l'application, si votre appareil le propose et si vous l'activez.

**Finalité :** commodité de connexion, alternative au code PIN.

**Stockage et partage :** **aucune donnée biométrique n'est jamais collectée, stockée ou transmise par Gléli.** L'authentification biométrique est intégralement traitée par le système d'exploitation de votre appareil (via les API sécurisées d'Android/iOS — Secure Enclave ou Keystore) ; Gléli reçoit uniquement un résultat « succès » ou « échec » de cette vérification, jamais l'empreinte ou l'image faciale elle-même. Cette donnée ne transite donc jamais par nos serveurs ni par aucun service tiers.

### 2.3 Localisation (GPS)

**Quoi :** coordonnées GPS (latitude/longitude) ponctuelles, avec une précision « équilibrée » (de l'ordre de la centaine de mètres, pas une précision de navigation).

**Finalité :** géolocaliser vos parcelles agricoles, horodater et géolocaliser vos opérations culturales (semis, traitement, récolte…), authentifier la position lors d'une signature de visite technicien, et enregistrer le point de départ d'un transport de marchandise — utile notamment pour la traçabilité agricole et les vérifications de conformité (ex. détection d'une opération saisie hors de la zone de la parcelle concernée).

**Quand :** la localisation n'est demandée qu'au moment précis de ces actions (création/édition de parcelle, saisie d'une opération, signature d'une visite, départ d'un transport) — **jamais en tâche de fond, jamais de suivi continu.** L'application demande uniquement la permission de localisation « au premier plan » (foreground), jamais en arrière-plan.

**Stockage :** localement, puis synchronisée vers notre serveur (PostgreSQL) pour que les autres membres de votre exploitation disposent des mêmes informations et pour la sauvegarde de vos données.

**Partage :** aucun partage avec un tiers externe. L'écran Carte peut afficher votre position actuelle en direct (bouton « me centrer ») uniquement à l'écran, sans jamais l'enregistrer ni la transmettre.

### 2.4 Photos

**Quoi :** photographies de plantes (diagnostic de maladies), photographies de documents (dossiers réglementaires, factures…), et éventuellement des photos jointes à vos ventes ou visites techniques.

**Finalités et partage :**
- **Diagnostic de maladies des plantes par intelligence artificielle** : lorsque vous photographiez une plante pour un diagnostic, la photo est transmise à notre serveur puis à **Anthropic** (fournisseur du modèle d'intelligence artificielle Claude) pour analyse. Anthropic reçoit uniquement l'image transmise pour cette analyse — voir section 7 pour le détail. La photo, ainsi que le résultat du diagnostic, sont ensuite conservés (voir section 4) pour que vous puissiez consulter l'historique de vos diagnostics.
- **Documents de dossiers réglementaires** (photos ou PDF de certificats, factures, etc.) : stockés pour vous permettre de les retrouver et de les partager en cas de contrôle ou d'export de traçabilité.
- Toutes ces photos sont stockées sur votre appareil et téléversées vers **Cloudflare R2** (service de stockage de fichiers, voir section 7) afin d'être accessibles depuis vos autres appareils et sauvegardées.
- **Étiquettes de traçabilité** (QR code imprimable pour vos lots de récolte) : générées localement sur votre appareil, sans transmission à notre serveur. L'image du QR code lui-même est générée par un service tiers public (api.qrserver.com) à partir du code du lot — cette information n'est pas une donnée personnelle (c'est un identifiant de lot agricole), mais transite techniquement par ce service tiers au moment de l'affichage/impression.

Le diagnostic de maladies des plantes concerne la **santé végétale**, pas votre santé personnelle — il ne s'agit en aucun cas d'une donnée de santé humaine.

### 2.5 Audio (messages vocaux)

**Quoi :** messages vocaux que vous enregistrez et envoyez à d'autres utilisateurs via la messagerie intégrée de Gléli (conversations individuelles ou de groupe).

**Finalité :** communication entre collègues d'une même exploitation ou entre contacts Gléli.

**Stockage :** enregistrés localement sur votre appareil, puis téléversés vers **Cloudflare R2** afin d'être accessibles par le ou les destinataires du message. Les informations de conversation (participants, groupes, horodatage) sont synchronisées sur notre serveur.

**Partage :** aucun partage avec un tiers autre que Cloudflare R2 (hébergement technique du fichier, voir section 7) — le contenu de vos messages n'est utilisé par personne d'autre que les destinataires que vous avez choisis.

### 2.6 Données financières

**Quoi :** montants et informations liés à vos ventes, prêts, remboursements, et paiements (y compris le moyen de paiement choisi — Mobile Money, espèces, virement, chèque), ainsi que les informations nécessaires pour traiter un paiement Mobile Money via notre partenaire **CinetPay**, et vos achats de crédits de diagnostic IA via **RevenueCat**.

**Finalité :** gestion de votre activité commerciale (ventes, prêts), traitement des paiements et décaissements Mobile Money, et achat de crédits pour le diagnostic IA au-delà du quota gratuit.

**Stockage :**
- Vos ventes, prêts, remboursements et paiements sont stockés localement puis synchronisés sur notre serveur.
- Les transactions traitées via CinetPay (numéro de téléphone Mobile Money, montant, devise, nom du bénéficiaire) sont enregistrées sur notre serveur et répliquées localement sur les appareils des membres autorisés de votre exploitation.

**Partage :**
- **CinetPay** (prestataire de paiement Mobile Money) reçoit le numéro de téléphone Mobile Money, le montant, la devise et, pour un décaissement fournisseur, le nom du bénéficiaire. Gléli ne traite ni ne stocke aucune donnée de carte bancaire — seuls les paiements Mobile Money sont pris en charge.
- **RevenueCat** (gestion des achats intégrés) ne reçoit qu'un identifiant interne anonymisé associé à votre compte — jamais votre nom, téléphone ou email. Les informations de paiement elles-mêmes (carte bancaire, etc.) sont traitées directement par Google Play ou l'App Store, jamais par Gléli ni par RevenueCat.

### 2.7 Contacts du répertoire téléphonique

**Quoi :** avec votre autorisation explicite, Gléli peut lire les noms et numéros de téléphone de votre répertoire téléphonique pour vous aider à retrouver des connaissances déjà présentes sur Gléli.

**Finalité :** faciliter l'ajout de contacts/partenaires commerciaux déjà inscrits sur Gléli.

**Stockage et partage :** cette vérification est effectuée **entièrement sur votre appareil** : votre répertoire n'est jamais envoyé à notre serveur ni à un tiers. Si vous choisissez d'inviter un contact non inscrit, l'invitation est envoyée par SMS via l'application native de votre téléphone — pas via nos serveurs.

### 2.8 Diagnostics de maladies des plantes

Voir section 2.4 pour le détail du flux de la photo. Les données textuelles de diagnostic (nom de la maladie détectée, symptômes, traitements recommandés) sont stockées localement et sur notre serveur, associées à votre exploitation, afin que vous puissiez consulter l'historique de vos diagnostics. Il s'agit de données agronomiques (santé des cultures), non de données de santé humaine.

### 2.9 Identifiants techniques

**Quoi :** un identifiant unique généré pour votre appareil, des jetons de session (connexion) et de renouvellement de session, et des informations techniques envoyées en cas d'erreur applicative (journal d'erreur, nom de l'écran concerné).

**Finalité :** maintenir votre session connectée de façon sécurisée, détecter et corriger les bugs de l'application.

**Stockage :** les jetons de connexion sont stockés dans l'espace de stockage sécurisé fourni par le système d'exploitation de votre appareil (jamais en base de données classique). L'identifiant d'appareil et les jetons de renouvellement sont associés à votre compte sur notre serveur pour permettre le renouvellement sécurisé de votre session.

**Partage :** **Sentry** (service de surveillance des erreurs applicatives) reçoit les journaux d'erreurs techniques en cas de plantage de l'application, afin de nous permettre de corriger les bugs. Nous avons configuré Sentry pour qu'il ne reçoive jamais de mot de passe, de code PIN, de jeton de session ou d'autre secret, même en cas d'erreur — voir section 7.

---

## 3. Base légale du traitement

Selon la nature de la donnée et le contexte, nous nous appuyons sur les bases légales suivantes :

- **Consentement** : pour la création de votre compte, l'activation de l'authentification biométrique, l'accès à votre répertoire téléphonique, et l'envoi d'un rapport de bug technique (toujours proposé, jamais automatique).
- **Exécution du contrat** (les conditions d'utilisation de Gléli que vous acceptez à l'inscription) : pour l'ensemble des fonctionnalités métier nécessaires au fonctionnement de l'application — gestion de vos parcelles, opérations, stocks, ventes, transport, transformation, traçabilité, messagerie entre membres de votre exploitation.
- **Intérêt légitime** : pour la sécurité de l'application (journaux d'erreurs techniques, détection de fraude géographique lors de la saisie d'opérations) et l'amélioration du service.
- **Obligation légale/traçabilité réglementaire** : certaines données de traçabilité (lots de récolte, transformation, transport, autoévaluations de conformité) sont conservées pour répondre aux exigences de traçabilité agroalimentaire (ex. règlement UE 178/2002, référentiels HACCP/ISO 22000/GlobalG.A.P. que vous choisissez d'utiliser dans l'application).

---

## 4. Durée de conservation

Nous conservons vos données aussi longtemps que votre compte est actif, afin de vous fournir le service. Au-delà, la situation actuelle est la suivante — **nous préférons être transparents sur ce qui reste à améliorer plutôt que de prétendre à une politique de purge qui n'existe pas encore** :

- **Photos (diagnostic IA, documents de dossiers) et messages vocaux stockés sur Cloudflare R2** : à ce jour, **aucune purge automatique n'est en place** — ces fichiers sont conservés indéfiniment sur notre espace de stockage, y compris après suppression d'une parcelle ou d'un dossier associé. Il s'agit d'un point que nous nous engageons à améliorer (mise en place d'une politique de rétention et de nettoyage automatique).
- **Résultats de diagnostic IA (texte)** : conservés sans limite de durée dans notre base de données, pour vous permettre de consulter l'historique complet de vos diagnostics.
- **Données de compte, parcelles, opérations, ventes, transport, transformation, traçabilité** : conservées tant que votre compte est actif, et au-delà selon les durées de conservation légales applicables à la traçabilité agroalimentaire pour les documents à valeur probante.
- **Code PIN et données biométriques** : le PIN reste local à votre appareil et est supprimé si vous désinstallez l'application ; les données biométriques ne sont jamais stockées par Gléli (voir 2.2).
- **Sur demande de suppression de compte** (voir section 5) : nous traitons votre demande manuellement ; à ce jour, ce traitement n'inclut pas encore une purge automatisée et exhaustive de tous les fichiers associés (photos, audio) sur notre espace de stockage — un chantier de suppression automatisée complète est en cours de construction.

---

## 5. Vos droits

### 5.1 Droit d'accès et de portabilité

Vous pouvez à tout moment exporter une copie de vos données au format JSON directement depuis l'application (Profil → Support & données → « Exporter mes données (backup) »). Cet export inclut vos informations de compte, exploitations, parcelles, opérations, stocks, ventes et autres données métier associées à votre exploitation active.

### 5.2 Droit à la suppression (droit à l'oubli)

Vous pouvez demander la suppression de votre compte et de vos données personnelles depuis l'application (Profil → Support & données → « Supprimer mon compte »).

**Comment cela fonctionne aujourd'hui :** votre demande est transmise à notre équipe par email et **traitée manuellement**, généralement sous 30 jours. Nous vous informons honnêtement que ce processus n'est pas encore entièrement automatisé — nous travaillons à la mise en place d'un mécanisme de suppression automatique et complet (y compris les fichiers stockés sur Cloudflare R2). Si vous êtes le seul propriétaire d'une exploitation partagée avec d'autres membres, l'application vous recommande de désigner un nouveau responsable avant d'envoyer votre demande, afin que vos collègues ne perdent pas l'accès à l'exploitation.

La simple déconnexion de l'application n'entraîne aucune suppression de données — c'est un geste distinct de la suppression de compte.

### 5.3 Droit de rectification

Vous pouvez à tout moment corriger vos informations d'identité (nom, email, téléphone, pays, date de naissance, etc.) directement depuis votre profil dans l'application. Pour toute correction que vous ne pouvez pas effectuer vous-même, contactez-nous à mailingiec@gmail.com.

### 5.4 Autres demandes

Pour toute question relative à vos droits, ou pour toute demande de limitation ou d'opposition au traitement de vos données, contactez-nous à mailingiec@gmail.com (voir section 8).

---

## 6. Sécurité des données

Nous mettons en œuvre les mesures suivantes pour protéger vos données :

- **Chiffrement en transit** : les échanges entre l'application et notre serveur, ainsi qu'avec nos prestataires tiers, utilisent le protocole HTTPS (chiffrement TLS).
- **Biométrie jamais transmise** : comme détaillé en section 2.2, aucune donnée biométrique ne quitte jamais votre appareil — elle est traitée exclusivement par le système d'exploitation.
- **Jetons de session sécurisés** : vos jetons de connexion sont stockés dans l'espace de stockage sécurisé fourni par votre système d'exploitation (jamais en base de données classique accessible en clair), et renouvelés selon un mécanisme de rotation sécurisée.
- **Mots de passe protégés par hachage cryptographique** côté serveur (norme du secteur) — jamais stockés ni transmis en clair.
- **Code PIN** protégé par hachage cryptographique, strictement local à votre appareil, jamais transmis à notre serveur.
- **Cloisonnement par exploitation** : l'accès aux fichiers stockés (photos, documents, audio) est restreint aux membres autorisés de l'exploitation concernée, via des liens d'accès temporaires (valables 15 minutes) plutôt que des liens permanents.
- **Surveillance des erreurs applicatives** configurée pour exclure activement tout secret (mots de passe, codes PIN, jetons) de ce qui pourrait être transmis à notre outil de surveillance des erreurs (Sentry), même en cas de plantage de l'application.

Aucune méthode de transmission ou de stockage n'étant totalement infaillible, nous ne pouvons garantir une sécurité absolue, mais nous nous engageons à maintenir et améliorer continuellement ces protections.

---

## 7. Partage des données avec des tiers

Nous ne vendons jamais vos données personnelles. Nous partageons certaines données, dans la stricte mesure nécessaire, avec les prestataires suivants pour faire fonctionner Gléli :

| Service tiers | Rôle | Données reçues |
|---|---|---|
| **EmailJS** | Envoi d'emails (support, rapport de bug, code de vérification à l'inscription) | Nom, téléphone, email, contenu de votre message ou du rapport de bug |
| **Anthropic** (modèle Claude) | Analyse par intelligence artificielle des photos de plantes pour le diagnostic de maladies | La photo de la plante soumise pour diagnostic |
| **Cloudflare R2** | Stockage des fichiers (photos de diagnostic, documents de dossiers, messages vocaux) | Les fichiers eux-mêmes, associés à votre exploitation |
| **CinetPay** | Traitement des paiements et décaissements Mobile Money | Numéro de téléphone Mobile Money, montant, devise, nom du bénéficiaire (décaissement) |
| **RevenueCat** | Gestion des achats intégrés (crédits de diagnostic IA) | Un identifiant interne anonymisé de votre compte (jamais votre nom, téléphone ou email) |
| **Sentry** | Surveillance et diagnostic des erreurs applicatives | Journaux d'erreurs techniques, à l'exclusion de tout mot de passe, code PIN ou jeton de session |
| **Neon (PostgreSQL)** | Hébergement de notre base de données serveur | L'ensemble des données synchronisées décrites en section 2 (hébergement technique, pas d'utilisation propre par Neon) |
| **Google Play / Apple App Store** | Traitement des paiements pour les achats intégrés | Vos informations de paiement (carte bancaire, etc.) — jamais transmises à Gléli ni à RevenueCat |
| **api.qrserver.com** | Génération de l'image du QR code sur les étiquettes de traçabilité | Le code du lot de récolte (identifiant agricole, pas une donnée personnelle) |

Chacun de ces prestataires est tenu par ses propres conditions d'utilisation et politique de confidentialité, que nous vous invitons à consulter si vous le souhaitez. Nous sélectionnons nos prestataires en tenant compte de leurs engagements en matière de protection des données.

---

## 8. Contact

Pour toute question concernant cette politique de confidentialité ou le traitement de vos données personnelles, contactez-nous :

- **Email :** mailingiec@gmail.com
- **Depuis l'application :** Profil → Support & données → « Contacter le support Gléli »

Nous nous engageons à répondre à toute demande dans un délai raisonnable.

---

*Cette politique peut être mise à jour pour refléter l'évolution de l'application ou de la réglementation applicable. Toute modification substantielle vous sera communiquée.*

