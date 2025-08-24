<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Our Family Cookbook</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Playfair+Display:wght@700&family=Roboto:wght@400;700&display=swap');

        body {
            font-family: 'Roboto', sans-serif;
            margin: 0;
            background-color: #fff;
            color: #222;
        }

        header {
            background-color: #000;
            color: #fff;
            text-align: center;
            padding: 1.5rem 0;
            font-family: 'Playfair Display', serif;
        }

        header h1 {
            margin: 0;
            font-size: 2rem;
        }

        nav {
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            background-color: #f5f5f5;
        }

        .tab-btn {
            background-color: #fff;
            color: #000;
            border: 2px solid #000;
            padding: 0.5rem 1rem;
            margin: 0.2rem;
            border-radius: 5px;
            cursor: pointer;
            font-weight: bold;
            transition: all 0.2s;
        }

        .tab-btn.active {
            background-color: #ff0000;
            color: #fff;
            border-color: #ff0000;
        }

        .container {
            max-width: 1000px;
            margin: 0 auto;
            padding: 1rem;
        }

        .form-section, .notes-section, .ai-generator-section {
            background-color: #fff;
            padding: 1rem;
            margin-bottom: 1rem;
            border: 2px solid #000;
            border-radius: 10px;
        }

        .form-section h2, .notes-section h2, .ai-generator-section h2 {
            font-family: 'Playfair Display', serif;
            color: #ff0000;
            text-align: center;
        }

        .form-group {
            margin-bottom: 0.8rem;
        }

        .form-group input, .form-group textarea, .form-group select {
            width: 100%;
            padding: 0.5rem;
            border-radius: 5px;
            border: 1px solid #ccc;
        }

        .submit-btn {
            background-color: #ff0000;
            color: #fff;
            border: none;
            padding: 0.7rem 1rem;
            border-radius: 5px;
            cursor: pointer;
            font-weight: bold;
            width: 100%;
        }

        .recipe-tab {
            display: none;
            flex-direction: column;
            gap: 1rem;
        }

        .recipe-card {
            border: 2px solid #000;
            border-radius: 10px;
            padding: 1rem;
            background-color: #f9f9f9;
        }

        .recipe-card h3 {
            margin-top: 0;
            font-family: 'Playfair Display', serif;
            color: #ff0000;
        }

        .recipe-card ul, .recipe-card ol {
            padding-left: 1.2rem;
        }

        .note {
            border: 1px solid #000;
            border-radius: 5px;
            padding: 0.5rem;
            margin-bottom: 0.5rem;
            background-color: #fff;
        }

        @media (max-width: 768px) {
            nav {
                flex-direction: column;
            }
        }
    </style>
</head>
<body>
    <header>
        <h1>Our Family Cookbook</h1>
    </header>

    <nav>
        <button class="tab-btn active" data-tab="Breakfast">Breakfast</button>
        <button class="tab-btn" data-tab="Lunch">Lunch</button>
        <button class="tab-btn" data-tab="Dinner">Dinner</button>
        <button class="tab-btn" data-tab="Desserts">Desserts</button>
        <button class="tab-btn" data-tab="Breads">Breads</button>
        <button class="tab-btn" data-tab="Sauces">Sauces</button>
    </nav>

    <div class="container">

        <div class="form-section">
            <h2>Add a New Recipe</h2>
            <form id="add-recipe-form">
                <div class="form-group">
                    <label for="recipeName">Recipe Name</label>
                    <input type="text" id="recipeName" required>
                </div>
                <div class="form-group">
                    <label for="ingredients">Ingredients (comma separated)</label>
                    <textarea id="ingredients" rows="4" required></textarea>
                </div>
                <div class="form-group">
                    <label for="instructions">Instructions (one step per line, include measurements & preheating)</label>
                    <textarea id="instructions" rows="6" required></textarea>
                </div>
                <div class="form-group">
                    <label for="category">Category</label>
                    <select id="category" required>
                        <option value="Breakfast">Breakfast</option>
                        <option value="Lunch">Lunch</option>
                        <option value="Dinner">Dinner</option>
                        <option value="Desserts">Desserts</option>
                        <option value="Breads">Breads</option>
                        <option value="Sauces">Sauces</option>
                    </select>
                </div>
                <button type="submit" class="submit-btn">Add Recipe</button>
            </form>
        </div>

        <div class="notes-section">
            <h2>Notes / Comments</h2>
            <form id="notes-form">
                <div class="form-group">
                    <label for="note-input">Leave a note or suggestion</label>
                    <textarea id="note-input" rows="4" required></textarea>
                </div>
                <button type="submit" class="submit-btn">Add Note</button>
            </form>
            <div id="notes-display"></div>
        </div>

        <div class="ai-generator-section">
            <h2>AI Recipe Generator</h2>
            <form id="ai-generator-form">
                <div class="form-group">
                    <label for="ai-input">Enter an idea (e.g., "Truffle Chicken Pasta")</label>
                    <input type="text" id="ai-input" required>
                </div>
                <button type="submit" class="submit-btn">Generate Recipe</button>
            </form>
            <div id="ai-output"></div>
        </div>

        <!-- Recipe Tabs -->
        <div id="Breakfast" class="recipe-tab"></div>
        <div id="Lunch" class="recipe-tab"></div>
        <div id="Dinner" class="recipe-tab"></div>
        <div id="Desserts" class="recipe-tab"></div>
        <div id="Breads" class="recipe-tab"></div>
        <div id="Sauces" class="recipe-tab"></div>

    </div>

<script>
    const recipes = []; // Add your recipes here (name, category, ingredients, instructions, notes)

    const tabButtons = document.querySelectorAll('.tab-btn');
    const tabs = document.querySelectorAll('.recipe-tab');

    function displayTab(category) {
        tabs.forEach(tab => tab.style.display = 'none');
        const currentTab = document.getElementById(category);
        currentTab.style.display = 'flex';
        currentTab.innerHTML = '';
        const filtered = recipes.filter(r => r.category === category);
        filtered.forEach(recipe => {
            const card = document.createElement('div');
            card.classList.add('recipe-card');
            card.innerHTML = `
                <h3>${recipe.name}</h3>
                <h4>Ingredients</h4>
                <ul>${recipe.ingredients.map(i => `<li>${i}</li>`).join('')}</ul>
                <h4>Instructions</h4>
                <ol>${recipe.instructions.map(i => `<li>${i}</li>`).join('')}</ol>
                ${recipe.notes ? `<p><strong>Notes:</strong> ${recipe.notes}</p>` : ''}
            `;
            currentTab.appendChild(card);
        });
    }

    tabButtons.forEach(btn => {
        btn.addEventListener('click', () => {
            tabButtons.forEach(b => b.classList.remove('active'));
            btn.classList.add('active');
            displayTab(btn.dataset.tab);
        });
    });

    // Show Breakfast by default
    displayTab('Breakfast');

    // Add new recipe
    document.getElementById('add-recipe-form').addEventListener('submit', e => {
        e.preventDefault();
        const newRecipe = {
            name: document.getElementById('recipeName').value,
