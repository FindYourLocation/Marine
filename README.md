<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Marine Coordinate Locator</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #e6f0f3;
      display: flex;
      flex-direction: column;
      align-items: center;
      padding: 50px;
    }
    .container {
      background: white;
      border-radius: 15px;
      padding: 30px;
      box-shadow: 0 4px 12px rgba(0,0,0,0.1);
      max-width: 500px;
      width: 100%;
      text-align: center;
    }
    input {
      width: 100%;
      padding: 10px;
      font-size: 16px;
      margin-top: 15px;
      margin-bottom: 20px;
    }
    button {
      padding: 10px 20px;
      background-color: #0077b6;
      color: white;
      border: none;
      font-size: 16px;
      border-radius: 5px;
      cursor: pointer;
    }
    #result {
      margin-top: 30px;
      display: none;
    }
    #map {
      width: 100%;
      height: 300px;
      margin-top: 20px;
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>Marine Coordinate Locator</h1>
    <p>Entrez des coordonnées GPS pour localiser une zone de plongée.</p>
    <input type="text" id="coordinates" placeholder="Coordonnées GPS">
    <button onclick="checkCoordinates()">Rechercher</button>

    <div id="result">
      <p><strong>Localisation trouvée :</strong> Mer Baltique, au large des côtes finlandaises. Zone connue pour plusieurs épaves historiques.</p>
      <div id="map"></div>
    </div>
  </div>

  <script>
    function checkCoordinates() {
      const input = document.getElementById('coordinates').value.trim();
      const result = document.getElementById('result');
      const map = document.getElementById('map');

      const correctCoords = [
        "58°42'N, 20°12'E",
        "58° 42' N, 20° 12' E",
        "58.7, 20.2",
        "58.7000, 20.2000"
      ];

      if (correctCoords.includes(input)) {
        result.style.display = 'block';
        initMap();
      } else {
        alert("Coordonnées non reconnues. Veuillez réessayer.");
      }
    }

    function initMap() {
      const mapDiv = document.getElementById('map');
      const script = document.createElement('script');
      script.src = `https://maps.googleapis.com/maps/api/js?key=YOUR_API_KEY&callback=loadMap`;
      script.async = true;
      document.body.appendChild(script);
    }

    function loadMap() {
      const location = { lat: 58.7, lng: 20.2 };
      const map = new google.maps.Map(document.getElementById('map'), {
        zoom: 6,
        center: location
      });
      new google.maps.Marker({ position: location, map: map });
    }
  </script>
</body>
</html>
