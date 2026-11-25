# PRODUCE AI

A responsive, static fruit and vegetable recognition app using your existing Google Teachable Machine image model.

## Setup
1. Open `index.html` and set `CFG.MODEL_URL` to your Teachable Machine TensorFlow.js model URL. The project intentionally retains the original placeholder until you provide the real model URL.
2. Run locally with `python3 -m http.server 8000` and open `http://localhost:8000`.
3. Deploy the entire folder to a static HTTPS host such as Netlify Drop. HTTPS is required for camera access on phones.

## Project files
- `index.html` — application shell, scanner, model integration, dashboard, history, analytics, settings and encyclopedia UI.
- `produce-database.js` — independent, structured information profiles for all 14 supported produce classes, with alias-safe lookup and source references.
- `README.md` — setup and deployment.

## Model and database separation
The scanner loads the configured Teachable Machine model with `tmImage.load()` and uses its real `predict()` output. The database does not create, modify or simulate model predictions. `getProduceInfo(className)` maps a predicted class name to a profile while tolerating capitalization, spaces, underscores, hyphens and common plural variants.

## Included features
- Camera capture, front/rear camera switching, image upload and drag-and-drop.
- Real model confidence scores and alternative predictions.
- Local scan history, analytics, CSV and JSON scan exports.
- Browse/search all 14 produce profiles; fruit/vegetable filters; favourites.
- Seven profile tabs: Overview, Growing Guide, Nutrition, Food Safety, Storage, Preparation and Facts.
- Per-100 g nutrition comparison for up to three produce items.
- Print-friendly profiles and downloadable JSON profile data.
- Responsive desktop/mobile layout and dark/light theme.

## Data quality notes
Nutrition figures are approximate values per 100 g edible raw portion, rounded from USDA FoodData Central entries and may vary by cultivar and maturity. Growing recommendations are general references, not location-specific agronomic prescriptions. Consult the linked government and university resources for local details. Shelf-life estimates are quality guidance, not a guarantee of food safety.

The image classifier identifies only a likely class. It cannot verify food safety, contamination, pesticide residues, toxins or internal spoilage. Never treat identification as proof that produce is safe to eat.

## Privacy
Predictions run in the browser. Saved scans remain in the browser's IndexedDB on that device. Favourites and settings use local storage.

## Install as a phone web app (PWA)
- This folder now includes `manifest.webmanifest`, `service-worker.js`, app icons, and install prompt support.
- Deploy the entire folder to an HTTPS static host (Netlify Drop is one option). HTTPS is required for camera access and service workers.
- **Android:** open the published site in Chrome. Use the visible Install app button if offered, or Chrome menu → Install app / Add to Home screen.
- **iPhone:** open the published site in Safari → Share → Add to Home Screen → Add. The install button also provides this guidance on iOS where the browser install prompt is not supported.
- The service worker caches the application shell for repeat visits/offline shell loading. AI predictions need the Teachable Machine model and TensorFlow/Teachable Machine libraries; initial model setup and prediction may still require internet.
- Set your actual model URL in `CFG.MODEL_URL` before deployment or use Settings → Model URL.
