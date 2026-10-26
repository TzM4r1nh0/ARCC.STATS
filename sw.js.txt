const CACHE_NAME = 'arcc-stats-v1';
const urlsToCache = [
  './index.html',
  './manifest.json',
  './icon-centered.png'
];

// Instalação do Service Worker e gravação em cache
self.addEventListener('install', event => {
  event.waitUntil(
    caches.open(CACHE_NAME)
      .then(cache => {
        return cache.addAll(urlsToCache);
      })
  );
});

// Interceção de pedidos para servir a app offline
self.addEventListener('fetch', event => {
  event.respondWith(
    caches.match(event.request)
      .then(response => {
        return response || fetch(event.request);
      })
  );
});
