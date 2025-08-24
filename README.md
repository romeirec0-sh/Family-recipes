<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Family Cookbook</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Playfair+Display:wght@700&family=Roboto:wght@400;700&display=swap');

        body {
            font-family: 'Roboto', sans-serif;
            margin: 0;
            background-color: #fdfaf6;
            color: #4a4a4a;
        }

        header {
            background-color: #ff7f50; /* Coral */
            color: white;
            padding: 1rem 0;
            text-align: center;
            font-family: 'Playfair Display', serif;
        }

        header h1 {
            margin: 0;
            font-size: 2.5rem;
        }

        nav {
            background-color: #d2b48c; /* Soft Brown */
            padding: 1rem;
            text-align: center;
        }

        .filter-btn {
            background-color: #ff7f50;
            color: white;
            border: none;
            padding: 0.5rem 1rem;
            margin: 0.2rem;
            border-radius: 5px;
            cursor: pointer;
            transition: background-color 0.3s;
        }

        .filter-btn:hover {
            background-color: #e56b3e;
        }

        .container {
            padding: 2rem;
        }

        #recipe-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
            gap: 1.5rem;
        }

        .recipe-card {
            background-color: #fff;
            border-radius: 10px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
            overflow: hidden;
            transition: transform 0.3s, box-shadow 0.3s;
        }

        .recipe-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 8px 16px rgba(0, 0, 0, 0.2);
        }

        .recipe-card h3 {
            background-color: #d2b48c;
            color: white;
            padding: 1rem;
            margin: 0;
        }

        .recipe-card-content {
            padding: 1rem;
        }

        .recipe-card h4 {
            color: #ff7f50;
            border-bottom: 2px solid #ff7f50;
            padding-bottom: 0.5rem;
        }

        .recipe-card ul, .recipe-card ol {
            padding-left: 1.2rem;
        }

        .recipe-card li {
            margin-bottom: 0.5rem;
        }

        .form-section, .notes-section, .ai-generator-section {
            background-color: #fff;
            padding: 2rem;
            margin-top: 2rem;
            border-radius: 10px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        }

        .form-section h2, .notes-section h2, .ai-generator-section h2 {
            font-family: 'Playfair Display', serif;
            color: #ff7f50;
            text-align: center;
        }

        .form-group {
            margin-bottom: 1rem;
        }

        .form-group label {
            display: block;
            margin-bottom: 0.5rem;
        }

        .form-group input, .form-group textarea, .form-group select {
            width: 100%;
            padding: 0.5rem;
            border-radius: 5px;
            border: 1px solid #ccc;
        }

        .submit-btn {
            background-color: #ff7f50;
            color: white;
            border: none;
            padding: 0.7rem 1.5rem;
            border-radius: 5px;
            cursor: pointer;
            transition: background-color 0.3s;
            display: block;
            width: 100%;
        }

        .submit-btn:hover {
            background-color: #e56b3e;
        }

        #notes-display {
            margin-top: 1rem;
            border-top: 1px solid #eee;
            padding-top: 1rem;
        }

        .note {
            background-color: #fdfaf6;
            padding: 1rem;
            border-radius: 5px;
            margin-bottom: 1rem;
        }

        @media (max-width: 768px) {
            #recipe-grid {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>

    <header>
        <h1>Our Family Cookbook</h1>
    </header>

    <nav>
        <button class="filter-btn" data-category="all">All</button>
        <button class="filter-btn" data-category="Breakfast">Breakfast</button>
        <button class="filter-btn" data-category="Lunch">Lunch</button>
        <button class="filter-btn" data-category="Dinner">Dinner</button>
        <button class="filter-btn" data-category="Desserts">Desserts</button>
        <button class="filter-btn" data-category="Breads">Breads</button>
        <button class="filter-btn" data-category="Sauces">Sauces</button>
    </nav>

    <div class="container">
        <div id="recipe-grid"></div>

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
                    <label for="instructions">Instructions (one step per line)</label>
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
    </div>

    <script>
        const recipes = [
            // Breakfast
            {
                name: "Sourdough Strawberry & Cream French Toast",
                category: "Breakfast",
                ingredients: ["4 slices sourdough bread", "2 eggs", "1/2 cup milk", "1 tsp vanilla extract", "1 cup strawberries, sliced", "1/2 cup heavy cream, whipped"],
                instructions: ["Whisk eggs, milk, and vanilla.", "Dip sourdough slices in the mixture.", "Cook on a griddle until golden brown.", "Top with fresh strawberries and whipped cream."],
                notes: "A delightful and elegant breakfast."
            },
            {
                name: "Blueberry Sourdough Pancakes",
                category: "Breakfast",
                ingredients: ["1 cup sourdough starter", "1 cup all-purpose flour", "1 tbsp sugar", "1 tsp baking powder", "1/2 tsp baking soda", "1/2 tsp salt", "1 egg", "1/4 cup milk", "1 cup blueberries"],
                instructions: ["Combine dry ingredients.", "In a separate bowl, mix sourdough starter, egg, and milk.", "Combine wet and dry ingredients.", "Fold in blueberries.", "Cook on a hot griddle."],
                notes: "Tangy and sweet, a perfect combination."
            },
            {
                name: "Fluffy Pancakes",
                category: "Breakfast",
                ingredients: ["1 1/2 cups all-purpose flour", "3 1/2 tsp baking powder", "1 tsp salt", "1 tbsp white sugar", "1 1/4 cups milk", "1 egg", "3 tbsp butter, melted"],
                instructions: ["In a large bowl, sift together the flour, baking powder, salt and sugar.", "Make a well in the center and pour in the milk, egg and melted butter; mix until smooth.", "Heat a lightly oiled griddle or frying pan over medium high heat.", "Pour or scoop the batter onto the griddle, using approximately 1/4 cup for each pancake.", "Brown on both sides and serve hot."],
                notes: "A classic for a reason!"
            },
            {
                name: "Classic Omelette",
                category: "Breakfast",
                ingredients: ["3 eggs", "1 tbsp milk", "Salt and pepper to taste", "1 tbsp butter", "1/2 cup shredded cheese", "Optional fillings: diced ham, bell peppers, onions"],
                instructions: ["Whisk eggs, milk, salt, and pepper.", "Melt butter in a non-stick skillet over medium heat.", "Pour in the egg mixture. Let it set slightly.", "Add cheese and fillings to one half.", "Fold the other half over and cook until the cheese is melted."],
                notes: "Customize with your favorite fillings."
            },
            {
                name: "Perfect French Toast",
                category: "Breakfast",
                ingredients: ["6 thick slices of bread", "2 large eggs", "2/3 cup milk", "1 tsp vanilla extract", "1/4 tsp cinnamon", "Butter for frying"],
                instructions: ["Whisk together eggs, milk, vanilla, and cinnamon.", "Heat butter in a large skillet over medium heat.", "Dip each slice of bread into the egg mixture, ensuring it's coated on both sides but not soggy.", "Fry for 2-3 minutes per side, until golden brown.", "Serve immediately with your favorite toppings."],
                notes: "Use day-old bread for the best results."
            },
            // Lunch
            {
                name: "Pizza Hut-Style Pan Pizza",
                category: "Lunch",
                ingredients: ["1 1/4 cups warm water", "2 tsp sugar", "2 1/4 tsp active dry yeast", "2 1/2 cups all-purpose flour", "1 tsp salt", "4 tbsp olive oil, divided", "Toppings of choice"],
                instructions: ["Combine water, sugar, and yeast. Let it sit for 5 minutes.", "Mix in flour and salt. Knead for 5-7 minutes.", "Coat a 9-inch cast-iron skillet with 2 tbsp of olive oil.", "Place dough in the skillet, cover, and let it rise for 1-2 hours.", "Top with sauce, cheese, and your favorite toppings. Drizzle with remaining olive oil.", "Bake at 450°F (230°C) for 15-20 minutes."],
                notes: "The crispy, oily crust is the star!"
            },
            {
                name: "Gourmet Grilled Cheese",
                category: "Lunch",
                ingredients: ["2 slices of brioche bread", "2 tbsp unsalted butter, softened", "1/2 cup shredded Gruyère cheese", "1/4 cup shredded cheddar cheese", "1 tbsp chopped chives"],
                instructions: ["Butter one side of each slice of bread.", "On the unbuttered side of one slice, layer the cheeses and chives.", "Top with the other slice of bread, butter-side-up.", "Grill in a non-stick skillet over medium heat for 3-4 minutes per side, until golden brown and the cheese is melted."],
                notes: "A sophisticated take on a childhood favorite."
            },
            {
                name: "Truffle Mac & Cheese",
                category: "Lunch",
                ingredients: ["1 lb elbow macaroni", "4 tbsp butter", "1/4 cup all-purpose flour", "3 cups milk", "1 cup shredded Gruyère cheese", "1 cup shredded sharp cheddar cheese", "2 tbsp truffle oil", "Salt and pepper to taste"],
                instructions: ["Cook macaroni according to package directions.", "In a large saucepan, melt butter. Whisk in flour and cook for 1 minute.", "Gradually whisk in milk until smooth. Cook until thickened.", "Remove from heat and stir in cheeses until melted. Stir in truffle oil, salt, and pepper.", "Add the cooked macaroni and stir to coat."],
                notes: "An indulgent and flavorful dish."
            },
            {
                name: "Classic Chicken Salad",
                category: "Lunch",
                ingredients: ["2 cups cooked, shredded chicken", "1/2 cup mayonnaise", "1/4 cup diced celery", "2 tbsp chopped red onion", "1 tbsp lemon juice", "Salt and pepper to taste"],
                instructions: ["In a medium bowl, combine all ingredients.", "Mix well.", "Serve on bread, in a croissant, or over a bed of lettuce."],
                notes: "Simple, yet satisfying."
            },
            {
                name: "Pasta Primavera",
                category: "Lunch",
                ingredients: ["12 oz penne pasta", "1 tbsp olive oil", "1 cup broccoli florets", "1 cup sliced carrots", "1 cup sliced bell peppers", "1/2 cup frozen peas", "2 cloves garlic, minced", "1/2 cup heavy cream", "1/4 cup grated Parmesan cheese", "Salt and pepper to taste"],
                instructions: ["Cook pasta according to package directions.", "While pasta is cooking, heat olive oil in a large skillet. Add broccoli, carrots, and bell peppers. Cook until tender-crisp.", "Add peas and garlic, cook for 1 minute more.", "Stir in heavy cream and Parmesan cheese. Season with salt and pepper.", "Drain pasta and add to the skillet. Toss to coat."],
                notes: "A fresh and vibrant pasta dish."
            },
            // Dinner
            {
                name: "Crispy Popeyes-Style Wings",
                category: "Dinner",
                ingredients: ["2 lbs chicken wings", "1 cup buttermilk", "1 tbsp Cajun seasoning", "2 cups all-purpose flour", "1 tbsp cornstarch", "1 tsp paprika", "1 tsp garlic powder", "Salt and pepper to taste", "Oil for frying"],
                instructions: ["Marinate wings in buttermilk and Cajun seasoning for at least 4 hours.", "In a separate bowl, combine flour, cornstarch, paprika, garlic powder, salt, and pepper.", "Dredge each wing in the flour mixture, ensuring it's fully coated.", "Fry in oil at 350°F (175°C) for 8-10 minutes, until golden brown and cooked through."],
                notes: "Serve with your favorite dipping sauces."
            },
            {
                name: "Garlic Butter Chicken",
                category: "Dinner",
                ingredients: ["4 boneless, skinless chicken breasts", "4 tbsp butter, melted", "4 cloves garlic, minced", "1 tsp dried oregano", "1 tsp dried parsley", "Salt and pepper to taste"],
                instructions: ["Preheat oven to 400°F (200°C).", "In a small bowl, combine melted butter, garlic, oregano, parsley, salt, and pepper.", "Place chicken in a baking dish and pour the garlic butter mixture over the top.", "Bake for 20-25 minutes, or until chicken is cooked through."],
                notes: "A simple and flavorful weeknight meal."
            },
            {
                name: "Lemon Herb Salmon",
                category: "Dinner",
                ingredients: ["4 (6 oz) salmon fillets", "2 tbsp olive oil", "2 cloves garlic, minced", "1 tsp dried thyme", "1 tsp dried rosemary", "Zest and juice of 1 lemon", "Salt and pepper to taste"],
                instructions: ["Preheat oven to 400°F (200°C).", "In a small bowl, combine olive oil, garlic, thyme, rosemary, lemon zest, and lemon juice.", "Place salmon on a baking sheet and brush with the lemon herb mixture. Season with salt and pepper.", "Bake for 12-15 minutes, or until salmon is cooked through."],
                notes: "Light, healthy, and delicious."
            },
            {
                name: "Truffle Mushroom Risotto",
                category: "Dinner",
                ingredients: ["1 tbsp olive oil", "1 shallot, finely chopped", "8 oz mushrooms, sliced", "1 1/2 cups Arborio rice", "1/2 cup dry white wine", "4 cups warm vegetable broth", "1/2 cup grated Parmesan cheese", "2 tbsp truffle oil", "Salt and pepper to taste"],
                instructions: ["In a large skillet, heat olive oil. Add shallot and cook until softened. Add mushrooms and cook until browned.", "Stir in Arborio rice and cook for 1 minute.", "Pour in white wine and cook until absorbed.", "Add vegetable broth, one ladle at a time, stirring constantly until each addition is absorbed before adding the next.", "Once the rice is cooked, stir in Parmesan cheese and truffle oil. Season with salt and pepper."],
                notes: "A creamy and decadent dish."
            },
            {
                name: "Carrot Cake Sourdough Casserole",
                category: "Dinner",
                ingredients: ["6 cups sourdough bread, cubed", "1 1/2 cups shredded carrots", "1/2 cup raisins", "1/2 cup chopped walnuts", "4 eggs", "2 cups milk", "1/2 cup brown sugar", "1 tsp cinnamon", "1/2 tsp nutmeg"],
                instructions: ["Preheat oven to 350°F (175°C).", "In a large bowl, combine sourdough bread cubes, shredded carrots, raisins, and walnuts.", "In a separate bowl, whisk together eggs, milk, brown sugar, cinnamon, and nutmeg.", "Pour the egg mixture over the bread mixture and stir to combine.", "Pour into a greased 9x13 inch baking dish.", "Bake for 45-50 minutes, or until a knife inserted into the center comes out clean."],
                notes: "A unique and delicious savory casserole."
            },
            // Desserts
            {
                name: "Mango Cheesecake Cobbler",
                category: "Desserts",
                ingredients: ["For the filling: 2 cups diced mango", "1/4 cup sugar", "1 tbsp cornstarch", "For the cheesecake layer: 8 oz cream cheese, softened", "1/4 cup sugar", "1 egg", "For the cobbler topping: 1 cup all-purpose flour", "1/2 cup sugar", "1 tsp baking powder", "1/4 cup cold butter, cubed", "1/4 cup milk"],
                instructions: ["Preheat oven to 375°F (190°C).", "In a saucepan, combine filling ingredients and cook until thickened. Pour into a baking dish.", "In a bowl, beat cheesecake layer ingredients until smooth. Spread over the mango filling.", "In another bowl, combine flour, sugar, and baking powder. Cut in butter until the mixture resembles coarse crumbs. Stir in milk to form a dough.", "Drop spoonfuls of dough over the cheesecake layer.", "Bake for 25-30 minutes, or until the topping is golden brown."],
                notes: "A tropical twist on a classic dessert."
            },
            {
                name: "Chocolate Lava Cake",
                category: "Desserts",
                ingredients: ["4 oz semi-sweet chocolate, chopped", "1/2 cup unsalted butter", "2 large eggs", "2 large egg yolks", "1/4 cup sugar", "2 tbsp all-purpose flour"],
                instructions: ["Preheat oven to 450°F (230°C). Grease and flour 4 ramekins.", "In a microwave-safe bowl, melt chocolate and butter together.", "In a separate bowl, whisk together eggs, egg yolks, and sugar until pale and thick.", "Fold the chocolate mixture into the egg mixture. Fold in the flour.", "Divide the batter among the prepared ramekins.", "Bake for 10-12 minutes, until the edges are firm and the center is soft.", "Let cool for 1 minute before inverting onto plates."],
                notes: "Serve immediately with a dusting of powdered sugar or a scoop of vanilla ice cream."
            },
            {
                name: "Ube Cream Cheese Danish",
                category: "Desserts",
                ingredients: ["1 sheet of puff pastry, thawed", "4 oz cream cheese, softened", "1/4 cup powdered sugar", "1/4 cup ube halaya (purple yam jam)"],
                instructions: ["Preheat oven to 400°F (200°C).", "Cut the puff pastry into 6 rectangles.", "In a bowl, beat cream cheese and powdered sugar until smooth.", "Spread the cream cheese mixture onto the center of each pastry rectangle.", "Top with a spoonful of ube halaya.", "Bake for 15-20 minutes, or until golden brown and puffed."],
                notes: "A beautiful and delicious pastry."
            },
            {
                name: "Strawberry Shortcake",
                category: "Desserts",
                ingredients: ["2 cups all-purpose flour", "1/4 cup sugar", "2 tsp baking powder", "1/2 tsp salt", "1/2 cup cold butter, cubed", "2/3 cup milk", "1 lb strawberries, sliced", "1/4 cup sugar", "1 cup heavy cream, whipped"],
                instructions: ["Preheat oven to 425°F (220°C).", "In a large bowl, combine flour, sugar, baking powder, and salt. Cut in butter until the mixture resembles coarse crumbs.", "Stir in milk to form a soft dough.", "Drop spoonfuls onto a baking sheet.", "Bake for 12-15 minutes, until golden brown.", "While the shortcakes are baking, combine strawberries and sugar in a bowl and let sit for 15 minutes.", "Split the warm shortcakes, and spoon strawberries and whipped cream over the bottom halves. Replace the tops and add more strawberries and cream."],
                notes: "A classic summer dessert."
            },
            {
                name: "Classic Lemon Tart",
                category: "Desserts",
                ingredients: ["1 pre-baked 9-inch tart shell", "4 large eggs", "1 cup granulated sugar", "1/2 cup fresh lemon juice", "1/4 cup all-purpose flour", "Zest of 1 lemon"],
                instructions: ["Preheat oven to 350°F (175°C).", "In a medium bowl, whisk together eggs and sugar until light and fluffy.", "Stir in lemon juice, flour, and lemon zest. Mix until well combined.", "Pour the filling into the pre-baked tart shell.", "Bake for 30-35 minutes, or until the center is set.", "Let cool completely before serving."],
                notes: "A bright and tangy dessert."
            },
            // Breads
            {
                name: "Soft Sandwich Loaf",
                category: "Breads",
                ingredients: ["1 cup warm milk", "2 tbsp sugar", "2 1/4 tsp active dry yeast", "3 cups all-purpose flour", "1 tsp salt", "3 tbsp unsalted butter, softened"],
                instructions: ["In a small bowl, combine warm milk, sugar, and yeast. Let it sit for 5 minutes.", "In a large bowl, combine flour and salt.", "Add the yeast mixture and softened butter to the flour mixture. Mix until a dough forms.", "Knead for 8-10 minutes, until smooth and elastic.", "Place in a greased bowl, cover, and let rise for 1-2 hours, or until doubled in size.", "Punch down the dough and shape it into a loaf. Place in a greased loaf pan.", "Cover and let rise for another 30-45 minutes.", "Bake at 375°F (190°C) for 30-35 minutes, until golden brown."],
                notes: "Perfect for sandwiches or toast."
            },
            {
                name: "Cinnamon Sourdough Rolls",
                category: "Breads",
                ingredients: ["For the dough: 1/2 cup active sourdough starter", "1/2 cup milk", "1/4 cup sugar", "1 egg", "2 1/2 cups all-purpose flour", "1 tsp salt", "1/4 cup unsalted butter, softened", "For the filling: 1/2 cup brown sugar", "2 tbsp cinnamon", "1/4 cup unsalted butter, softened"],
                instructions: ["In a large bowl, combine all dough ingredients. Knead for 10-12 minutes.", "Place in a greased bowl, cover, and let it rise for 4-6 hours.", "Roll the dough into a large rectangle. Spread with softened butter and sprinkle with the brown sugar and cinnamon mixture.", "Roll up the dough tightly and slice into 12 rolls.", "Place in a greased baking dish, cover, and let rise for another 2-3 hours.", "Bake at 375°F (190°C) for 20-25 minutes."],
                notes: "A tangy and sweet twist on a classic."
            },
            {
                name: "Herb Focaccia",
                category: "Breads",
                ingredients: ["1 1/2 cups warm water", "2 tsp sugar", "2 1/4 tsp active dry yeast", "3 1/2 cups all-purpose flour", "2 tsp salt", "1/4 cup olive oil, plus more for drizzling", "Fresh herbs (rosemary, thyme)", "Coarse sea salt"],
                instructions: ["Combine warm water, sugar, and yeast. Let it sit for 5 minutes.", "In a large bowl, combine flour and salt. Add the yeast mixture and olive oil.", "Mix until a dough forms. Knead for 5 minutes.", "Place in a greased bowl, cover, and let it rise for 1 hour.", "Press the dough into a greased baking sheet. Drizzle with olive oil and dimple the surface with your fingers.", "Sprinkle with fresh herbs and coarse sea salt.", "Let it rise for another 20 minutes.", "Bake at 425°F (220°C) for 20-25 minutes."],
                notes: "A flavorful and aromatic bread."
            },
            {
                name: "Brioche Loaf",
                category: "Breads",
                ingredients: ["1/2 cup warm milk", "2 1/4 tsp active dry yeast", "3 tbsp sugar", "3 1/2 cups all-purpose flour", "1 tsp salt", "4 large eggs", "1 cup unsalted butter, softened and cubed"],
                instructions: ["In a small bowl, combine warm milk, yeast, and 1 tbsp of sugar. Let sit for 5 minutes.", "In a large bowl, combine flour, remaining sugar, and salt. Add the yeast mixture and eggs. Mix until a shaggy dough forms.", "Gradually add the softened butter, a few cubes at a time, kneading until fully incorporated.", "Knead for 10-15 minutes, until the dough is smooth and elastic.", "Place in a greased bowl, cover, and refrigerate overnight.", "The next day, shape the dough into a loaf and place it in a greased loaf pan. Let it rise for 1-2 hours.", "Bake at 350°F (175°C) for 30-40 minutes."],
                notes: "A rich and buttery bread."
            },
            {
                name: "Rustic Olive Bread",
                category: "Breads",
                ingredients: ["3 cups all-purpose flour", "1 1/2 tsp salt", "1/2 tsp active dry yeast", "1 1/2 cups warm water", "1 cup Kalamata olives, pitted and roughly chopped"],
                instructions: ["In a large bowl, combine flour, salt, and yeast.", "Add warm water and mix until a shaggy dough forms.", "Fold in the olives.", "Cover the bowl and let it rise for 12-18 hours.", "The next day, preheat the oven and a Dutch oven to 450°F (230°C).", "Shape the dough into a ball and place it in the preheated Dutch oven.", "Bake, covered, for 30 minutes. Remove the lid and bake for another 15-20 minutes."],
                notes: "A no-knead bread with a chewy crust."
            },
            // Sauces
            {
                name: "Classic Buffalo Sauce",
                category: "Sauces",
                ingredients: ["1/2 cup hot sauce (e.g., Frank's RedHot)", "1/3 cup unsalted butter, melted", "1 1/2 tbsp white vinegar", "1/4 tsp Worcestershire sauce", "1/4 tsp cayenne pepper", "1/8 tsp garlic powder"],
                instructions: ["In a small bowl, whisk together all ingredients until well combined."],
                notes: "Perfect for wings, sandwiches, or as a dipping sauce."
            },
            {
                name: "Parmesan Garlic Sauce",
                category: "Sauces",
                ingredients: ["1/2 cup unsalted butter, melted", "4 cloves garlic, minced", "1/2 cup grated Parmesan cheese", "1 tbsp chopped fresh parsley", "Salt and pepper to taste"],
                instructions: ["In a small bowl, combine all ingredients and mix well."],
                notes: "A rich and savory sauce for wings, bread, or pasta."
            },
            {
                name: "Classic Tomato Sauce",
                category: "Sauces",
                ingredients: ["2 tbsp olive oil", "1 onion, chopped", "2 cloves garlic, minced", "1 (28 oz) can crushed tomatoes", "1 tsp dried oregano", "1 tsp dried basil", "Salt and pepper to taste"],
                instructions: ["In a large saucepan, heat olive oil over medium heat. Add onion and cook until softened.", "Add garlic and cook for 1 minute more.", "Stir in crushed tomatoes, oregano, and basil. Season with salt and pepper.", "Bring to a simmer and cook for at least 30 minutes, stirring occasionally."],
                notes: "A versatile sauce for pasta, pizza, and more."
            },
            {
                name: "Truffle Aioli",
                category: "Sauces",
                ingredients: ["1 cup mayonnaise", "2 cloves garlic, minced", "2 tbsp truffle oil", "1 tbsp lemon juice", "Salt and pepper to taste"],
                instructions: ["In a small bowl, combine all ingredients and mix until well combined.", "Let it sit for at least 30 minutes for the flavors to meld."],
                notes: "An elegant and flavorful aioli for fries, sandwiches, or as a dip."
            },
            {
                name: "Honey Mustard",
                category: "Sauces",
                ingredients: ["1/2 cup Dijon mustard", "1/4 cup honey", "2 tbsp mayonnaise", "1 tbsp apple cider vinegar"],
                instructions: ["In a small bowl, whisk together all ingredients until smooth."],
                notes: "A sweet and tangy sauce for chicken, pretzels, or salads."
            }
        ];

        const recipeGrid = document.getElementById('recipe-grid');
        const filterBtns = document.querySelectorAll('.filter-btn');
        const addRecipeForm = document.getElementById('add-recipe-form');
        const notesForm = document.getElementById('notes-form');
        const notesDisplay = document.getElementById('notes-display');
        const aiGeneratorForm = document.getElementById('ai-generator-form');
        const aiOutput = document.getElementById('ai-output');

        function displayRecipes(filteredRecipes) {
            recipeGrid.innerHTML = '';
            filteredRecipes.forEach(recipe => {
                const recipeCard = document.createElement('div');
                recipeCard.classList.add('recipe-card');
                recipeCard.innerHTML = `
                    <h3>${recipe.name}</h3>
                    <div class="recipe-card-content">
                        <h4>Ingredients</h4>
                        <ul>
                            ${recipe.ingredients.map(ing => `<li>${ing}</li>`).join('')}
                        </ul>
                        <h4>Instructions</h4>
                        <ol>
                            ${recipe.instructions.map(inst => `<li>${inst}</li>`).join('')}
                        </ol>
                        ${recipe.notes ? `<p><strong>Notes:</strong> ${recipe.notes}</p>` : ''}
                    </div>
                `;
                recipeGrid.appendChild(recipeCard);
            });
        }

        displayRecipes(recipes);

        filterBtns.forEach(btn => {
            btn.addEventListener('click', () => {
                const category = btn.dataset.category;
                if (category === 'all') {
                    displayRecipes(recipes);
                } else {
                    const filteredRecipes = recipes.filter(recipe => recipe.category === category);
                    displayRecipes(filteredRecipes);
                }
            });
        });

        addRecipeForm.addEventListener('submit', (e) => {
            e.preventDefault();
            const newRecipe = {
                name: document.getElementById('recipeName').value,
                category: document.getElementById('category').value,
                ingredients: document.getElementById('ingredients').value.split(',').map(item => item.trim()),
                instructions: document.getElementById('instructions').value.split('\n').map(item => item.trim()),
                notes: ''
            };
            recipes.push(newRecipe);
            displayRecipes(recipes);
            addRecipeForm.reset();
        });

        notesForm.addEventListener('submit', (e) => {
            e.preventDefault();
            const noteInput = document.getElementById('note-input');
            const noteText = noteInput.value;
            const noteElement = document.createElement('div');
            noteElement.classList.add('note');
            noteElement.textContent = noteText;
            notesDisplay.appendChild(noteElement);
            noteInput.value = '';
        });

        aiGeneratorForm.addEventListener('submit', (e) => {
            e.preventDefault();
            const idea = document.getElementById('ai-input').value;
            aiOutput.innerHTML = `
                <div class="recipe-card">
                    <h3>Generated Recipe: ${idea}</h3>
                    <div class="recipe-card-content">
                        <h4>Ingredients</h4>
                        <ul>
                            <li>1 lb Chicken Breast, cubed</li>
                            <li>8 oz Pasta (e.g., Fettuccine)</li>
                            <li>1 cup Heavy Cream</li>
                            <li>1/2 cup Grated Parmesan</li>
                            <li>2 tbsp Truffle Oil</li>
                            <li>2 cloves Garlic, minced</li>
                            <li>Salt and Pepper to taste</li>
                        </ul>
                        <h4>Instructions</h4>
                        <ol>
                            <li>Cook pasta according to package directions.</li>
                            <li>Season chicken with salt and pepper. Sauté until golden brown.</li>
                            <li>In a separate pan, sauté garlic. Add heavy cream and bring to a simmer.</li>
                            <li>Stir in Parmesan cheese until melted. Add truffle oil.</li>
                            <li>Combine pasta, chicken, and sauce. Serve immediately.</li>
                        </ol>
                    </div>
                </div>
            `;
        });
    </script>
</body>
</html>
