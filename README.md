<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Family Recipes</title>
  <style>
    body {
      font-family: "Georgia", serif;
      margin: 0;
      padding: 20px;
      background: #fff8f0;
      color: #333;
    }
    h1 {
      text-align: center;
      font-size: 3em;
      margin-bottom: 10px;
      color: #b85c38;
    }
    .recipe-form, .recipe-list {
      max-width: 700px;
      margin: 20px auto;
      background: #fff;
      padding: 20px;
      border-radius: 8px;
      box-shadow: 0px 4px 10px rgba(0,0,0,0.1);
    }
    label {
      display: block;
      margin: 10px 0 5px;
    }
    input, textarea, button {
      width: 100%;
      padding: 10px;
      margin-bottom: 15px;
      border-radius: 5px;
      border: 1px solid #ccc;
      font-size: 1em;
    }
    button {
      background: #b85c38;
      color: white;
      border: none;
      cursor: pointer;
    }
    button:hover {
      background: #8c4227;
    }
    .recipe-card {
      border-bottom: 1px solid #ddd;
      padding: 10px 0;
    }
    .recipe-card h3 {
      margin: 0;
      color: #444;
    }
    .recipe-card p {
      margin: 5px 0;
    }
  </style>
</head>
<body>
  <h1>🍴 Family Recipes 🍴</h1>

  <div class="recipe-form">
    <h2>Add a Recipe</h2>
    <label for="name">Recipe Name</label>
    <input type="text" id="name" placeholder="Ex: Garlic Butter Wings">

    <label for="ingredients">Ingredients</label>
    <textarea id="ingredients" placeholder="List ingredients here..."></textarea>

    <label for="steps">Instructions</label>
    <textarea id="steps" placeholder="Write step-by-step instructions..."></textarea>

    <button onclick="saveRecipe()">Save Recipe</button>
  </div>

  <div class="recipe-list">
    <h2>Saved Recipes</h2>
    <div id="recipes"></div>
  </div>

  <script>
    function saveRecipe() {
      let name = document.getElementById("name").value.trim();
      let ingredients = document.getElementById("ingredients").value.trim();
      let steps = document.getElementById("steps").value.trim();

      if (!name || !ingredients || !steps) {
        alert("Please fill in all fields!");
        return;
      }

      let recipes = JSON.parse(localStorage.getItem("recipes")) || [];
      recipes.push({ name, ingredients, steps });
      localStorage.setItem("recipes", JSON.stringify(recipes));

      displayRecipes();
      document.getElementById("name").value = "";
      document.getElementById("ingredients").value = "";
      document.getElementById("steps").value = "";
    }

    function displayRecipes() {
      let recipes = JSON.parse(localStorage.getItem("recipes")) || [];
      let recipeContainer = document.getElementById("recipes");
      recipeContainer.innerHTML = "";

      recipes.forEach((r, index) => {
        let div = document.createElement("div");
        div.className = "recipe-card";
        div.innerHTML = `
          <h3>${r.name}</h3>
          <p><strong>Ingredients:</strong> ${r.ingredients}</p>
          <p><strong>Instructions:</strong> ${r.steps}</p>
          <button onclick="deleteRecipe(${index})">Delete</button>
        `;
        recipeContainer.appendChild(div);
      });
    }

    function deleteRecipe(index) {
      let recipes = JSON.parse(localStorage.getItem("recipes")) || [];
      recipes.splice(index, 1);
      localStorage.setItem("recipes", JSON.stringify(recipes));
      displayRecipes();
    }

    window.onload = displayRecipes;
  </script>
</body>
</html>
