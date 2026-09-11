# SPOTLIGHT — Studio de Création Signature

Site web immersif et vitrine haut de gamme pour **SPOTLIGHT**, studio de création indépendant spécialisé en **Identité Visuelle, Impression d'Exception, UI/UX Digital et Packaging**.

---

## 🎨 Charte Graphique & Design Tokens

Tous les éléments et ajouts futurs respectent scrupuleusement la charte graphique :

- **Couleurs Principales** :
  - `onyx` : `#0A0B0E` (Fond d'écran et contraste absolu)
  - `graphite` : `#14171F` (Cartes de projets, panneaux, modales)
  - `coal` : `#0F1116` (Contrastes d'ambiance et séparations)
  - `bone` : `#F4F2ED` (Typographie principale et accents lumineux)
  - `gold` : `#FFD026` (Couleur signature dorée, états actifs, lueurs)
- **Typographies** :
  - **Syne** (`font-syne`) : Titres monumentaux en majuscules, impact visuel brutaliste raffiné.
  - **Plus Jakarta Sans** (`font-jak`) : Textes de lecture, formulaires, labels et micro-copies.
  - **Instrument Serif** (`font-serif` italique) : Accents poétiques et artisanaux (*« vision »*, *« respire »*, *« orfèvre »*).
- **Textures & Finitions** :
  - Grain papier discret (`.grain` à 3.5% d'opacité).
  - *Glassmorphism* avec `backdrop-filter: blur(26px) saturate(150%)`.
  - Spots lumineux interactifs réagissant au curseur (`.spot`).

---

## 🧭 Navigation & Mega Menu Gauche (Responsive)

1. **Bouton Hamburger** :
   - **Mobile & Tablette** : Positionné à gauche dans le header supérieur, à côté du logo Spotlight.
   - **Desktop (Grand écran)** : Accessible via le bouton dédié **« Mega Menu · Catégories »** en haut du rail gauche flottant.
   - **Raccourci Clavier** : Appuyez sur la touche `M` (en dehors des champs de texte) pour ouvrir/fermer le Mega Menu instantanément.
2. **Left Mega Menu Drawer** :
   - Panneau coulissant depuis la gauche avec fond sombre flouté.
   - **Catégories & Pôles de Compétences** :
     - `01 · BRANDING` : Identité Visuelle, Logos, Monogrammes, Chartes 60p+, Typographie vectorielle.
     - `02 · PRINT` : Impression d'Orfèvre, Dorure or 24k, Gaufrage, Papiers 600g+, Reliure suisse.
     - `03 · DIGITAL` : UI/UX & Web Moderne, Design Systems Figma, SaaS, Accessibilité WCAG AA.
     - `04 · PACKAGING` : Volumes structurés, Dielines 3D, Packaging luxe, Merch & Apparel streetwear.
   - **Études de cas directes** (Aurora Labs, Kora Streetwear, Monolith, Flux Inc.) ouvrant les fiches projets détaillées.
   - **Plan du site & Contact direct** (WhatsApp instantané, statut des créneaux Q1 2026, horloge temps réel de Luanda GMT+1).
3. **Recherche Universelle** :
   - Accessible via le bouton de recherche ou le raccourci `⌘K` / `Ctrl+K` / `/`.

---

## ⚡ Connexion avec Supabase (Prête à l'emploi)

Le site est d'ores et déjà préparé pour enregistrer les briefs directement dans Supabase.

### 1. Script CDN à insérer dans `<head>` (quand vous connecterez vos clés)
```html
<script src="https://cdn.jsdelivr.net/npm/@supabase/supabase-js@2"></script>
```

### 2. Configuration dans `index.html`
Modifiez l'objet `window.SPOTLIGHT_CONFIG` en haut du fichier :
```javascript
window.SPOTLIGHT_CONFIG = {
  WHATSAPP_NUMBER: '244900000000', // Votre numéro WhatsApp
  STUDIO_EMAIL:    'studio@spotlight.design',
  STUDIO_LOCATION: 'Luanda, Angola — International',
  
  // Activer Supabase :
  ENABLE_SUPABASE:   true,
  SUPABASE_URL:      'https://VOTRE_PROJET.supabase.co',
  SUPABASE_ANON_KEY: 'VOTRE_CLE_PUBLIQUE_ANON'
};

// Initialisation :
if (window.SPOTLIGHT_CONFIG.ENABLE_SUPABASE && window.supabase) {
  window.supabaseClient = supabase.createClient(
    window.SPOTLIGHT_CONFIG.SUPABASE_URL,
    window.SPOTLIGHT_CONFIG.SUPABASE_ANON_KEY
  );
}
```

### 3. Schéma SQL de la table `briefs` dans Supabase
Exécutez ce script dans l'éditeur SQL de votre projet Supabase :
```sql
CREATE TABLE IF NOT EXISTS public.briefs (
  id UUID DEFAULT gen_random_uuid() PRIMARY KEY,
  created_at TIMESTAMP WITH TIME ZONE DEFAULT timezone('utc'::text, now()) NOT NULL,
  full_name TEXT NOT NULL,
  email TEXT NOT NULL,
  services TEXT[] DEFAULT '{}',
  budget_range TEXT,
  message TEXT NOT NULL
);

-- Activation de RLS (Row Level Security)
ALTER TABLE public.briefs ENABLE ROW LEVEL SECURITY;

-- Autoriser l'insertion publique depuis le site web
CREATE POLICY "Permettre l'envoi public de briefs" 
ON public.briefs FOR INSERT 
WITH CHECK (true);
```

---

## 🚀 Visualisation Locale

Vous pouvez ouvrir directement `index.html` dans votre navigateur (double-clic) ou lancer un serveur local avec n'importe quelle commande :
```bash
# Avec npx serve :
npx serve .

# Ou avec Python 3 :
python3 -m http.server 8080
```
Puis accédez à `http://localhost:8080`.
