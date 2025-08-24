# Family-recipes

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Family Recipe Generator</title>
    <style>
        /* Add your CSS styles here */
    </style>
</head>
<body>
    <h1>Family Recipe Generator</h1>
    <input type="text" id="recipeIdea" placeholder="Enter a recipe idea">
    <button onclick="generateRecipe()">Generate Recipe</button>
    <div id="generatedRecipe"></div>
    <h2>Saved Recipes</h2>
    <div id="recipeLibrary"></div>

    <script>
        const GEMINI_API_KEY = 'YOUR_API_KEY_HERE'; // Replace with your Gemini 2.5 Pro API key
        let recipeLibrary = [];

        async function generateRecipe() {
            const idea = document.getElementById('recipeIdea').value.trim();
            if (!idea) {
                alert("Please enter a recipe idea.");
                return;
            }

            const prompt = `You are a friendly, creative, and detailed chef assistant. Create a full recipe based on this idea: "${idea}". Output should include: Title, Description, Ingredients with measurements, Step-by-step instructions (include timing, preheat, marinate, bake, rest), Notes/Options (substitutions, tips, variations)`;

            try {
                const response = await fetch('https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-pro:generateContent', {
                    method: 'POST',
                    headers: {
                        'Authorization': `Bearer ${GEMINI_API_KEY}`,
                        'Content-Type': 'application/json'
                    },
                    body: JSON.stringify({
                        contents: [{ text: prompt }]
                    })
                });

                const data = await response.json();
                const aiText = data.output_text || data.text || "Failed to generate recipe.";

                const recipe = parseRecipe(aiText);
                displayGeneratedRecipe(recipe);
            } catch (err) {
                console.error(err);
                alert("Error generating recipe. Please try again.");
            }
        }

        function parseRecipe(text) {
            const lines = text.split("\n").filter(line => line.trim() !== "");
            const recipe = { title: "", description: "", ingredients: [], instructions: [], notes: [] };

            lines.forEach(line => {
                if (line.toLowerCase().startsWith("title:")) recipe.title = line.split(":")[1].trim();
                else if (line.toLowerCase().startsWith("description:")) recipe.description = line.split(":")[1].trim();
                else if (line.toLowerCase().startsWith("ingredients:")) recipe.ingredients.push(line.split(":")[1].trim());
                else if (line.toLowerCase().startsWith("instructions:")) recipe.instructions.push(line.split(":")[1].trim());
                else if (line.toLowerCase().startsWith("notes:")) recipe.notes.push(line.split(":")[1].trim());
                else recipe.notes.push(line.trim());
            });

            if (!recipe.title) recipe.title = "Generated Recipe";
            if (!recipe.description) recipe.description = "A delicious recipe generated from your idea.";
            if (recipe.ingredients.length === 0) recipe.ingredients = ["1 cup example ingredient", "2 tsp example spice"];
            if (recipe.instructions.length === 0) recipe.instructions = ["Step 1: Do something", "Step 2: Do next thing"];
            return recipe;
        }

        function displayGeneratedRecipe(recipe) {
            const container = document.getElementById('generatedRecipe');
            container.innerHTML = `
                <div class="recipe">
                    <h3>${recipe.title}</h3>
                    <p><em>${recipe.description}</em></p>
                    <strong>Ingredients:</strong><ul>${recipe.ingredients.map(i => `<li>${i}</li>`).join('')}</ul>
                    <strong>Instructions:</strong><ol>${recipe.instructions.map(s => `<li>${s}</li>`).join('')}</ol>
                    <strong>Notes/Options:</strong><ul>${recipe.notes.map(n => `<li>${n}</li>`).join('')}</ul>
                    <button onclick='saveRecipe(${JSON.stringify(recipe)})'>Save Recipe</button>
                </div>`;
        }

        function saveRecipe(recipe) {
            recipeLibrary.push(recipe);
            displayLibrary();
        }

        function displayLibrary() {
            const container = document.getElementById('recipeLibrary');
            container.innerHTML = recipeLibrary.map((r, i) => `
                <div class="recipe">
                    <h4>${r.title}</h4>
                    <p><em>${r.description}</em></p>
                    <button onclick='removeRecipe(${i})'>Remove</button>
                </div>
            `).join('');
        }

        function removeRecipe(index) {
            recipeLibrary.splice(index, 1);
            displayLibrary();
        }
    </script>
</body>
</html>
