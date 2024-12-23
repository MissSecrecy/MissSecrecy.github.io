<!DOCTYPE html>
<html>
<head>
  <title>Interaktive Karte</title>
  <link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css" />
  <style>
    html, body {
      height: 100%;
      margin: 0;
    }
    #map {
      height: 100%;
      width: 100%;
    }
  </style>
</head>
<body>
  <div id="map"></div>
  <script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>
  <script>
    // Karte initialisieren
    var map = L.map('map').setView([47.0, 9.0], 6); // Anfangsposition auf Mitteleuropa

    // Kartenlayer hinzufügen (OpenStreetMap)
    L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
      attribution: '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors'
    }).addTo(map);

    // Wegpunkte mit Koordinaten und Fotos
    var waypoints = [
      {coords: [54.1, 11.6], photos: ['photo_rerik.jpg'], description: 'Rerik 1'},
      {coords: [53.629, 11.414], photos: ['photo_schwerin.jpg'], description: 'Schwerin'},
      {coords: [54.15, 11.65], photos: ['photo_rerik2.jpg'], description: 'Rerik 2'},
      {coords: [50.422362650588056, 10.093844216283632], photos: ['photo_sondernau.jpg'], description: 'Sondernau'},
      {coords: [49.409, 8.694], photos: ['photo_heidelberg.jpg'], description: 'Heidelberg'},
      {coords: [47.384, 8.118], photos: ['photo_hunzenschwil.jpg', 'photo_hunzenschwil2.jpg'], description: 'Hunzenschwil'},
      {coords: [47.354, 8.155], photos: ['photo_seon.jpg'], description: 'Seon'},
      {coords: [47.391, 8.05], photos: ['photo_aarau.jpg'], description: 'Aarau'},
      {coords: [47.050, 8.308], photos: ['photo_luzern.jpg'], description: 'Luzern'},
      {coords: [47.34818496845918, 8.158562032745069], photos: ['photo_seon2.jpg'], description: 'Seon'},
      {coords: [47.697, 8.636], photos: ['photo_schaffhausen.jpg', 'photo_schaffhausen2.jpg'], description: 'Schaffhausen'},
      {coords: [47.266, 9.620], photos: ['photo_uebersaxen.jpg', 'photo_uebersaxen2.jpg'], description: 'Übersaxen'},
      {coords: [46.406, 8.080], photos: ['photo_aletsch.jpg', 'photo_aletsch2.jpg'], video: 'video_aletsch.mp4', description: 'Aletsch Arena'},
      {coords: [45.976, 7.658], photos: ['photo_zermatt.jpg', 'photo_zermatt2.jpg'], description: 'Zermatt'},
      {coords: [42.356, 10.921], photos: ['photo_giglio.jpg', 'photo_giglio2.jpg'], description: 'Giglio'},
      {coords: [41.902, 12.496], photos: ['photo_rom.jpg', 'photo_rom2.jpg'], description: 'Rom'}
    ];

    // Marker hinzufügen
    var coordinates = [];
    waypoints.forEach(point => {
      // Dynamische HTML-Generierung für größere Fotos und Videos
      var photoHtml = point.photos.map(photo => `<img src="${photo}" alt="Photo" width="300" style="margin: 5px;">`).join('');
      var videoHtml = point.video ? `<video controls width="300" style="margin: 5px;"><source src="${point.video}" type="video/mp4">Your browser does not support the video tag.</video>` : '';
      L.marker(point.coords).addTo(map)
        .bindPopup(`<h3>${point.description}</h3>${photoHtml}${videoHtml}`);
      coordinates.push(point.coords);
    });

    // Linienverbindung zwischen den Punkten
    var polyline = L.polyline(coordinates, {color: 'blue'}).addTo(map);
    map.fitBounds(polyline.getBounds());
  </script>
</body>
</html>


