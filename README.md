<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Healthy Food Guide</title>
    <link rel="manifest" href="manifest.json">
    <meta name="theme-color" content="#4ade80">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Arial', sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            color: #333;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }

        .header {
            text-align: center;
            margin-bottom: 30px;
            color: white;
        }

        .header h1 {
            font-size: 2.5rem;
            margin-bottom: 10px;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
        }

        .nav {
            display: flex;
            justify-content: center;
            gap: 10px;
            margin-bottom: 30px;
            flex-wrap: wrap;
        }

        .nav-btn {
            background: rgba(255,255,255,0.2);
            border: 2px solid rgba(255,255,255,0.3);
            color: white;
            padding: 12px 24px;
            border-radius: 25px;
            cursor: pointer;
            transition: all 0.3s ease;
            backdrop-filter: blur(10px);
        }

        .nav-btn:hover, .nav-btn.active {
            background: rgba(255,255,255,0.3);
            border-color: rgba(255,255,255,0.5);
            transform: translateY(-2px);
        }

        .content-section {
            display: none;
            background: rgba(255,255,255,0.95);
            border-radius: 20px;
            padding: 30px;
            box-shadow: 0 20px 40px rgba(0,0,0,0.1);
            backdrop-filter: blur(20px);
        }

        .content-section.active {
            display: block;
            animation: fadeIn 0.5s ease-in;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .search-bar {
            width: 100%;
            padding: 15px;
            border: 2px solid #e5e7eb;
            border-radius: 12px;
            font-size: 16px;
            margin-bottom: 20px;
            transition: border-color 0.3s ease;
        }

        .search-bar:focus {
            outline: none;
            border-color: #4ade80;
        }

        .food-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
            gap: 20px;
            margin-top: 20px;
        }

        .food-card {
            background: white;
            border-radius: 15px;
            padding: 20px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
            transition: transform 0.3s ease, box-shadow 0.3s ease;
            border-left: 5px solid #4ade80;
        }

        .food-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 30px rgba(0,0,0,0.15);
        }

        .food-name {
            font-size: 1.4rem;
            font-weight: bold;
            color: #1f2937;
            margin-bottom: 10px;
        }

        .food-category {
            background: #4ade80;
            color: white;
            padding: 4px 12px;
            border-radius: 20px;
            font-size: 0.8rem;
            display: inline-block;
            margin-bottom: 10px;
        }

        .nutrition-info {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 10px;
            margin: 15px 0;
        }

        .nutrition-item {
            background: #f3f4f6;
            padding: 8px 12px;
            border-radius: 8px;
            text-align: center;
        }

        .nutrition-label {
            font-size: 0.8rem;
            color: #6b7280;
        }

        .nutrition-value {
            font-weight: bold;
            color: #1f2937;
        }

        .benefits {
            margin-top: 15px;
            padding: 15px;
            background: #f0fdf4;
            border-radius: 10px;
            border-left: 4px solid #22c55e;
        }

        .benefits h4 {
            color: #15803d;
            margin-bottom: 8px;
        }

        .meal-planner {
            display: grid;
            grid-template-columns: repeat(7, 1fr);
            gap: 15px;
            margin-top: 20px;
        }

        .day-card {
            background: white;
            border-radius: 12px;
            padding: 15px;
            box-shadow: 0 3px 10px rgba(0,0,0,0.1);
            text-align: center;
        }

        .day-header {
            font-weight: bold;
            color: #4ade80;
            margin-bottom: 10px;
            border-bottom: 2px solid #f3f4f6;
            padding-bottom: 5px;
        }

        .meal-item {
            background: #f8fafc;
            margin: 5px 0;
            padding: 8px;
            border-radius: 6px;
            font-size: 0.9rem;
        }

        .recipe-card {
            background: white;
            border-radius: 15px;
            padding: 25px;
            margin-bottom: 20px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
        }

        .recipe-title {
            font-size: 1.6rem;
            font-weight: bold;
            color: #1f2937;
            margin-bottom: 15px;
        }

        .recipe-meta {
            display: flex;
            gap: 20px;
            margin-bottom: 15px;
            flex-wrap: wrap;
        }

        .recipe-meta span {
            background: #e5e7eb;
            padding: 6px 12px;
            border-radius: 15px;
            font-size: 0.9rem;
        }

        .ingredients, .instructions {
            margin: 20px 0;
        }

        .ingredients h4, .instructions h4 {
            color: #4ade80;
            margin-bottom: 10px;
        }

        .ingredients ul {
            list-style: none;
            padding-left: 0;
        }

        .ingredients li {
            padding: 5px 0;
            border-bottom: 1px solid #f3f4f6;
        }

        .instructions ol {
            padding-left: 20px;
        }

        .instructions li {
            margin: 10px 0;
            line-height: 1.6;
        }

        .stats-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 20px;
            margin-bottom: 30px;
        }

        .stat-card {
            background: white;
            padding: 20px;
            border-radius: 12px;
            text-align: center;
            box-shadow: 0 3px 10px rgba(0,0,0,0.1);
        }

        .stat-number {
            font-size: 2rem;
            font-weight: bold;
            color: #4ade80;
        }

        .stat-label {
            color: #6b7280;
            margin-top: 5px;
        }

        @media (max-width: 768px) {
            .container {
                padding: 10px;
            }
            
            .header h1 {
                font-size: 2rem;
            }
            
            .meal-planner {
                grid-template-columns: 1fr;
            }
            
            .nav {
                flex-direction: column;
                align-items: center;
            }
            
            .nav-btn {
                width: 100%;
                max-width: 200px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>🥗 Healthy Food Guide</h1>
            <p>Your complete guide to nutritious eating</p>
        </div>

        <div class="nav">
            <button class="nav-btn active" onclick="showSection('foods')">Food Database</button>
            <button class="nav-btn" onclick="showSection('planner')">Meal Planner</button>
            <button class="nav-btn" onclick="showSection('recipes')">Healthy Recipes</button>
            <button class="nav-btn" onclick="showSection('tracker')">Nutrition Tracker</button>
        </div>

        <div id="foods" class="content-section active">
            <input type="text" class="search-bar" placeholder="Search foods..." oninput="searchFoods(this.value)">
            <div class="food-grid" id="foodGrid"></div>
        </div>

        <div id="planner" class="content-section">
            <h2>Weekly Meal Planner</h2>
            <div class="meal-planner" id="mealPlanner"></div>
        </div>

        <div id="recipes" class="content-section">
            <h2>Healthy Recipes</h2>
            <input type="text" class="search-bar" placeholder="Search recipes..." oninput="searchRecipes(this.value)">
            <div id="recipeList"></div>
        </div>

        <div id="tracker" class="content-section">
            <h2>Daily Nutrition Tracker</h2>
            <div class="stats-grid">
                <div class="stat-card">
                    <div class="stat-number" id="totalCalories">0</div>
                    <div class="stat-label">Calories</div>
                </div>
                <div class="stat-card">
                    <div class="stat-number" id="totalProtein">0</div>
                    <div class="stat-label">Protein (g)</div>
                </div>
                <div class="stat-card">
                    <div class="stat-number" id="totalCarbs">0</div>
                    <div class="stat-label">Carbs (g)</div>
                </div>
                <div class="stat-card">
                    <div class="stat-number" id="totalFat">0</div>
                    <div class="stat-label">Fat (g)</div>
                </div>
            </div>
            <div class="food-grid" id="trackerFoods"></div>
        </div>
    </div>

    <script>
        const foodDatabase = [
            {
                name: "Avocado",
                category: "Fruits",
                calories: 160,
                protein: 2,
                carbs: 9,
                fat: 15,
                benefits: "Rich in healthy fats, fiber, and potassium. Supports heart health and may help reduce cholesterol."
            },
            {
                name: "Salmon",
                category: "Protein",
                calories: 208,
                protein: 22,
                carbs: 0,
                fat: 12,
                benefits: "Excellent source of omega-3 fatty acids. Supports brain health and reduces inflammation."
            },
            {
                name: "Spinach",
                category: "Vegetables",
                calories: 23,
                protein: 3,
                carbs: 4,
                fat: 0,
                benefits: "High in iron, vitamins A and K. Supports bone health and boosts immune system."
            },
            {
                name: "Quinoa",
                category: "Grains",
                calories: 222,
                protein: 8,
                carbs: 39,
                fat: 4,
                benefits: "Complete protein source with all essential amino acids. Gluten-free and high in fiber."
            },
            {
                name: "Blueberries",
                category: "Fruits",
                calories: 84,
                protein: 1,
                carbs: 21,
                fat: 0,
                benefits: "Packed with antioxidants and vitamin C. May improve memory and support brain health."
            },
            {
                name: "Greek Yogurt",
                category: "Dairy",
                calories: 100,
                protein: 17,
                carbs: 6,
                fat: 0,
                benefits: "High in protein and probiotics. Supports digestive health and muscle building."
            },
            {
                name: "Sweet Potato",
                category: "Vegetables",
                calories: 112,
                protein: 2,
                carbs: 26,
                fat: 0,
                benefits: "Rich in beta-carotene and fiber. Supports eye health and stable blood sugar."
            },
            {
                name: "Almonds",
                category: "Nuts",
                calories: 164,
                protein: 6,
                carbs: 6,
                fat: 14,
                benefits: "Good source of vitamin E and healthy fats. May help lower cholesterol and support heart health."
            }
        ];

        const recipes = [
            {
                title: "Quinoa Buddha Bowl",
                category: "Lunch",
                prepTime: "15 min",
                cookTime: "20 min",
                servings: 2,
                ingredients: [
                    "1 cup quinoa",
                    "2 cups spinach",
                    "1 avocado, sliced",
                    "1 cup roasted sweet potato",
                    "1/4 cup pumpkin seeds",
                    "2 tbsp olive oil",
                    "1 tbsp lemon juice",
                    "Salt and pepper to taste"
                ],
                instructions: [
                    "Cook quinoa according to package instructions",
                    "Roast sweet potato cubes at 400°F for 25 minutes",
                    "Massage spinach with olive oil and lemon juice",
                    "Arrange all ingredients in bowls",
                    "Top with pumpkin seeds and serve"
                ]
            },
            {
                title: "Baked Salmon with Herbs",
                category: "Dinner",
                prepTime: "10 min",
                cookTime: "15 min",
                servings: 4,
                ingredients: [
                    "4 salmon fillets",
                    "2 tbsp olive oil",
                    "2 cloves garlic, minced",
                    "1 tbsp fresh dill",
                    "1 lemon, sliced",
                    "Salt and pepper"
                ],
                instructions: [
                    "Preheat oven to 425°F",
                    "Place salmon on baking sheet",
                    "Drizzle with olive oil and season",
                    "Add garlic, dill, and lemon slices",
                    "Bake for 12-15 minutes until flaky"
                ]
            },
            {
                title: "Berry Smoothie Bowl",
                category: "Breakfast",
                prepTime: "5 min",
                cookTime: "0 min",
                servings: 1,
                ingredients: [
                    "1 cup frozen blueberries",
                    "1/2 banana",
                    "1/2 cup Greek yogurt",
                    "1 tbsp almond butter",
                    "1 tbsp honey",
                    "Granola for topping"
                ],
                instructions: [
                    "Blend frozen fruit with yogurt until thick",
                    "Pour into bowl",
                    "Top with granola and fresh fruit",
                    "Drizzle with honey and serve immediately"
                ]
            }
        ];

        const mealPlan = {
            Monday: ["Berry Smoothie Bowl", "Quinoa Buddha Bowl", "Baked Salmon"],
            Tuesday: ["Greek Yogurt & Berries", "Spinach Salad", "Grilled Chicken"],
            Wednesday: ["Overnight Oats", "Sweet Potato Bowl", "Fish Tacos"],
            Thursday: ["Avocado Toast", "Quinoa Salad", "Vegetable Stir-fry"],
            Friday: ["Smoothie Bowl", "Buddha Bowl", "Salmon & Vegetables"],
            Saturday: ["Pancakes (Healthy)", "Grain Bowl", "Lean Protein"],
            Sunday: ["Yogurt Parfait", "Salad Mix", "Roasted Vegetables"]
        };

        let currentFoods = [...foodDatabase];
        let currentRecipes = [...recipes];
        let dailyIntake = { calories: 0, protein: 0, carbs: 0, fat: 0 };

        function showSection(sectionId) {
            document.querySelectorAll('.content-section').forEach(section => {
                section.classList.remove('active');
            });
            document.querySelectorAll('.nav-btn').forEach(btn => {
                btn.classList.remove('active');
            });
            
            document.getElementById(sectionId).classList.add('active');
            event.target.classList.add('active');
            
            if (sectionId === 'foods') loadFoods();
            if (sectionId === 'planner') loadMealPlanner();
            if (sectionId === 'recipes') loadRecipes();
            if (sectionId === 'tracker') loadTracker();
        }

        function loadFoods() {
            const grid = document.getElementById('foodGrid');
            grid.innerHTML = currentFoods.map(food => `
                <div class="food-card">
                    <div class="food-category">${food.category}</div>
                    <div class="food-name">${food.name}</div>
                    <div class="nutrition-info">
                        <div class="nutrition-item">
                            <div class="nutrition-label">Calories</div>
                            <div class="nutrition-value">${food.calories}</div>
                        </div>
                        <div class="nutrition-item">
                            <div class="nutrition-label">Protein</div>
                            <div class="nutrition-value">${food.protein}g</div>
                        </div>
                        <div class="nutrition-item">
                            <div class="nutrition-label">Carbs</div>
                            <div class="nutrition-value">${food.carbs}g</div>
                        </div>
                        <div class="nutrition-item">
                            <div class="nutrition-label">Fat</div>
                            <div class="nutrition-value">${food.fat}g</div>
                        </div>
                    </div>
                    <div class="benefits">
                        <h4>Health Benefits</h4>
                        <p>${food.benefits}</p>
                    </div>
                </div>
            `).join('');
        }

        function loadMealPlanner() {
            const planner = document.getElementById('mealPlanner');
            planner.innerHTML = Object.entries(mealPlan).map(([day, meals]) => `
                <div class="day-card">
                    <div class="day-header">${day}</div>
                    ${meals.map(meal => `<div class="meal-item">${meal}</div>`).join('')}
                </div>
            `).join('');
        }

        function loadRecipes() {
            const list = document.getElementById('recipeList');
            list.innerHTML = currentRecipes.map(recipe => `
                <div class="recipe-card">
                    <div class="recipe-title">${recipe.title}</div>
                    <div class="recipe-meta">
                        <span>📝 ${recipe.category}</span>
                        <span>⏰ Prep: ${recipe.prepTime}</span>
                        <span>🔥 Cook: ${recipe.cookTime}</span>
                        <span>👥 Serves: ${recipe.servings}</span>
                    </div>
                    <div class="ingredients">
                        <h4>Ingredients</h4>
                        <ul>
                            ${recipe.ingredients.map(ingredient => `<li>${ingredient}</li>`).join('')}
                        </ul>
                    </div>
                    <div class="instructions">
                        <h4>Instructions</h4>
                        <ol>
                            ${recipe.instructions.map(step => `<li>${step}</li>`).join('')}
                        </ol>
                    </div>
                </div>
            `).join('');
        }

        function loadTracker() {
            updateTrackerStats();
            const grid = document.getElementById('trackerFoods');
            grid.innerHTML = foodDatabase.map(food => `
                <div class="food-card">
                    <div class="food-category">${food.category}</div>
                    <div class="food-name">${food.name}</div>
                    <div class="nutrition-info">
                        <div class="nutrition-item">
                            <div class="nutrition-label">Calories</div>
                            <div class="nutrition-value">${food.calories}</div>
                        </div>
                        <div class="nutrition-item">
                            <div class="nutrition-label">Protein</div>
                            <div class="nutrition-value">${food.protein}g</div>
                        </div>
                    </div>
                    <button onclick="addToTracker('${food.name}')" style="width: 100%; padding: 8px; background: #4ade80; color: white; border: none; border-radius: 6px; cursor: pointer; margin-top: 10px;">Add to Today</button>
                </div>
            `).join('');
        }

        function addToTracker(foodName) {
            const food = foodDatabase.find(f => f.name === foodName);
            if (food) {
                dailyIntake.calories += food.calories;
                dailyIntake.protein += food.protein;
                dailyIntake.carbs += food.carbs;
                dailyIntake.fat += food.fat;
                updateTrackerStats();
            }
        }

        function updateTrackerStats() {
            document.getElementById('totalCalories').textContent = dailyIntake.calories;
            document.getElementById('totalProtein').textContent = dailyIntake.protein;
            document.getElementById('totalCarbs').textContent = dailyIntake.carbs;
            document.getElementById('totalFat').textContent = dailyIntake.fat;
        }

        function searchFoods(query) {
            currentFoods = foodDatabase.filter(food => 
                food.name.toLowerCase().includes(query.toLowerCase()) ||
                food.category.toLowerCase().includes(query.toLowerCase())
            );
            loadFoods();
        }

        function searchRecipes(query) {
            currentRecipes = recipes.filter(recipe =>
                recipe.title.toLowerCase().includes(query.toLowerCase()) ||
                recipe.category.toLowerCase().includes(query.toLowerCase())
            );
            loadRecipes();
        }

        if ('serviceWorker' in navigator) {
            navigator.serviceWorker.register('/sw.js')
                .then(registration => console.log('SW registered'))
                .catch(error => console.log('SW registration failed'));
        }

        loadFoods();
    </script>
</body>
</html>
