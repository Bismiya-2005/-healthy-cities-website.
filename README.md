<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Healthy Cities & Human Settlements</title>
  <link href="https://cdn.jsdelivr.net/npm/tailwindcss@2.2.19/dist/tailwind.min.css" rel="stylesheet">
  <link rel="stylesheet" href="https://unpkg.com/leaflet/dist/leaflet.css" />
  <style>
    body { font-family: 'Inter', sans-serif; }
    .hero {
      background: linear-gradient(rgba(0,0,0,0.5), rgba(0,0,0,0.5)),
                  url('https://images.unsplash.com/photo-1505761671935-60b3a7427bad') center/cover;
    }
    #map { height: 500px; width: 100%; }
  </style>
</head>
<body class="bg-gray-50 text-gray-800">

  <!-- Header -->
  <header class="bg-white shadow fixed w-full z-10">
    <div class="max-w-7xl mx-auto px-6 py-4 flex justify-between items-center">
      <h1 class="text-2xl font-bold text-green-700">Healthy Cities</h1>
      <nav class="space-x-6">
        <a href="#mission" class="hover:text-green-600">Mission</a>
        <a href="#datasets" class="hover:text-green-600">Datasets</a>
        <a href="#maps" class="hover:text-green-600">Maps</a>
        <a href="#collaboration" class="hover:text-green-600">Collaborate</a>
      </nav>
    </div>
  </header>

  <!-- Hero -->
  <section class="hero h-screen flex items-center justify-center text-center text-white">
    <div>
      <h2 class="text-5xl font-bold">Data Pathways to Healthy Cities</h2>
      <p class="mt-4 text-lg max-w-2xl mx-auto">
        Using data to monitor health, manage resources, reduce pollution, improve housing & transport, 
        and ensure equity — making cities inclusive, safe, resilient, and sustainable.
      </p>
      <a href="#collaboration" class="mt-6 inline-block bg-green-600 hover:bg-green-700 text-white px-6 py-3 rounded-lg text-lg font-medium shadow">
        Get Involved
      </a>
    </div>
  </section>

  <!-- Mission -->
  <section id="mission" class="py-16 bg-gray-100">
    <div class="max-w-5xl mx-auto px-6 text-center">
      <h3 class="text-3xl font-bold text-green-700">Our Mission</h3>
      <p class="mt-6 text-lg leading-relaxed">
        We use urban data to track health, housing, transport, and environment. 
        This work directly supports UN SDG 11: 
        <span class="font-semibold">Make cities and human settlements inclusive, safe, resilient and sustainable.</span>
      </p>
    </div>
  </section>

  <!-- Datasets -->
  <section id="datasets" class="py-16">
    <div class="max-w-6xl mx-auto px-6">
      <h3 class="text-3xl font-bold text-center text-green-700">Key Datasets We Monitor</h3>
      <div class="mt-10 grid md:grid-cols-3 gap-8">
        <div class="bg-white shadow rounded-2xl p-6 hover:shadow-lg">
          <h4 class="font-semibold text-xl text-green-600">Urban Health</h4>
          <p class="mt-4 text-gray-600">Air quality, disease prevalence, healthcare access, green spaces.</p>
        </div>
        <div class="bg-white shadow rounded-2xl p-6 hover:shadow-lg">
          <h4 class="font-semibold text-xl text-green-600">Pollution & Resources</h4>
          <p class="mt-4 text-gray-600">Air, water, waste management, energy efficiency.</p>
        </div>
        <div class="bg-white shadow rounded-2xl p-6 hover:shadow-lg">
          <h4 class="font-semibold text-xl text-green-600">Housing & Transport</h4>
          <p class="mt-4 text-gray-600">Affordable housing, sustainable mobility, service equity.</p>
        </div>
      </div>
    </div>
  </section>

  <!-- Map -->
  <section id="maps" class="py-16 bg-gray-100">
    <div class="max-w-6xl mx-auto px-6 text-center">
      <h3 class="text-3xl font-bold text-green-700">Kerala Climate Dashboard</h3>
      <p class="mt-4 text-lg text-gray-700">Climatic conditions, temperatures, and betterment suggestions across 14 districts.</p>
      <div class="mt-8 border rounded-xl overflow-hidden shadow-lg">
        <div id="map"></div>
      </div>
    </div>
  </section>

  <!-- Collaboration -->
  <section id="collaboration" class="py-16">
    <div class="max-w-4xl mx-auto px-6 text-center">
      <h3 class="text-3xl font-bold text-green-700">Collaborate With Us</h3>
      <p class="mt-4 text-lg text-gray-600">
        Governments, NGOs, researchers, and communities can partner with us to create sustainable urban solutions.
      </p>
      <form class="mt-8 space-y-4 max-w-md mx-auto">
        <input type="text" placeholder="Your Name" class="w-full px-4 py-3 border rounded-lg focus:ring-2 focus:ring-green-600">
        <input type="email" placeholder="Your Email" class="w-full px-4 py-3 border rounded-lg focus:ring-2 focus:ring-green-600">
        <textarea placeholder="Your Message" rows="4" class="w-full px-4 py-3 border rounded-lg focus:ring-2 focus:ring-green-600"></textarea>
        <button type="submit" class="w-full bg-green-600 text-white px-6 py-3 rounded-lg font-medium hover:bg-green-700">
          Submit
        </button>
      </form>
    </div>
  </section>

  <!-- Footer -->
  <footer class="bg-green-700 text-white py-6 mt-10">
    <div class="max-w-6xl mx-auto px-6 text-center">
      <p>&copy; 2025 Healthy Cities Initiative. All rights reserved.</p>
    </div>
  </footer>

  <!-- Scripts -->
  <script src="https://unpkg.com/leaflet/dist/leaflet.js"></script>
  <script>
    var map = L.map('map').setView([10.5, 76.2], 7);
    L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
      attribution: '&copy; OpenStreetMap contributors'
    }).addTo(map);

    // Suggestions based on conditions
    function getSuggestion(cond) {
      switch(cond.toLowerCase()) {
        case "hot": return "Expand tree cover, promote rooftop gardens, ensure water supply.";
        case "rain": return "Strengthen drainage, harvest rainwater, flood-proof infrastructure.";
        case "cloudy": return "Diversify energy with wind & hydro, improve lighting efficiency.";
        case "humid": return "Expand ventilation, monitor vector-borne diseases, promote greenery.";
        case "cool": return "Support eco-tourism, sustainable heating, promote organic farming.";
        case "sunny": return "Harness solar energy, conserve water, plant drought-resistant crops.";
        default: return "Adopt climate-smart urban planning.";
      }
    }

    // Kerala districts with conditions + temp
    const districts = [
      { name: "Thiruvananthapuram", lat: 8.5241, lon: 76.9366, cond: "Sunny", temp: 30 },
      { name: "Kollam", lat: 8.8932, lon: 76.6141, cond: "Cloudy", temp: 29 },
      { name: "Pathanamthitta", lat: 9.2640, lon: 76.7870, cond: "Rain", temp: 26 },
      { name: "Alappuzha", lat: 9.4981, lon: 76.3388, cond: "Humid", temp: 28 },
      { name: "Kottayam", lat: 9.5916, lon: 76.5222, cond: "Cloudy", temp: 27 },
      { name: "Idukki", lat: 9.9185, lon: 77.1025, cond: "Cool", temp: 21 },
      { name: "Ernakulam", lat: 9.9816, lon: 76.2999, cond: "Sunny", temp: 30 },
      { name: "Thrissur", lat: 10.5276, lon: 76.2144, cond: "Humid", temp: 29 },
      { name: "Palakkad", lat: 10.7867, lon: 76.6548, cond: "Hot", temp: 32 },
      { name: "Malappuram", lat: 11.0730, lon: 76.0743, cond: "Sunny", temp: 31 },
      { name: "Kozhikode", lat: 11.2588, lon: 75.7804, cond: "Cloudy", temp: 28 },
      { name: "Wayanad", lat: 11.6854, lon: 76.1320, cond: "Cool", temp: 20 },
      { name: "Kannur", lat: 11.8745, lon: 75.3704, cond: "Rain", temp: 25 },
      { name: "Kasaragod", lat: 12.4996, lon: 74.9860, cond: "Cloudy", temp: 27 },
    ];

    // Add markers
    districts.forEach(d => {
      const suggestion = getSuggestion(d.cond);
      L.marker([d.lat, d.lon]).addTo(map)
        .bindPopup(`<b>${d.name}</b><br>🌡 Temp: ${d.temp}°C<br>🌤 Condition: ${d.cond}<br>💡 Suggestion: ${suggestion}`);
    });
  </script>
</body>
</html>
