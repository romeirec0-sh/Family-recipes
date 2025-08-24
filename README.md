<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Family Recipes</title>
  <style>
    body {
      font-family: "Poppins", sans-serif;
      margin: 0;
      padding: 0;
      background: #faf9f6;
      color: #333;
    }
    header {
      background: linear-gradient(135deg, #ff6f61, #ffcc70);
      color: white;
      padding: 1.5rem;
      text-align: center;
    }
    header h1 {
      margin: 0;
      font-size: 2rem;
      letter-spacing: 2px;
    }
    nav {
      background: #fff;
      box-shadow: 0 2px 5px rgba(0,0,0,0.1);
      display: flex;
      justify-content: center;
      padding: 0.5rem;
    }
    nav ul {
      list-style: none;
      margin: 0;
      padding: 0;
      display: flex;
      gap: 2rem;
    }
    nav li {
      position: relative;
    }
    nav a {
      text-decoration: none;
      color: #333;
      font-weight: 600;
      padding: 0.5rem;
    }
    nav li:hover ul {
      display: block;
    }
    nav ul ul {
      display: none;
      position: absolute;
      top: 2rem;
      left: 0;
      background: #fff;
      padding: 0.5rem;
      box-shadow: 0 2px 5px rgba(0,0,0,0.2);
    }
    nav ul ul li {
      margin: 0;
    }
    main {
      max-width: 900px;
      margin: 2rem auto;
      padding: 1rem;
    }
    section {
      margin-bottom: 2.5rem;
    }
    h2 {
      border-bottom: 2px solid #ff6f61;
      padding-bottom: 0.3rem;
      margin-bottom: 1rem;
      color: #ff6f61;
    }
    .recipe-card {
      background: #fff;
      padding: 1rem;
      margin-bottom: 1rem;
      border-radius: 8px;
      box-shadow: 0 2px 6px rgba(0,0,0,0.1);
    }
    .recipe-card h3 {
      margin: 0;
      color: #333;
    }
    .generator {
      background: #fff;
      padding: 1.5rem;
      border-radius: 8px;
      box-shadow: 0 2px 6px rgba(0,0,0,0.1);
    }
    textarea, input, button {
      width: 100%;
      padding: 0.7rem;
      margin-top: 0.5rem;
      border: 1px solid #ddd;
      border-radius: 6px;
      font-size: 1rem;
    }
    button {
      background: #ff6f61;
      color: white;
      border: none;
      cursor: pointer;
      transition: 0.2s;
    }
    button:hover {
      background: #e85c50;
    }
    footer {
      text-align: center;
      background: #ffcc70;
      padding: 1rem;
      margin-top: 2rem;
      font-weight: 500;
    }
  </style>
</head>
<body>
  <header>
    <h1>🍴 Family Recipes 🍴</h1>
    <p>Our little book of flavor, love & memories</p>
  </header>
  <nav>
    <ul>
      <li><a href="#">Breakfast</a>
        <ul>
          <li><a href="#breakfast">Pancakes</a></li>
          <li><a href="#breakfast">Omelettes</a></li>
        </ul>
      </li>
      <li><a href="#">Lunch</a>
        <ul>
          <li><a href="#lunch">Sandwiches</a></li>
          <li><a href="#lunch">Pasta</a></li>
        </ul>
      </li>
      <li><a href="#">Dinner</a>
        <ul>
          <li><a href="#dinner">Chicken</a></li>
          <li><a href="#dinner">Seafood</a></li>
        </ul>
      </li>
      <li><a href="#">Desserts</a></li>
      <li><a href="#">Sauces</a></li>
      <li><a href="#">Breads</a></li>
    </ul>
  </nav>

  <main>
    <section id="breakfast">
      <h2>Breakfast</h2>
      <div class="recipe-card">
        <h3>Fluffy Pancakes</h3>
        <p>Light, buttery pancakes — perfect with maple syrup & berries.</p>
      </div>
    </section>

    <section id="generator">
      <h2>AI Recipe Generator</h2>
      <div class="generator">
        <label for="idea">Enter your idea (ex: “Garlic butter chicken wings with citrus”):</label>
        <textarea id="idea" rows="3"></textarea>
        <button onclick="generateRecipe()">Generate Recipe</button>
        <div id="recipe-output"></div>
      </div>
    </section>

    <section id="notes">
      <h2>Notes & Comments</h2>
      <textarea id="comment" placeholder="Leave a note for the family..."></textarea>
      <button onclick="saveComment()">Save Note</button>
      <div id="comments-list"></div>
    </section>
  </main>

  <footer>
    Family Recipes © 2025 | Made with ❤️
  </footer>

  <script>
    function generateRecipe() {
      const idea = document.getElementById("idea").value;
      const output = document.getElementById("recipe-output");
      if (!idea.trim()) {
        output.innerHTML = "<p>Please type an idea first!</p>";
        return;
      }
      output.innerHTML = `<h3>✨ Recipe for: ${idea}</h3>
        <p><em>This is where AI-generated recipe details would appear (connect API later).</em></p>`;
    }

    function saveComment() {
      const comment = document.getElementById("comment").value;
      if (!comment.trim()) return;
      const list = document.getElementById("comments-list");
      const div = document.createElement("div");
      div.classList.add("recipe-card");
      div.innerHTML = `<p>${comment}</p>`;
      list.appendChild(div);
      document.getElementById("comment").value = "";
    }
  </script>
</body>
</html>
