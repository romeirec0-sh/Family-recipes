
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Family Recipes</title>
<style>
  body {
    margin: 0;
    font-family: 'Georgia', serif;
    background: #fffaf4;
    color: #333;
  }

  header {
    background: #b85c38;
    color: white;
    text-align: center;
    padding: 2rem;
  }
  header h1 {
    margin: 0;
    font-size: 2.5rem;
    letter-spacing: 2px;
  }
  nav {
    background: #f7e7d7;
    padding: 0.5rem 1rem;
    display: flex;
    justify-content: center;
  }
  nav ul {
    display: flex;
    list-style: none;
    margin: 0;
    padding: 0;
    gap: 1.5rem;
  }
  nav li { position: relative; }
  nav a {
    text-decoration: none;
    color: #b85c38;
    font-weight: bold;
    padding: 0.5rem;
  }
  nav li:hover > ul { display: block; }
  nav ul ul {
    display: none;
    position: absolute;
    top: 2rem;
    left: 0;
    background: #fff5eb;
    padding: 0.5rem;
    border-radius: 5px;
    box-shadow: 0 2px 6px rgba(0,0,0,0.1);
  }
  nav ul ul li { margin: 0; }

  main { max-width: 900px; margin: 2rem auto; padding: 1rem; }

  section { margin-bottom: 3rem; }
  h2 {
    border-bottom: 2px solid #b85c38;
    padding-bottom: 0.3rem;
    margin-bottom: 1rem;
    color: #b85c38;
  }

  .recipe-card {
    background: #fff;
    padding: 1rem 1.5rem;
    margin-bottom: 1.5rem;
    border-radius: 8px;
    box-shadow: 0 3px 8px rgba(0,0,0,0.1);
  }
  .recipe-card h3 { margin: 0 0 0.5rem 0; color: #8d3b1d; }
  .recipe-card ul { margin: 0.5rem 0; padding-left: 1.2rem; }
  .recipe-card ol { margin: 0.5rem 0; padding-left: 1.2rem; }

  .form-section, .notes-section, .ai-section {
    background: #fff5eb;
    padding: 1.5rem;
    border-radius: 8px;
    box-shadow: 0 3px 6px rgba(0,0,0,0.08);
    margin-bottom: 2rem;
  }

  input, textarea, button {
    width: 100%;
    padding: 0.8rem;
    margin-top: 0.5rem;
    margin-bottom: 1rem;
    border-radius: 6px;
    border: 1px solid #ddd;
    font-size: 1rem;
  }
  button {
    background: #b85c38;
    color: white;
    font-weight: bold;
    border: none;
    cursor: pointer;
    transition: 0.2s;
  }
  button:hover { background: #8d3b1d; }

  footer {
    text-align: center;
    padding: 1.5rem;
    background: #f7e7d7;
    font-weight: 500;
    margin-top: 2rem;
  }
</style>
</head>
<body>

<header>
  <h1>🍴 Family Recipes 🍴</h1>
  <p>A boujie chef-style cookbook for the whole family</p>
</header>

<nav>
  <ul>
    <li><a href="#breakfast">Breakfast</a></li>
    <li><a href="#lunch">Lunch</a></li>
    <li><a href="#dinner">Dinner</a></li>
    <li><a href="#desserts">Desserts</a></li>
    <li><a href="#breads">Breads</a></li>
    <li><a href="#sauces">Sauces</a></li>
    <li><a href="#add-recipe">Add Recipe</a></li>
    <li><a href="#notes">Notes</a></li>
    <li><a href="#ai">AI Generator</a></li>
  </ul>
</nav>

<main>
  <!-- Breakfast Section -->
  <section id="breakfast">
    <h2>Breakfast</h2>
    <div class="recipe-card">
      <h3>Sourdough Strawberry & Cream</h3>
      <ul>
        <li>Sourdough starter</li>
        <li>Flour, water, salt</li>
        <li>Strawberries</li>
        <li>Cream cheese filling</li>
      </ul>
      <ol>
        <li>Prepare dough and fold in strawberries.</li>
        <li>Spread cream cheese filling.</li>
        <li>Shape and bake until golden.</li>
      </ol>
    </div>
  </section>

  <!-- Lunch Section -->
  <section id="lunch">
    <h2>Lunch</h2>
    <div class="recipe-card">
      <h3>Pizza Hut-Style Pizza</h3>
      <ul>
        <li>Flour, yeast, salt, sugar</li>
        <li>Olive oil</li>
        <li>Tomato sauce</li>
        <li>Mozzarella cheese</li>
      </ul>
      <ol>
        <li>Prepare dough with overnight ferment.</li>
        <li>Shape, top, and bake to golden perfection.</li>
      </ol>
    </div>
  </section>

  <!-- Dinner Section -->
  <section id="dinner">
    <h2>Dinner</h2>
    <div class="recipe-card">
      <h3>Crispy Popeyes-Style Wings</h3>
      <ul>
        <li>Chicken wings</li>
        <li>Spices: paprika, cayenne, garlic powder</li>
        <li>Oil for baking</li>
      </ul>
      <ol>
        <li>Marinate wings with spices and oil.</li>
        <li>Bake until crispy outside, juicy inside.</li>
        <li>Toss with buffalo or parmesan sauce.</li>
      </ol>
    </div>
  </section>

  <!-- Desserts Section -->
  <section id="desserts">
    <h2>Desserts</h2>
    <div class="recipe-card">
      <h3>Mango Cheesecake Cobbler</h3>
      <ul>
        <li>Shortbread crust</li>
        <li>Mango filling</li>
        <li>Cream cheese swirl</li>
      </ul>
      <ol>
        <li>Prepare crust and mango filling.</li>
        <li>Swirl cream cheese into filling.</li>
        <li>Bake until set and golden.</li>
      </ol>
    </div>
  </section>

  <!-- Breads Section -->
  <section id="breads">
    <h2>Breads</h2>
    <div class="recipe-card">
      <h3>Blueberry Sourdough</h3>
      <ul>
        <li>Sourdough starter</li>
        <li>Flour, water, salt</li>
        <li>Blueberries</li>
        <li>Cream cheese filling</li>
      </ul>
      <ol>
        <li>Mix dough and fold in blueberries.</li>
        <li>Spread cream cheese inside.</li>
        <li>Shape and bake to perfection.</li>
      </ol>
    </div>
  </section>

  <!-- Add Recipe -->
  <section id="add-recipe" class="form-section">
    <h2>Add Your Recipe</h2>
    <input type="text" id="recipeName" placeholder="Recipe Name"/>
    <textarea id="recipeIngredients" placeholder="Ingredients (comma separated)"></textarea>
    <textarea id="recipeSteps" placeholder="Step-by-step Instructions (numbered)"></textarea>
    <button onclick="addRecipe()">Add Recipe</button>
    <div id="addedRecipes"></div>
  </section>

  <!-- Notes -->
  <section id="notes" class="notes-section">
    <h2>Family Notes / Comments</h2>
    <textarea id="commentInput" placeholder="Leave a note for the family..."></textarea>
    <button onclick="addComment()">Save Note</button>
    <div id="commentsList"></div>
  </section>

  <!-- AI Generator -->
  <section id="ai" class="ai-section">
    <h2>AI Recipe Generator</h2>
    <input type="text" id="aiInput" placeholder="Type your idea (e.g. Truffle pasta)"/>
    <button onclick="generateAIRecipe()">Generate Recipe</button>
    <div id="aiOutput"></div>
  </section>
</main>

<footer>
  Family Recipes © 2025 | Made with ❤️
</footer>

<script>
  function addRecipe() {
    const name = document.getElementById('recipeName').value;
    const ingredients = document.getElementById('recipeIngredients').value.split(',');
    const steps = document.getElementById('recipeSteps').value.split('.');
    if(!name || ingredients.length === 0 || steps.length === 0) return alert('Fill all fields');
    const container = document.getElementById('addedRecipes');
    const card = document.createElement('div');
    card.className = 'recipe-card';
    card.innerHTML = `<h3>${name}</h3>
      <ul>${ingredients.map(i=>`<li>${i.trim()}</li>`).join('')}</ul>
      <ol>${steps.map(s=>`<li>${s.trim()}</li>`).join('')}</ol>`;
    container.appendChild(card);
    document.getElementById('recipeName').value='';
    document.getElementById('recipeIngredients').value='';
    document.getElementById('recipeSteps').value='';
  }

  function addComment() {
    const comment = document.getElementById('commentInput').value;
    if(!comment) return;
    const container = document.getElementById('commentsList');
    const card = document.createElement('div');
    card.className='recipe-card';
    card.innerHTML = `<p>${comment}</p>`;
    container.appendChild(card);
    document.getElementById('commentInput').value='';
  }

  function generateAIRecipe() {
    const idea = document.getElementById('aiInput').value;
    const container = document.getElementById('aiOutput');
    if(!idea) return alert('Type something first');
    container.innerHTML = `<h3>AI Recipe for: ${idea}</h3>
      <p><em>Recipe details would appear here once AI is connected</em></p>`;
  }
</script>

</body>
</html>
