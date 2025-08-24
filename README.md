<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Our Family Recipes</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Playfair+Display:wght@700&family=Roboto:wght@400;700&display=swap');

  body { font-family:'Roboto',sans-serif; margin:0; background:#fff; color:#111; }
  header { background:#c00; color:#fff; text-align:center; padding:1rem; font-family:'Playfair Display',serif; font-size:2rem; position:sticky; top:0; z-index:1000;}
  nav { display:flex; overflow-x:auto; background:#000; color:#fff; }
  nav button { flex:1; padding:.8rem 1rem; border:none; cursor:pointer; background:#000; color:#fff; font-weight:700; transition:.3s; white-space:nowrap;}
  nav button:hover, nav button.active { background:#c00; color:#fff; }
  .container { padding:1rem; }

  .recipe-card { border:1px solid #ccc; border-radius:10px; margin-bottom:1rem; background:#fff; box-shadow:0 4px 6px rgba(0,0,0,0.1);}
  .recipe-header { padding:1rem; background:#c00; color:#fff; font-weight:700; cursor:pointer; display:flex; justify-content:space-between; align-items:center; }
  .recipe-content { display:none; padding:1rem; }
  .recipe-content h4 { margin:.5rem 0; color:#c00; border-bottom:1px solid #c00; padding-bottom:.2rem; }
  .recipe-content ul, .recipe-content ol { margin:0 0 1rem 1.2rem; }
  .note-section { margin-top:1rem; }
  .note { background:#f9f9f9; padding:.5rem; border-radius:5px; margin-bottom:.5rem; border:1px solid #ddd; }

  form { background:#f1f1f1; padding:1rem; border-radius:10px; margin-bottom:1rem; }
  form h2 { color:#c00; font-family:'Playfair Display',serif; text-align:center; }
  input, textarea, select, button { width:100%; padding:.5rem; margin:.3rem 0; border-radius:5px; border:1px solid #ccc; }
  button.submit-btn { background:#c00; color:#fff; border:none; cursor:pointer; transition:.3s; font-weight:700; }
  button.submit-btn:hover { background:#900; }

  @media (max-width:768px){ nav button{ font-size:.9rem; padding:.6rem .5rem; } }
</style>
</head>
<body>

<header>Our Family Recipes</header>

<nav id="category-tabs">
  <button class="active" data-category="All">All</button>
  <button data-category="Breakfast">Breakfast</button>
  <button data-category="Lunch">Lunch</button>
  <button data-category="Dinner">Dinner</button>
  <button data-category="Desserts">Desserts</button>
  <button data-category="Breads">Breads</button>
  <button data-category="Sauces">Sauces</button>
</nav>

<div class="container">

  <!-- Add Recipe Form -->
  <form id="add-recipe-form">
    <h2>Add a New Recipe</h2>
    <input type="text" id="recipeName" placeholder="Recipe Name" required>
    <select id="category" required>
      <option value="Breakfast">Breakfast</option>
      <option value="Lunch">Lunch</option>
      <option value="Dinner">Dinner</option>
      <option value="Desserts">Desserts</option>
      <option value="Breads">Breads</option>
      <option value="Sauces">Sauces</option>
    </select>
    <textarea id="ingredients" rows="3" placeholder="Ingredients (comma separated, include measurements)" required></textarea>
    <textarea id="instructions" rows="4" placeholder="Instructions (one step per line, include preheat/timing)" required></textarea>
    <button type="submit" class="submit-btn">Add Recipe</button>
  </form>

  <!-- Recipe Grid -->
  <div id="recipe-grid"></div>

  <!-- Notes Section -->
  <form id="notes-form">
    <h2>Add a Note</h2>
    <textarea id="note-input" rows="2" placeholder="Leave a note or comment"></textarea>
    <button type="submit" class="submit-btn">Add Note</button>
  </form>
  <div id="notes-display"></div>

  <!-- AI Recipe Generator -->
  <form id="ai-generator-form">
    <h2>AI Recipe Generator</h2>
    <input type="text" id="ai-input" placeholder='E.g., "Truffle Chicken Pasta"' required>
    <button type="submit" class="submit-btn">Generate Recipe</button>
  </form>
  <div id="ai-output"></div>
</div>

<script>
const recipes = [
  // Example recipes
  {name:"Sourdough Strawberry & Cream French Toast",category:"Breakfast",ingredients:["4 slices sourdough bread","2 eggs","1/2 cup milk","1 tsp vanilla extract","1 cup strawberries, sliced","1/2 cup heavy cream, whipped"],instructions:["Preheat griddle to medium heat.","Whisk eggs, milk, vanilla.","Dip sourdough slices in mixture.","Cook 2-3 min per side until golden.","Top with strawberries and whipped cream."]},
  {name:"Pizza Hut-Style Pan Pizza",category:"Lunch",ingredients:["1 1/4 cups warm water","2 tsp sugar","2 1/4 tsp active dry yeast","2 1/2 cups all-purpose flour","1 tsp salt","4 tbsp olive oil, divided","Toppings of choice"],instructions:["Combine water, sugar, yeast. Sit 5 min.","Mix in flour & salt, knead 5-7 min.","Coat skillet with 2 tbsp olive oil, place dough, rise 1-2 hrs.","Add toppings, drizzle remaining oil.","Bake 450°F 15-20 min."]},
  {name:"Crispy Popeyes-Style Wings",category:"Dinner",ingredients:["2 lbs chicken wings","1 cup buttermilk","1 tbsp Cajun seasoning","2 cups flour","1 tbsp cornstarch","1 tsp paprika","1 tsp garlic powder","Salt & pepper","Oil for frying"],instructions:["Marinate wings in buttermilk & seasoning 4 hrs.","Mix flour, cornstarch, paprika, garlic, salt, pepper.","Dredge wings, fry 350°F 8-10 min."]}
];

const recipeGrid = document.getElementById('recipe-grid');
const tabs = document.querySelectorAll('#category-tabs button');
const addRecipeForm = document.getElementById('add-recipe-form');
const notesForm = document.getElementById('notes-form');
const notesDisplay = document.getElementById('notes-display');
const aiGeneratorForm = document.getElementById('ai-generator-form');
const aiOutput = document.getElementById('ai-output');

function createRecipeCard(recipe){
  const card = document.createElement('div');
  card.classList.add('recipe-card');
  card.innerHTML = `
    <div class="recipe-header">${recipe.name} <span>+</span></div>
    <div class="recipe-content">
      <h4>Ingredients</h4><ul>${recipe.ingredients.map(i=>`<li>${i}</li>`).join('')}</ul>
      <h4>Instructions</h4><ol>${recipe.instructions.map(i=>`<li>${i}</li>`).join('')}</ol>
    </div>
  `;
  card.querySelector('.recipe-header').addEventListener('click',()=>{
    const content = card.querySelector('.recipe-content');
    content.style.display = content.style.display==="block"?"none":"block";
  });
  return card;
}

function displayRecipes(filter="All"){
  recipeGrid.innerHTML="";
  recipes.filter(r=>filter==="All"||r.category===filter).forEach(r=>recipeGrid.appendChild(createRecipeCard(r)));
}

tabs.forEach(tab=>{
  tab.addEventListener('click',()=>{
    tabs.forEach(t=>t.classList.remove('active'));
    tab.classList.add('active');
    displayRecipes(tab.dataset.category);
  });
});

addRecipeForm.addEventListener('submit',e=>{
  e.preventDefault();
  const newRecipe={
    name:document.getElementById('recipeName').value,
    category:document.getElementById('category').value,
    ingredients:document.getElementById('ingredients').value.split(',').map(i=>i.trim()),
    instructions:document.getElementById('instructions').value.split('\n').map(i=>i.trim())
  };
  recipes.push(newRecipe);
  displayRecipes(document.querySelector('#category-tabs button.active').dataset.category);
  addRecipeForm.reset();
});
