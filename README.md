manajemen-pembelajaran/
│
├── package.json
├── server.js
├── .env
├── /config
│   └── db.js
│
├── /middleware
│   └── auth.js
│
├── /routes
│   ├── public.js
│   ├── guru.js
│   └── auth.js
│
├── /views
│   ├── layout.ejs
│   ├── home.ejs
│   ├── materi.ejs
│   ├── login.ejs
│   └── partials/
│        ├── header.ejs
│        └── footer.ejs
│
├── /public
│   ├── css/style.css
│   ├── js/script.js
│   └── images/
│
└── /database
    └── schema.sql
{
  "name": "manajemen-pembelajaran",
  "version": "1.0.0",
  "description": "Website Manajemen Pembelajaran Guru Terintegrasi",
  "main": "server.js",
  "scripts": {
    "start": "node server.js",
    "dev": "nodemon server.js"
  },
  "dependencies": {
    "bcrypt": "^5.1.0",
    "chart.js": "^4.4.0",
    "dotenv": "^16.0.3",
    "ejs": "^3.1.9",
    "express": "^4.18.2",
    "express-session": "^1.17.3",
    "mysql2": "^3.6.0",
    "pdfkit": "^0.14.0"
  }
}
require("dotenv").config();
const express = require("express");
const session = require("express-session");
const path = require("path");

const app = express();

app.use(express.urlencoded({ extended: true }));
app.use(express.json());
app.use(express.static("public"));

app.set("view engine", "ejs");

app.use(
  session({
    secret: "secretkey123",
    resave: false,
    saveUninitialized: false,
  })
);

app.use((req, res, next) => {
  res.locals.user = req.session.user || null;
  next();
});

app.use("/", require("./routes/public"));
app.use("/guru", require("./routes/guru"));
app.use("/auth", require("./routes/auth"));

app.listen(3000, () => {
  console.log("Server running on http://localhost:3000");
});
const mysql = require("mysql2");

const connection = mysql.createConnection({
  host: "localhost",
  user: "root",
  password: "",
  database: "manajemen_guru",
});

connection.connect((err) => {
  if (err) throw err;
  console.log("MySQL Connected");
});

module.exports = connection;
function isLoggedIn(req, res, next) {
  if (!req.session.user) {
    return res.redirect("/auth/login");
  }
  next();
}

module.exports = { isLoggedIn };
const express = require("express");
const router = express.Router();
const bcrypt = require("bcrypt");
const db = require("../config/db");

router.get("/login", (req, res) => {
  res.render("login");
});

router.post("/login", (req, res) => {
  const { username, password } = req.body;

  db.query("SELECT * FROM users WHERE username=?", [username], async (err, result) => {
    if (result.length === 0) return res.send("User tidak ditemukan");

    const valid = await bcrypt.compare(password, result[0].password);
    if (!valid) return res.send("Password salah");

    req.session.user = result[0];
    res.redirect("/");
  });
});

router.get("/logout", (req, res) => {
  req.session.destroy();
  res.redirect("/");
});

module.exports = router;
const express = require("express");
const router = express.Router();
const db = require("../config/db");

router.get("/", (req, res) => {
  db.query("SELECT * FROM materi", (err, materi) => {
    res.render("home", { materi });
  });
});

module.exports = router;
const express = require("express");
const router = express.Router();
const db = require("../config/db");
const { isLoggedIn } = require("../middleware/auth");

router.get("/", isLoggedIn, (req, res) => {
  res.render("home");
});

router.post("/materi", isLoggedIn, (req, res) => {
  const { judul, mapel, kelas, link } = req.body;

  db.query(
    "INSERT INTO materi (judul,mapel,kelas,link) VALUES (?,?,?,?)",
    [judul, mapel, kelas, link],
    () => res.redirect("/")
  );
});

module.exports = router;
<!DOCTYPE html>
<html>
<head>
  <title>Manajemen Pembelajaran</title>
  <link rel="stylesheet" href="/css/style.css">
</head>
<body>

<%- include("partials/header") %>

<main>
  <%- body %>
</main>

<%- include("partials/footer") %>

</body>
</html>
<h2>Materi Pembelajaran</h2>

<div class="card-container">
  <% materi.forEach(m => { %>
    <div class="card">
      <h3><%= m.judul %></h3>
      <p><%= m.mapel %> - <%= m.kelas %></p>
      <a href="<%= m.link %>" target="_blank">Buka Materi</a>

      <% if (user) { %>
        <button>Edit</button>
        <button>Hapus</button>
      <% } %>
    </div>
  <% }) %>
</div>
body {
  font-family: Arial;
  margin: 0;
  background: #f4f8ff;
}

header {
  background: #0d6efd;
  color: white;
  padding: 15px;
}

nav a {
  color: white;
  margin-right: 15px;
  text-decoration: none;
}

.card-container {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
  padding: 20px;
}

.card {
  background: white;
  padding: 15px;
  border-radius: 10px;
  width: 250px;
  box-shadow: 0 2px 5px rgba(0,0,0,0.1);
}
CREATE DATABASE manajemen_guru;
USE manajemen_guru;

CREATE TABLE users (
  id INT AUTO_INCREMENT PRIMARY KEY,
  username VARCHAR(100),
  password VARCHAR(255)
);

CREATE TABLE materi (
  id INT AUTO_INCREMENT PRIMARY KEY,
  judul VARCHAR(255),
  mapel VARCHAR(100),
  kelas VARCHAR(50),
  link TEXT
);
npm install
npm start
http://localhost:3000
