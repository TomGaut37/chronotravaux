# chronotravaux
Suivi de chantier 
ChronoTravaux/
│
├── ChronoTravaux.html   ← ton fichier HTML complet
├── manifest.json        ← manifest pour PWA
├── sw.js                ← service worker pour hors-ligne
└── icon.png             ← icône 192x192 pour la PWA
{
  "name": "ChronoTravaux",
  "short_name": "Chrono",
  "start_url": "./ChronoTravaux.html",
  "display": "standalone",
  "background_color": "#f5f5f5",
  "theme_color": "#4caf50",
  "icons": [
    {
      "src": "icon.png",
      "sizes": "192x192",
      "type": "image/png"
    }
  ]
}
self.addEventListener('install', function(e) {
  e.waitUntil(
    caches.open('ChronoCache').then(function(cache) {
      return cache.addAll([
        './ChronoTravaux.html',
        './manifest.json',
        './icon.png'
      ]);
    })
  );
});

self.addEventListener('fetch', function(e) {
  e.respondWith(
    caches.match(e.request).then(function(response) {
      return response || fetch(e.request);
    })
  );
});
https://TonNom.github.io/ChronoTravaux/ChronoTravaux.html
