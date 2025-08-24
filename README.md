<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Family Recipes</title>
  <style>
    body {
      font-family: "Georgia", serif;
      margin: 0;
      background: #faf7f2;
      color: #333;
    }

    header {
      background: linear-gradient(135deg, #d4a373, #8d5524);
      padding: 20px;
      text-align: center;
      color: white;
      font-size: 28px;
      font-weight: bold;
      letter-spacing: 2px;
    }

    nav {
      background: #fff;
      box-shadow: 0 2px 5px rgba(0,0,0,0.1);
      display: flex;
      justify-content: center;
      padding: 10px 0;
    }

    nav ul {
      list-style: none;
      padding: 0;
      margin: 0;
      display: flex;
      gap: 20px;
    }

    nav li {
      position: relative;
    }

    nav a {
      text-decoration: none;
      color: #8d5524;
      font-weight: bold;
      padding: 8px 12px;
      transition: 0.3s;
    }

    nav a:hover {
      color: #d4a373;
    }

    nav ul ul {
      display: none;
      position: absolute;
      top: 30px;
      left: 0;
      background: #fff;
      box-shadow: 0 2px 5px rgba(0,0,0,0.2);
      padding: 10px;
    }

    nav li:hover > ul {
      display: block;
    }

    section {
      max-width: 900px;
      margin: 30px auto;
      padding: 20px;
      background: white;
      border-radius: 8px;
      box-shadow: 0 3px 8px rgba(0,0,0,0.1);
    }

    h2 {
      color: #8d5524;
      border-bottom: 2px solid #d4a373;
      padding-bottom: 5px;
    }

    .recipe-card {
      border: 1px solid #eee;
      padding: 15px;
      margin: 10px 0;
      border-radius: 6px;
      background: #fafafa;
    }

    .note-box {
      width: 100%;
      height: 100px;
      margin: 10px 0;
      padding: 10px;
      border-radius: 6px;
      border: 1px solid #ccc;
    }

    button {
      background: #d4a373;
      border: none;
      color: white;
      padding: 10px 15px;
      border-radius: 6px;
      cursor: pointer;
      font-weight: bold;
      transition: 0.3s;
    }

    button:hover {
      background: #8d5524;
    }
  </style>
</head>
<body>
  <header>🍴 Family Recipes</header>

  <nav>
    <ul>
      <li><a href="#">Categories ▾</a>
        <ul>
          <li><a href="#breakfast">Breakfast</a></li>
          <li><a href="#lunch">Lunch</a></li>
          <li><a href="#dinner">Dinner</a></li>
          <li><a href="#desserts">Desserts</a></li>
          <li><a href="#sauces">Sauces</a></li>
          <li><a href="#breads">Breads</a></li>
        </ul>
      </li>
      <li><a href="#add-recipe">Add Recipe</a></li>
      <li><a href="#notes">Notes</a></li>
      <li><a href="#ai">AI Generator</a></li>
    </ul>
  </nav>

  <section id="breakfast">
    <h2>Breakfast</h2>
    <div class="recipe-card">
      <h3>Sourdough Strawberry & Cream</h3>
      <p>Soft sourdough loaf swirled with strawberry and cream cheese filling.</p>
    </div>
  </section>

  <section id="lunch">
    <h2>Lunch</h2>
    <div class="recipe-card">
      <h3>Pizza Hut Style Pizza</h3>
      <p>Thick, buttery crust with overnight ferment for max flavor.</p>
    </div>
  </section>

  <section id="dinner">
    <h2>Dinner</h2>
    <div class="recipe-card">
      <h3>Crispy Popeyes-Style Wings</h3>
      <p>Perfectly seasoned, crispy outside, juicy inside. Toss with buffalo or parm.</p>
    </div>
  </section>

  <section id="desserts">
    <h2>Desserts</h2>
    <div class="recipe-card">
      <h3>Mango Cheesecake Cobbler</h3>
      <p>Mango filling with shortbread crust and cream cheese swirl.</p>
    </div>
  </section>

  <section id="sauces">
    <h2>Sauces</h2>
    <div class="recipe-card">
      <h3>Buffalo Sauce</h3>
      <p>Rich, spicy butter-based sauce for wings and more.</p>
    </div>
  </section>

  <section id="breads">
    <h2>Breads</h2>
    <div class="recipe-card">
      <h3>Blueberry Sourdough</h3>
      <p>Soft sourdough loaf with fresh blueberries and cream cheese filling.</p>
    </div>
  </section>

  <section id="add-recipe">
    <h2>Add Your Own Recipe</h2>
    <form>
      <input type="text" placeholder="Recipe Name" style="width:100%; padding:10px; margin:5px 0;"><br>
      <textarea placeholder="Ingredients & Instructions" style="width:100%; height:150px; padding:10px; margin:5px 0;"></textarea><br>
      <button type="submit">Add Recipe</button>
    </form>
  </section>

  <section id="notes">
    <h2>Notes</h2>
    <textarea class="note-box" placeholder="Write your family notes here..."></textarea>
    <button>Save Note</button>
  </section>

  <section id="ai">
    <h2>AI Recipe Generator</h2>
    <p>Type an idea and let AI build a recipe for you:</p>
    <input type="text" placeholder="e.g. truffle mac and cheese" style="width:100%; padding:10px; margin:10px 0;">
    <button>Generate Recipe</button>
    <div id="ai-result" style="margin-top:15px; padding:15px; background:#fafafa; border-radius:6px;"></div>
  </section>
</body>
</html>
