# find-your-dream-hom

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>HomeFinder India</title>
<style>
* { box-sizing: border-box; }
body {
  margin: 0;
  font-family: Arial, sans-serif;
  background: #f4f6fa;
  color: #222;
}
header {
  background: #123b65;
  color: white;
  padding: 22px;
  text-align: center;
}
nav {
  background: #092b4d;
  padding: 14px;
  text-align: center;
}
nav a {
  color: white;
  text-decoration: none;
  margin: 12px;
}
.hero {
  text-align: center;
  padding: 35px 15px;
  background: #dcecff;
}
.container {
  max-width: 1100px;
  margin: auto;
  padding: 20px;
}
.filters, .add-form {
  background: white;
  padding: 20px;
  border-radius: 12px;
  margin-bottom: 25px;
}
input, select, button {
  width: 100%;
  padding: 12px;
  margin: 7px 0;
  border: 1px solid #ccc;
  border-radius: 6px;
}
button {
  background: #1267a5;
  color: white;
  border: 0;
  cursor: pointer;
  font-weight: bold;
}
button:hover { background: #084b80; }
.properties {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 20px;
}
.card {
  background: white;
  border-radius: 12px;
  padding: 18px;
  box-shadow: 0 2px 8px #ddd;
}
.card h3 { color: #123b65; }
.price {
  color: #087b48;
  font-size: 21px;
  font-weight: bold;
}
footer {
  text-align: center;
  padding: 20px;
  background: #123b65;
  color: white;
}
</style>
</head>
<body>

<header>
  <h1>HomeFinder India</h1>
  <p>Find Your Dream House – Buy or Rent</p>
</header>

<nav>
  <a href="#home">Home</a>
  <a href="#properties">Properties</a>
  <a href="#add">Add Property</a>
</nav>

<section class="hero" id="home">
  <h2>Find Houses Across India</h2>
  <p>Search properties according to your budget and location.</p>
</section>

<main class="container">

<section class="filters">
  <h2>Search Your Property</h2>

  <select id="type">
    <option value="">Buy or Rent</option>
    <option value="Sale">For Sale</option>
    <option value="Rent">For Rent</option>
  </select>

  <input id="state" placeholder="Enter State">
  <input id="district" placeholder="Enter District">
  <input id="area" placeholder="Enter Area">

  <input id="min" type="number" placeholder="Minimum budget (₹)">
  <input id="max" type="number" placeholder="Maximum budget (₹)">

  <button onclick="searchProperties()">Search Properties</button>
  <button onclick="showAll()">Show All Properties</button>
</section>

<section id="properties">
  <h2>Available Properties</h2>
  <div class="properties" id="propertyList"></div>
</section>

<section class="add-form" id="add">
  <h2>Add Your Property</h2>
  <input id="owner" placeholder="Owner name">
  <select id="newType">
    <option value="Sale">For Sale</option>
    <option value="Rent">For Rent</option>
  </select>
  <input id="newTitle" placeholder="House title">
  <input id="newState" placeholder="State">
  <input id="newDistrict" placeholder="District">
  <input id="newArea" placeholder="Area">
  <input id="newPrice" type="number" placeholder="Amount in ₹">
  <input id="phone" type="tel" placeholder="Owner contact number">
  <button onclick="addProperty()">Submit Property</button>
  <p id="message"></p>
</section>

</main>

<footer>
  <p>© 2026 HomeFinder India | Property Search Website</p>
</footer>

<script>
let properties = [
 {
  title: "2 BHK House",
  type: "Sale",
  state: "Telangana",
  district: "Hyderabad",
  area: "Kukatpally",
  price: 4500000,
  owner: "Demo Owner",
  phone: "9000000001"
 },
 {
  title: "1 BHK House",
  type: "Rent",
  state: "Andhra Pradesh",
  district: "Guntur",
  area: "Brodipet",
  price: 8000,
  owner: "Demo Owner",
  phone: "9000000002"
 },
 {
  title: "3 BHK House",
  type: "Sale",
  state: "Karnataka",
  district: "Bengaluru",
  area: "Whitefield",
  price: 7500000,
  owner: "Demo Owner",
  phone: "9000000003"
 }
];

function displayProperties(list) {
 const container = document.getElementById("propertyList");
 container.innerHTML = "";

 if (list.length === 0) {
  container.innerHTML = "<p>No matching properties found.</p>";
  return;
 }

 list.forEach(p => {
  container.innerHTML += `
   <div class="card">
    <h3>${p.title}</h3>
    <p><b>${p.type === "Sale" ? "For Sale" : "For Rent"}</b></p>
    <p>${p.area}, ${p.district}, ${p.state}</p>
    <p class="price">₹${p.price.toLocaleString("en-IN")}</p>
    <p>Owner: ${p.owner}</p>
    <p>Contact: ${p.phone}</p>
   </div>`;
 });
}

function searchProperties() {
 const type = document.getElementById("type").value;
 const state = document.getElementById("state").value.toLowerCase();
 const district = document.getElementById("district").value.toLowerCase();
 const area = document.getElementById("area").value.toLowerCase();
 const min = Number(document.getElementById("min").value) || 0;
 const max = Number(document.getElementById("max").value) || Infinity;

 const results = properties.filter(p =>
  (!type || p.type === type) &&
  p.state.toLowerCase().includes(state) &&
  p.district.toLowerCase().includes(district) &&
  p.area.toLowerCase().includes(area) &&
  p.price >= min && p.price <= max
 );

 displayProperties(results);
}

function showAll() {
 displayProperties(properties);
}

function addProperty() {
 const owner = document.getElementById("owner").value.trim();
 const title = document.getElementById("newTitle").value.trim();
 const state = document.getElementById("newState").value.trim();
 const district = document.getElementById("newDistrict").value.trim();
 const area = document.getElementById("newArea").value.trim();
 const price = Number(document.getElementById("newPrice").value);
 const phone = document.getElementById("phone").value.trim();

 if (!owner || !title || !state || !district ||
     !area || !price || !phone) {
  alert("Please fill all property details.");
  return;
 }

 if (!/^[0-9]{10}$/.test(phone)) {
  alert("Enter a valid 10-digit Indian mobile number.");
  return;
 }

 properties.push({
  title,
  type: document.getElementById("newType").value,
  state, district, area, price, owner, phone
 });

 displayProperties(properties);
 document.getElementById("message").textContent =
  "Property added successfully in this browser!";
}

displayProperties(properties);
</script>

</body>
</html>
