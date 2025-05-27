<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Bye Béo - Ứng dụng dinh dưỡng MVP</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #f0fdf4 0%, #dcfce7 100%);
            min-height: 100vh;
            color: #1f2937;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }

        .header {
            background: linear-gradient(135deg, #22c55e, #16a34a);
            color: white;
            padding: 30px;
            border-radius: 20px;
            text-align: center;
            margin-bottom: 30px;
            box-shadow: 0 10px 30px rgba(34, 197, 94, 0.3);
        }

        .header h1 {
            font-size: 2.5em;
            margin-bottom: 10px;
        }

        .subtitle {
            font-size: 1.1em;
            opacity: 0.9;
        }

        .main-content {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 30px;
            margin-bottom: 30px;
        }

        .card {
            background: white;
            border-radius: 15px;
            padding: 25px;
            box-shadow: 0 5px 20px rgba(0,0,0,0.1);
            border: 2px solid #e5e7eb;
        }

        .card h2 {
            color: #16a34a;
            margin-bottom: 20px;
            font-size: 1.5em;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .form-group {
            margin-bottom: 15px;
        }

        .form-group label {
            display: block;
            margin-bottom: 5px;
            font-weight: 600;
            color: #374151;
        }

        .form-group input, .form-group select {
            width: 100%;
            padding: 12px;
            border: 2px solid #d1d5db;
            border-radius: 8px;
            font-size: 14px;
            transition: border-color 0.3s;
        }

        .form-group input:focus, .form-group select:focus {
            outline: none;
            border-color: #22c55e;
        }

        .btn {
            background: linear-gradient(135deg, #22c55e, #16a34a);
            color: white;
            border: none;
            padding: 12px 24px;
            border-radius: 8px;
            font-weight: 600;
            cursor: pointer;
            transition: transform 0.2s;
            width: 100%;
            font-size: 16px;
        }

        .btn:hover {
            transform: translateY(-2px);
        }

        .btn-secondary {
            background: #3b82f6;
        }

        .btn-danger {
            background: #ef4444;
        }

        .stats-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
            gap: 15px;
            margin: 20px 0;
        }

        .stat-item {
            background: #f0fdf4;
            padding: 15px;
            border-radius: 10px;
            text-align: center;
            border: 2px solid #22c55e;
        }

        .stat-number {
            font-size: 1.8em;
            font-weight: bold;
            color: #16a34a;
        }

        .stat-label {
            font-size: 0.9em;
            color: #6b7280;
            margin-top: 5px;
        }

        .food-log {
            grid-column: 1 / -1;
        }

        .food-search {
            display: flex;
            gap: 10px;
            margin-bottom: 15px;
        }

        .food-search input {
            flex: 1;
        }

        .food-list {
            max-height: 200px;
            overflow-y: auto;
            border: 2px solid #e5e7eb;
            border-radius: 8px;
            margin-bottom: 15px;
        }

        .food-item {
            padding: 10px;
            border-bottom: 1px solid #e5e7eb;
            display: flex;
            justify-content: space-between;
            align-items: center;
            cursor: pointer;
            transition: background-color 0.2s;
        }

        .food-item:hover {
            background-color: #f9fafb;
        }

        .food-item:last-child {
            border-bottom: none;
        }

        .food-name {
            font-weight: 600;
            flex: 1;
        }

        .food-calories {
            color: #6b7280;
            font-size: 0.9em;
        }

        .add-food-form {
            background: #f9fafb;
            padding: 15px;
            border-radius: 8px;
            margin-top: 15px;
            display: none;
        }

        .add-food-form.active {
            display: block;
        }

        .quantity-input {
            display: flex;
            gap: 10px;
            align-items: center;
            margin: 15px 0;
        }

        .today-log {
            margin-top: 20px;
        }

        .meal-section {
            margin-bottom: 20px;
            background: #f8fafc;
            padding: 15px;
            border-radius: 8px;
        }

        .meal-title {
            font-weight: bold;
            color: #16a34a;
            margin-bottom: 10px;
            font-size: 1.1em;
        }

        .logged-food {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 8px 0;
            border-bottom: 1px solid #e5e7eb;
        }

        .logged-food:last-child {
            border-bottom: none;
        }

        .delete-btn {
            background: #ef4444;
            color: white;
            border: none;
            padding: 5px 10px;
            border-radius: 5px;
            cursor: pointer;
            font-size: 12px;
        }

        .macro-bar {
            background: #e5e7eb;
            height: 20px;
            border-radius: 10px;
            overflow: hidden;
            margin: 10px 0;
            position: relative;
        }

        .macro-fill {
            height: 100%;
            border-radius: 10px;
            transition: width 0.3s;
        }

        .protein-fill { background: #ef4444; }
        .carb-fill { background: #3b82f6; }
        .fat-fill { background: #f59e0b; }

        .macro-text {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            font-size: 12px;
            font-weight: bold;
            color: white;
            text-shadow: 1px 1px 2px rgba(0,0,0,0.5);
        }

        @media (max-width: 768px) {
            .main-content {
                grid-template-columns: 1fr;
            }
            
            .stats-grid {
                grid-template-columns: repeat(2, 1fr);
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>🌿 BYE BÉO MVP</h1>
            <p class="subtitle">Ứng dụng theo dõi dinh dưỡng thông minh - Giai đoạn 1</p>
        </div>

        <div class="main-content">
            <!-- Thông tin cá nhân và tính toán -->
            <div class="card">
                <h2>👤 Thông tin cá nhân</h2>
                <div class="form-group">
                    <label>Tuổi:</label>
                    <input type="number" id="age" value="25" min="16" max="80">
                </div>
                <div class="form-group">
                    <label>Giới tính:</label>
                    <select id="gender">
                        <option value="female">Nữ</option>
                        <option value="male">Nam</option>
                    </select>
                </div>
                <div class="form-group">
                    <label>Cân nặng (kg):</label>
                    <input type="number" id="weight" value="60" step="0.1">
                </div>
                <div class="form-group">
                    <label>Chiều cao (cm):</label>
                    <input type="number" id="height" value="165" step="0.1">
                </div>
                <div class="form-group">
                    <label>Mức độ hoạt động:</label>
                    <select id="activity">
                        <option value="1.2">Ít vận động</option>
                        <option value="1.375">Nhẹ (1-3 ngày/tuần)</option>
                        <option value="1.55" selected>Vừa (3-5 ngày/tuần)</option>
                        <option value="1.725">Nặng (6-7 ngày/tuần)</option>
                        <option value="1.9">Rất nặng</option>
                    </select>
                </div>
                <div class="form-group">
                    <label>Mục tiêu:</label>
                    <select id="goal">
                        <option value="-500" selected>Giảm cân (0.5kg/tuần)</option>
                        <option value="-250">Giảm cân nhẹ (0.25kg/tuần)</option>
                        <option value="0">Duy trì cân nặng</option>
                        <option value="250">Tăng cân nhẹ</option>
                        <option value="500">Tăng cân</option>
                    </select>
                </div>
                <button class="btn" onclick="calculateNutrition()">📊 Tính toán dinh dưỡng</button>
            </div>

            <!-- Hiển thị kết quả tính toán -->
            <div class="card">
                <h2>📊 Chỉ số dinh dưỡng</h2>
                <div class="stats-grid">
                    <div class="stat-item">
                        <div class="stat-number" id="bmi">--</div>
                        <div class="stat-label">BMI</div>
                    </div>
                    <div class="stat-item">
                        <div class="stat-number" id="bmr">--</div>
                        <div class="stat-label">BMR (kcal)</div>
                    </div>
                    <div class="stat-item">
                        <div class="stat-number" id="tdee">--</div>
                        <div class="stat-label">TDEE (kcal)</div>
                    </div>
                    <div class="stat-item">
                        <div class="stat-number" id="target-calories">--</div>
                        <div class="stat-label">Calo mục tiêu</div>
                    </div>
                </div>

                <h3 style="margin: 20px 0 10px 0; color: #16a34a;">Macronutrients hàng ngày:</h3>
                
                <div style="margin-bottom: 10px;">
                    <div style="display: flex; justify-content: space-between; align-items: center;">
                        <span><strong>Protein:</strong> <span id="protein-target">--</span>g</span>
                        <span id="protein-percent">--%</span>
                    </div>
                    <div class="macro-bar">
                        <div class="macro-fill protein-fill" id="protein-bar" style="width: 0%"></div>
                        <div class="macro-text" id="protein-text">0g / 0g</div>
                    </div>
                </div>

                <div style="margin-bottom: 10px;">
                    <div style="display: flex; justify-content: space-between; align-items: center;">
                        <span><strong>Carbs:</strong> <span id="carb-target">--</span>g</span>
                        <span id="carb-percent">--%</span>
                    </div>
                    <div class="macro-bar">
                        <div class="macro-fill carb-fill" id="carb-bar" style="width: 0%"></div>
                        <div class="macro-text" id="carb-text">0g / 0g</div>
                    </div>
                </div>

                <div style="margin-bottom: 10px;">
                    <div style="display: flex; justify-content: space-between; align-items: center;">
                        <span><strong>Fat:</strong> <span id="fat-target">--</span>g</span>
                        <span id="fat-percent">--%</span>
                    </div>
                    <div class="macro-bar">
                        <div class="macro-fill fat-fill" id="fat-bar" style="width: 0%"></div>
                        <div class="macro-text" id="fat-text">0g / 0g</div>
                    </div>
                </div>
            </div>

            <!-- Ghi log thực phẩm -->
            <div class="card food-log">
                <h2>🍽️ Ghi log bữa ăn</h2>
                
                <div class="food-search">
                    <input type="text" id="search-input" placeholder="Tìm kiếm thực phẩm..." onkeyup="searchFood()">
                    <button class="btn btn-secondary" onclick="toggleAddForm()">➕ Thêm món mới</button>
                </div>

                <div class="food-list" id="food-list">
                    <!-- Danh sách thực phẩm sẽ được hiển thị ở đây -->
                </div>

                <!-- Form thêm thực phẩm mới -->
                <div class="add-food-form" id="add-food-form">
                    <h3>Thêm món ăn mới</h3>
                    <div class="form-group">
                        <label>Tên món:</label>
                        <input type="text" id="new-food-name" placeholder="Ví dụ: Cơm trắng">
                    </div>
                    <div style="display: grid; grid-template-columns: repeat(4, 1fr); gap: 10px;">
                        <div class="form-group">
                            <label>Calo/100g:</label>
                            <input type="number" id="new-food-calories" placeholder="130">
                        </div>
                        <div class="form-group">
                            <label>Protein (g):</label>
                            <input type="number" id="new-food-protein" placeholder="2.7" step="0.1">
                        </div>
                        <div class="form-group">
                            <label>Carbs (g):</label>
                            <input type="number" id="new-food-carbs" placeholder="28" step="0.1">
                        </div>
                        <div class="form-group">
                            <label>Fat (g):</label>
                            <input type="number" id="new-food-fat" placeholder="0.3" step="0.1">
                        </div>
                    </div>
                    <div style="display: flex; gap: 10px;">
                        <button class="btn" onclick="addNewFood()">✅ Thêm vào CSDL</button>
                        <button class="btn btn-danger" onclick="toggleAddForm()">❌ Hủy</button>
                    </div>
                </div>

                <!-- Form thêm vào bữa ăn -->
                <div class="add-food-form" id="add-to-meal-form">
                    <h3 id="selected-food-name">Thêm vào bữa ăn</h3>
                    <div class="form-group">
                        <label>Bữa ăn:</label>
                        <select id="meal-type">
                            <option value="breakfast">Sáng</option>
                            <option value="lunch">Trưa</option>
                            <option value="dinner">Tối</option>
                            <option value="snack">Ăn vặt</option>
                        </select>
                    </div>
                    <div class="quantity-input">
                        <label>Số lượng (g):</label>
                        <input type="number" id="food-quantity" value="100" min="1" step="1">
                        <span>gram</span>
                    </div>
                    <div id="nutrition-preview" style="background: #f0fdf4; padding: 10px; border-radius: 5px; margin: 10px 0;">
                        <!-- Preview dinh dưỡng sẽ hiển thị ở đây -->
                    </div>
                    <div style="display: flex; gap: 10px;">
                        <button class="btn" onclick="addToMeal()">✅ Thêm vào bữa ăn</button>
                        <button class="btn btn-danger" onclick="closeAddToMeal()">❌ Hủy</button>
                    </div>
                </div>

                <!-- Log bữa ăn hôm nay -->
                <div class="today-log">
                    <h3 style="color: #16a34a; margin-bottom: 15px;">📅 Bữa ăn hôm nay</h3>
                    <div class="stats-grid" style="margin-bottom: 20px;">
                        <div class="stat-item">
                            <div class="stat-number" id="total-calories">0</div>
                            <div class="stat-label">Tổng Calo</div>
                        </div>
                        <div class="stat-item">
                            <div class="stat-number" id="total-protein">0</div>
                            <div class="stat-label">Protein (g)</div>
                        </div>
                        <div class="stat-item">
                            <div class="stat-number" id="total-carbs">0</div>
                            <div class="stat-label">Carbs (g)</div>
                        </div>
                        <div class="stat-item">
                            <div class="stat-number" id="total-fat">0</div>
                            <div class="stat-label">Fat (g)</div>
                        </div>
                    </div>

                    <div id="meals-log">
                        <div class="meal-section">
                            <div class="meal-title">🌅 Bữa sáng</div>
                            <div id="breakfast-foods">Chưa có món nào</div>
                        </div>
                        <div class="meal-section">
                            <div class="meal-title">☀️ Bữa trưa</div>
                            <div id="lunch-foods">Chưa có món nào</div>
                        </div>
                        <div class="meal-section">
                            <div class="meal-title">🌆 Bữa tối</div>
                            <div id="dinner-foods">Chưa có món nào</div>
                        </div>
                        <div class="meal-section">
                            <div class="meal-title">🍿 Ăn vặt</div>
                            <div id="snack-foods">Chưa có món nào</div>
                        </div>
                    </div>

                    <button class="btn btn-danger" onclick="clearAllMeals()" style="margin-top: 15px;">🗑️ Xóa tất cả bữa ăn</button>
                </div>
            </div>
        </div>
    </div>

    <script>
        // Cơ sở dữ liệu thực phẩm Việt Nam (50 món phổ biến)
        let foodDatabase = [
            {name: "Cơm trắng", calories: 130, protein: 2.7, carbs: 28, fat: 0.3},
            {name: "Phở bò", calories: 320, protein: 15, carbs: 45, fat: 8},
            {name: "Bánh mì thịt", calories: 280, protein: 12, carbs: 35, fat: 10},
            {name: "Bún chả", calories: 350, protein: 18, carbs: 40, fat: 12},
            {name: "Cháo gà", calories: 180, protein: 8, carbs: 30, fat: 2},
            {name: "Thịt heo nạc", calories: 143, protein: 20.8, carbs: 0, fat: 6.2},
            {name: "Thịt bò nạc", calories: 158, protein: 26, carbs: 0, fat: 5.5},
            {name: "Gà luộc (không da)", calories: 165, protein: 31, carbs: 0, fat: 3.6},
            {name: "Cá hồi", calories: 208, protein: 25, carbs: 0, fat: 12},
            {name: "Tôm luộc", calories: 99, protein: 18, carbs: 0.2, fat: 1.4},
            {name: "Trứng gà", calories: 155, protein: 13, carbs: 1.1, fat: 11},
            {name: "Sữa tươi", calories: 42, protein: 3.4, carbs: 5, fat: 1},
            {name: "Sữa chua", calories: 59, protein: 3.5, carbs: 4.7, fat: 3.3},
            {name: "Rau cải xanh", calories: 13, protein: 1.5, carbs: 2.4, fat: 0.2},
            {name: "Cà rốt", calories: 25, protein: 1, carbs: 6, fat: 0.2},
            {name: "Cà chua", calories: 18, protein: 0.9, carbs: 3.9, fat: 0.2},
            {name: "Dưa chuột", calories: 16, protein: 0.7, carbs: 4, fat: 0.1},
            {name: "Rau muống", calories: 19, protein: 2.6, carbs: 2.1, fat: 0.2},
            {name: "Bắp cải trắng", calories: 25, protein: 1.3, carbs: 5.8, fat: 0.1},
            {name: "Khoai tây", calories: 77, protein: 2, carbs: 17, fat: 0.1},
            {name: "Khoai lang", calories: 86, protein: 1.6, carbs: 20, fat: 0.1},
            {name: "Chuối", calories: 89, protein: 1.1, carbs: 23, fat: 0.3},
            {name: "Táo", calories: 52, protein: 0.3, carbs: 14, fat: 0.2},
            {name: "Cam", calories: 47, protein: 0.9, carbs: 12, fat: 0.1},
            {name: "Xoài", calories: 60, protein: 0.8, carbs: 15, fat: 0.4},
            {name: "Nho", calories: 69, protein: 0.7, carbs: 18, fat: 0.2},
            {name: "Dưa hấu", calories: 30, protein: 0.6, carbs: 8, fat: 0.2},
            {name: "Đu đủ", calories: 43, protein: 0.5, carbs: 11, fat: 0.3},
            {name: "Bơ", calories: 160, protein: 2, carbs: 9, fat: 15},
            {name: "Hạt điều", calories: 553, protein: 18, carbs: 30, fat: 44},
            {name: "Hạt óc chó", calories: 654, protein: 15, carbs: 14, fat: 65},
            {name: "Đậu phụ", calories: 76, protein: 8, carbs: 1.9, fat: 4.8},
            {name: "Đậu xanh", calories: 347, protein: 23, carbs: 63, fat: 1.2},
            {name: "Đậu đỏ", calories: 333, protein: 20, carbs: 61, fat: 1.1},
            {name: "Yến mạch", calories: 389, protein: 17, carbs: 66, fat: 7},
            {name: "Bánh mì sandwich", calories: 265, protein: 9, carbs: 49, fat: 3.2},
            {name: "Mì ý", calories: 371, protein: 13, carbs: 75, fat: 1.5},
            {name: "Bún tươi", calories: 109, protein: 2.5, carbs: 25, fat: 0.1},
            {name: "Miến", calories: 351, protein: 0.1, carbs: 86, fat: 0.1},
            {name: "Bánh phở", calories: 109, protein: 2.5, carbs: 25, fat: 0.1},
            {name: "Chè đậu xanh", calories: 180, protein: 4, carbs: 35, fat: 2},
            {name: "Chè bà ba", calories: 220, protein: 3, carbs: 45, fat: 3},
            {name: "Bánh flan", calories: 150, protein: 4, carbs: 22, fat: 5.5},
            {name: "Kem vanilla", calories: 207, protein: 3.5, carbs: 24, fat: 11},
            {name: "Nước mía", calories: 269, protein: 0, carbs: 73, fat: 0},
            {name: "Nước dừa", calories: 19, protein: 0.7, carbs: 3.7, fat: 0.2},
            {name: "Cà phê đen", calories: 2, protein: 0.3, carbs: 0, fat: 0},
            {name: "Cà phê sữa", calories: 150, protein: 2, carbs: 24, fat: 5},
            {name: "Trà xanh", calories: 2, protein: 0.2, carbs: 0, fat: 0}
        ];

        // Lưu trữ bữa ăn trong ngày
        let todayMeals = {
            breakfast: [],
            lunch: [],
            dinner: [],
            snack: []
        };

        // Biến lưu thông tin dinh dưỡng mục tiêu
        let nutritionTargets = {
            calories: 0,
            protein: 0,
            carbs: 0,
            fat: 0
        };

        // Biến lưu thực phẩm được chọn
        let selectedFood = null;

        // Khởi tạo app
        function initApp() {
            displayFoodList();
            updateMealDisplay();
            updateNutritionBars();
        }

        // Hiển thị danh sách thực phẩm
        function displayFoodList(foods = foodDatabase) {
            const foodList = document.getElementById('food-list');
            foodList.innerHTML = '';
            
            foods.forEach((food, index) => {
                const foodItem = document.createElement('div');
                foodItem.className = 'food-item';
                foodItem.onclick = () => selectFood(food);
                foodItem.innerHTML = `
                    <div class="food-name">${food.name}</div>
                    <div class="food-calories">${food.calories} kcal/100g</div>
                `;
                foodList.appendChild(foodItem);
            });
        }

        // Tìm kiếm thực phẩm
        function searchFood() {
            const searchTerm = document.getElementById('search-input').value.toLowerCase();
            const filteredFoods = foodDatabase.filter(food => 
                food.name.toLowerCase().includes(searchTerm)
            );
            displayFoodList(filteredFoods);
        }

        // Tính toán dinh dưỡng
        function calculateNutrition() {
            const age = parseInt(document.getElementById('age').value);
            const gender = document.getElementById('gender').value;
            const weight = parseFloat(document.getElementById('weight').value);
            const height = parseFloat(document.getElementById('height').value);
            const activity = parseFloat(document.getElementById('activity').value);
            const goal = parseInt(document.getElementById('goal').value);

            // Tính BMI
            const bmi = (weight / ((height/100) ** 2)).toFixed(1);
            document.getElementById('bmi').textContent = bmi;

            // Tính BMR (Harris-Benedict)
            let bmr;
            if (gender === 'male') {
                bmr = 88.362 + (13.397 * weight) + (4.799 * height) - (5.677 * age);
            } else {
                bmr = 447.593 + (9.247 * weight) + (3.098 * height) - (4.330 * age);
            }

            // Tính TDEE
            const tdee = bmr * activity;
            
            // Tính calories mục tiêu
            const targetCalories = tdee + goal;

            // Tính macros (30% protein, 40% carbs, 30% fat)
            const proteinCalories = targetCalories * 0.30;
            const carbCalories = targetCalories * 0.40;
            const fatCalories = targetCalories * 0.30;

            const proteinGrams = Math.round(proteinCalories / 4);
            const carbGrams = Math.round(carbCalories / 4);
            const fatGrams = Math.round(fatCalories / 9);

            // Hiển thị kết quả
            document.getElementById('bmr').textContent = Math.round(bmr);
            document.getElementById('tdee').textContent = Math.round(tdee);
            document.getElementById('target-calories').textContent = Math.round(targetCalories);
            document.getElementById('protein-target').textContent = proteinGrams;
            document.getElementById('carb-target').textContent = carbGrams;
            document.getElementById('fat-target').textContent = fatGrams;

            // Lưu targets
            nutritionTargets = {
                calories: Math.round(targetCalories),
                protein: proteinGrams,
                carbs: carbGrams,
                fat: fatGrams
            };

            // Cập nhật thanh macro
            updateNutritionBars();
        }

        // Chọn thực phẩm để thêm vào bữa ăn
        function selectFood(food) {
            selectedFood = food;
            document.getElementById('selected-food-name').textContent = `Thêm ${food.name} vào bữa ăn`;
            document.getElementById('add-to-meal-form').classList.add('active');
            updateNutritionPreview();
        }

        // Cập nhật preview dinh dưỡng khi thay đổi số lượng
        function updateNutritionPreview() {
            if (!selectedFood) return;
            
            const quantity = parseFloat(document.getElementById('food-quantity').value) || 100;
            const multiplier = quantity / 100;
            
            const calories = Math.round(selectedFood.calories * multiplier);
            const protein = Math.round(selectedFood.protein * multiplier * 10) / 10;
            const carbs = Math.round(selectedFood.carbs * multiplier * 10) / 10;
            const fat = Math.round(selectedFood.fat * multiplier * 10) / 10;
            
            document.getElementById('nutrition-preview').innerHTML = `
                <strong>Dinh dưỡng cho ${quantity}g ${selectedFood.name}:</strong><br>
                🔥 Calories: ${calories} kcal<br>
                🥩 Protein: ${protein}g<br>
                🌾 Carbs: ${carbs}g<br>
                🥑 Fat: ${fat}g
            `;
        }

        // Cập nhật preview khi thay đổi số lượng
        document.getElementById('food-quantity').addEventListener('input', updateNutritionPreview);

        // Thêm thực phẩm vào bữa ăn
        function addToMeal() {
            if (!selectedFood) return;
            
            const mealType = document.getElementById('meal-type').value;
            const quantity = parseFloat(document.getElementById('food-quantity').value) || 100;
            const multiplier = quantity / 100;
            
            const mealItem = {
                name: selectedFood.name,
                quantity: quantity,
                calories: Math.round(selectedFood.calories * multiplier),
                protein: Math.round(selectedFood.protein * multiplier * 10) / 10,
                carbs: Math.round(selectedFood.carbs * multiplier * 10) / 10,
                fat: Math.round(selectedFood.fat * multiplier * 10) / 10,
                id: Date.now() // ID unique để xóa sau này
            };
            
            todayMeals[mealType].push(mealItem);
            
            // Đóng form và reset
            closeAddToMeal();
            
            // Cập nhật hiển thị
            updateMealDisplay();
            updateTotalNutrition();
            updateNutritionBars();
        }

        // Đóng form thêm vào bữa ăn
        function closeAddToMeal() {
            document.getElementById('add-to-meal-form').classList.remove('active');
            selectedFood = null;
            document.getElementById('food-quantity').value = 100;
        }

        // Cập nhật hiển thị bữa ăn
        function updateMealDisplay() {
            const mealNames = {
                breakfast: 'breakfast-foods',
                lunch: 'lunch-foods',
                dinner: 'dinner-foods',
                snack: 'snack-foods'
            };
            
            Object.keys(mealNames).forEach(mealType => {
                const container = document.getElementById(mealNames[mealType]);
                const meals = todayMeals[mealType];
                
                if (meals.length === 0) {
                    container.innerHTML = 'Chưa có món nào';
                } else {
                    container.innerHTML = meals.map(meal => `
                        <div class="logged-food">
                            <div>
                                <strong>${meal.name}</strong> (${meal.quantity}g)<br>
                                <small>${meal.calories} kcal | P: ${meal.protein}g | C: ${meal.carbs}g | F: ${meal.fat}g</small>
                            </div>
                            <button class="delete-btn" onclick="removeMealItem('${mealType}', ${meal.id})">✕</button>
                        </div>
                    `).join('');
                }
            });
        }

        // Xóa món ăn khỏi bữa ăn
        function removeMealItem(mealType, itemId) {
            todayMeals[mealType] = todayMeals[mealType].filter(item => item.id !== itemId);
            updateMealDisplay();
            updateTotalNutrition();
            updateNutritionBars();
        }

        // Cập nhật tổng dinh dưỡng
        function updateTotalNutrition() {
            let totalCalories = 0;
            let totalProtein = 0;
            let totalCarbs = 0;
            let totalFat = 0;
            
            Object.values(todayMeals).forEach(meals => {
                meals.forEach(meal => {
                    totalCalories += meal.calories;
                    totalProtein += meal.protein;
                    totalCarbs += meal.carbs;
                    totalFat += meal.fat;
                });
            });
            
            document.getElementById('total-calories').textContent = Math.round(totalCalories);
            document.getElementById('total-protein').textContent = Math.round(totalProtein * 10) / 10;
            document.getElementById('total-carbs').textContent = Math.round(totalCarbs * 10) / 10;
            document.getElementById('total-fat').textContent = Math.round(totalFat * 10) / 10;
        }

        // Cập nhật thanh macro
        function updateNutritionBars() {
            if (nutritionTargets.calories === 0) return;
            
            const currentNutrition = getCurrentNutrition();
            
            // Protein bar
            const proteinPercent = Math.min((currentNutrition.protein / nutritionTargets.protein) * 100, 100);
            document.getElementById('protein-bar').style.width = proteinPercent + '%';
            document.getElementById('protein-text').textContent = `${Math.round(currentNutrition.protein * 10) / 10}g / ${nutritionTargets.protein}g`;
            document.getElementById('protein-percent').textContent = Math.round(proteinPercent) + '%';
            
            // Carbs bar
            const carbPercent = Math.min((currentNutrition.carbs / nutritionTargets.carbs) * 100, 100);
            document.getElementById('carb-bar').style.width = carbPercent + '%';
            document.getElementById('carb-text').textContent = `${Math.round(currentNutrition.carbs * 10) / 10}g / ${nutritionTargets.carbs}g`;
            document.getElementById('carb-percent').textContent = Math.round(carbPercent) + '%';
            
            // Fat bar
            const fatPercent = Math.min((currentNutrition.fat / nutritionTargets.fat) * 100, 100);
            document.getElementById('fat-bar').style.width = fatPercent + '%';
            document.getElementById('fat-text').textContent = `${Math.round(currentNutrition.fat * 10) / 10}g / ${nutritionTargets.fat}g`;
            document.getElementById('fat-percent').textContent = Math.round(fatPercent) + '%';
        }

        // Lấy dinh dưỡng hiện tại
        function getCurrentNutrition() {
            let totalProtein = 0;
            let totalCarbs = 0;
            let totalFat = 0;
            
            Object.values(todayMeals).forEach(meals => {
                meals.forEach(meal => {
                    totalProtein += meal.protein;
                    totalCarbs += meal.carbs;
                    totalFat += meal.fat;
                });
            });
            
            return {
                protein: totalProtein,
                carbs: totalCarbs,
                fat: totalFat
            };
        }

        // Toggle form thêm thực phẩm mới
        function toggleAddForm() {
            const form = document.getElementById('add-food-form');
            form.classList.toggle('active');
            
            if (!form.classList.contains('active')) {
                // Reset form
                document.getElementById('new-food-name').value = '';
                document.getElementById('new-food-calories').value = '';
                document.getElementById('new-food-protein').value = '';
                document.getElementById('new-food-carbs').value = '';
                document.getElementById('new-food-fat').value = '';
            }
        }

        // Thêm thực phẩm mới vào database
        function addNewFood() {
            const name = document.getElementById('new-food-name').value.trim();
            const calories = parseFloat(document.getElementById('new-food-calories').value);
            const protein = parseFloat(document.getElementById('new-food-protein').value);
            const carbs = parseFloat(document.getElementById('new-food-carbs').value);
            const fat = parseFloat(document.getElementById('new-food-fat').value);
            
            if (!name || !calories || isNaN(protein) || isNaN(carbs) || isNaN(fat)) {
                alert('Vui lòng điền đầy đủ thông tin!');
                return;
            }
            
            const newFood = {
                name: name,
                calories: calories,
                protein: protein,
                carbs: carbs,
                fat: fat
            };
            
            foodDatabase.push(newFood);
            displayFoodList();
            toggleAddForm();
            
            alert(`Đã thêm "${name}" vào cơ sở dữ liệu!`);
        }

        // Xóa tất cả bữa ăn
        function clearAllMeals() {
            if (confirm('Bạn có chắc muốn xóa tất cả bữa ăn?')) {
                todayMeals = {
                    breakfast: [],
                    lunch: [],
                    dinner: [],
                    snack: []
                };
                updateMealDisplay();
                updateTotalNutrition();
                updateNutritionBars();
            }
        }

        // Lưu dữ liệu vào localStorage (cho phiên bản tương lai)
        function saveData() {
            try {
                localStorage.setItem('byebeo_meals', JSON.stringify(todayMeals));
                localStorage.setItem('byebeo_targets', JSON.stringify(nutritionTargets));
                localStorage.setItem('byebeo_custom_foods', JSON.stringify(foodDatabase.slice(49))); // Chỉ lưu món tự thêm
            } catch (e) {
                console.log('Không thể lưu dữ liệu:', e);
            }
        }

        // Tải dữ liệu từ localStorage
        function loadData() {
            try {
                const savedMeals = localStorage.getItem('byebeo_meals');
                const savedTargets = localStorage.getItem('byebeo_targets');
                const savedCustomFoods = localStorage.getItem('byebeo_custom_foods');
                
                if (savedMeals) {
                    todayMeals = JSON.parse(savedMeals);
                }
                
                if (savedTargets) {
                    nutritionTargets = JSON.parse(savedTargets);
                    // Hiển thị lại targets
                    if (nutritionTargets.calories > 0) {
                        document.getElementById('target-calories').textContent = nutritionTargets.calories;
                        document.getElementById('protein-target').textContent = nutritionTargets.protein;
                        document.getElementById('carb-target').textContent = nutritionTargets.carbs;
                        document.getElementById('fat-target').textContent = nutritionTargets.fat;
                    }
                }
                
                if (savedCustomFoods) {
                    const customFoods = JSON.parse(savedCustomFoods);
                    foodDatabase = [...foodDatabase.slice(0, 49), ...customFoods]; // Ghép với 49 món gốc
                }
            } catch (e) {
                console.log('Không thể tải dữ liệu:', e);
            }
        }

        // Tự động lưu khi có thay đổi
        function autoSave() {
            saveData();
        }

        // Export dữ liệu dưới dạng JSON
        function exportData() {
            const data = {
                meals: todayMeals,
                targets: nutritionTargets,
                customFoods: foodDatabase.slice(49),
                exportDate: new Date().toISOString()
            };
            
            const dataStr = JSON.stringify(data, null, 2);
            const dataBlob = new Blob([dataStr], {type: 'application/json'});
            const url = URL.createObjectURL(dataBlob);
            
            const link = document.createElement('a');
            link.href = url;
            link.download = `byebeo_data_${new Date().toISOString().split('T')[0]}.json`;
            link.click();
            
            URL.revokeObjectURL(url);
        }

        // Reset dữ liệu về mặc định
        function resetAllData() {
            if (confirm('⚠️ Bạn có chắc muốn xóa TẤT CẢ dữ liệu?\n\nĐiều này sẽ xóa:\n- Tất cả bữa ăn\n- Thông tin dinh dưỡng\n- Món ăn tự thêm\n\nHành động này không thể hoàn tác!')) {
                // Reset về trạng thái ban đầu
                todayMeals = {
                    breakfast: [],
                    lunch: [],
                    dinner: [],
                    snack: []
                };
                
                nutritionTargets = {
                    calories: 0,
                    protein: 0,
                    carbs: 0,
                    fat: 0
                };
                
                // Reset foodDatabase về 49 món gốc
                foodDatabase = foodDatabase.slice(0, 49);
                
                // Xóa localStorage
                try {
                    localStorage.removeItem('byebeo_meals');
                    localStorage.removeItem('byebeo_targets');
                    localStorage.removeItem('byebeo_custom_foods');
                } catch (e) {
                    console.log('Không thể xóa localStorage:', e);
                }
                
                // Cập nhật giao diện
                document.getElementById('bmi').textContent = '--';
                document.getElementById('bmr').textContent = '--';
                document.getElementById('tdee').textContent = '--';
                document.getElementById('target-calories').textContent = '--';
                document.getElementById('protein-target').textContent = '--';
                document.getElementById('carb-target').textContent = '--';
                document.getElementById('fat-target').textContent = '--';
                
                updateMealDisplay();
                updateTotalNutrition();
                updateNutritionBars();
                displayFoodList();
                
                alert('✅ Đã reset tất cả dữ liệu về mặc định!');
            }
        }

        // Tính toán khuyến nghị nước uống
        function calculateWaterIntake() {
            const weight = parseFloat(document.getElementById('weight').value) || 60;
            const activity = parseFloat(document.getElementById('activity').value) || 1.55;
            
            // Công thức cơ bản: 35ml/kg + thêm cho hoạt động
            let waterNeeded = weight * 35; // ml
            
            if (activity >= 1.725) {
                waterNeeded += 500; // Thêm 500ml cho người tập nặng
            } else if (activity >= 1.55) {
                waterNeeded += 300; // Thêm 300ml cho người tập vừa
            }
            
            return Math.round(waterNeeded);
        }

        // Hiển thị khuyến nghị nước
        function showWaterRecommendation() {
            const waterNeeded = calculateWaterIntake();
            const liters = (waterNeeded / 1000).toFixed(1);
            
            alert(`💧 Khuyến nghị nước uống cho bạn:\n\n${waterNeeded}ml = ${liters} lít/ngày\n\nBao gồm:\n- Nước lọc: ${Math.round(waterNeeded * 0.7)}ml\n- Trà/café: ${Math.round(waterNeeded * 0.2)}ml\n- Từ thức ăn: ${Math.round(waterNeeded * 0.1)}ml`);
        }

        // Tính BMI và đưa ra lời khuyên
        function getBMIAdvice(bmi) {
            if (bmi < 18.5) {
                return "Thiếu cân - Nên tăng cường dinh dưỡng";
            } else if (bmi >= 18.5 && bmi < 23) {
                return "Bình thường - Duy trì tốt!";
            } else if (bmi >= 23 && bmi < 25) {
                return "Thừa cân nhẹ - Cần chú ý chế độ ăn";
            } else if (bmi >= 25 && bmi < 30) {
                return "Béo phì độ I - Nên giảm cân";
            } else if (bmi >= 30 && bmi < 35) {
                return "Béo phì độ II - Cần giảm cân nghiêm túc";
            } else {
                return "Béo phì độ III - Nên tham khảo bác sĩ";
            }
        }

        // Cập nhật hàm calculateNutrition để hiển thị lời khuyên BMI
        const originalCalculateNutrition = calculateNutrition;
        calculateNutrition = function() {
            originalCalculateNutrition();
            
            // Thêm lời khuyên BMI
            const bmi = parseFloat(document.getElementById('bmi').textContent);
            if (bmi && bmi > 0) {
                const advice = getBMIAdvice(bmi);
                document.getElementById('bmi').title = advice;
                
                // Thêm màu cho BMI
                const bmiElement = document.getElementById('bmi');
                if (bmi < 18.5 || bmi >= 25) {
                    bmiElement.style.color = '#ef4444'; // Đỏ
                } else if (bmi >= 23 && bmi < 25) {
                    bmiElement.style.color = '#f59e0b'; // Vàng
                } else {
                    bmiElement.style.color = '#16a34a'; // Xanh
                }
            }
            
            // Tự động lưu
            autoSave();
        };

        // Override các hàm để tự động lưu
        const originalAddToMeal = addToMeal;
        addToMeal = function() {
            originalAddToMeal();
            autoSave();
        };

        const originalRemoveMealItem = removeMealItem;
        removeMealItem = function(mealType, itemId) {
            originalRemoveMealItem(mealType, itemId);
            autoSave();
        };

        const originalAddNewFood = addNewFood;
        addNewFood = function() {
            originalAddNewFood();
            autoSave();
        };

        // Thêm keyboard shortcuts
        document.addEventListener('keydown', function(e) {
            // Ctrl + S: Lưu dữ liệu
            if (e.ctrlKey && e.key === 's') {
                e.preventDefault();
                saveData();
                alert('💾 Đã lưu dữ liệu!');
            }
            
            // Ctrl + E: Export dữ liệu
            if (e.ctrlKey && e.key === 'e') {
                e.preventDefault();
                exportData();
            }
            
            // Esc: Đóng các form đang mở
            if (e.key === 'Escape') {
                document.getElementById('add-food-form').classList.remove('active');
                document.getElementById('add-to-meal-form').classList.remove('active');
            }
        });

        // Thêm nút utilities vào giao diện
        function addUtilityButtons() {
            const header = document.querySelector('.header');
            const utilityDiv = document.createElement('div');
            utilityDiv.style.marginTop = '15px';
            utilityDiv.innerHTML = `
                <button onclick="showWaterRecommendation()" style="background: #06b6d4; color: white; border: none; padding: 8px 15px; border-radius: 5px; margin: 5px; cursor: pointer;">💧 Khuyến nghị nước</button>
                <button onclick="exportData()" style="background: #3b82f6; color: white; border: none; padding: 8px 15px; border-radius: 5px; margin: 5px; cursor: pointer;">📥 Xuất dữ liệu</button>
                <button onclick="resetAllData()" style="background: #ef4444; color: white; border: none; padding: 8px 15px; border-radius: 5px; margin: 5px; cursor: pointer;">🔄 Reset tất cả</button>
            `;
            header.appendChild(utilityDiv);
        }

        // Cập nhật hàm khởi tạo
        function initApp() {
            loadData(); // Tải dữ liệu trước
            displayFoodList();
            updateMealDisplay();
            updateTotalNutrition();
            updateNutritionBars();
            addUtilityButtons();
            
            // Hiển thị thông báo chào mừng
            if (!localStorage.getItem('byebeo_first_visit')) {
                setTimeout(() => {
                    alert('🌿 Chào mừng đến với Bye Béo MVP!\n\n✨ Tính năng chính:\n• Tính toán BMR, TDEE, Macros\n• Theo dõi bữa ăn hàng ngày\n• 50+ món ăn Việt phổ biến\n• Tự động lưu dữ liệu\n\n💡 Mẹo: Nhấn Ctrl+S để lưu, Ctrl+E để xuất dữ liệu!');
                    localStorage.setItem('byebeo_first_visit', 'true');
                }, 1000);
            }
        }

        // Khởi tạo app khi trang load
        window.addEventListener('load', initApp);

        // Tự động lưu khi đóng trang
        window.addEventListener('beforeunload', function(e) {
            saveData();
        });

        // Debug: Hiển thị thông tin version
        console.log('🌿 Bye Béo MVP v1.0 - Giai đoạn 1');
        console.log('📊 Tính năng: BMR/TDEE calculation, Food logging, Macro tracking');
        console.log('🍽️ Database: 49 món Việt + custom foods');
        console.log('💾 Storage: LocalStorage support');
        console.log('⌨️ Shortcuts: Ctrl+S (save), Ctrl+E (export), Esc (close forms)');
    </script>
</body>
</html>
    </script>
</body>
</html>
