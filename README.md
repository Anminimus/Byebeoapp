<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Bye Béo - Ứng dụng dinh dưỡng thông minh</title>
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
            line-height: 1.6;
        }

        .container {
            max-width: 1400px;
            margin: 0 auto;
            padding: 20px;
        }

        .header {
            background: linear-gradient(135deg, #22c55e, #16a34a);
            color: white;
            padding: 40px;
            border-radius: 25px;
            text-align: center;
            margin-bottom: 40px;
            box-shadow: 0 15px 40px rgba(34, 197, 94, 0.4);
            position: relative;
            overflow: hidden;
        }

        .header::before {
            content: '';
            position: absolute;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
            background: linear-gradient(45deg, transparent, rgba(255,255,255,0.1), transparent);
            transform: rotate(45deg);
            animation: shimmer 3s infinite;
        }

        @keyframes shimmer {
            0% { transform: translateX(-100%) translateY(-100%) rotate(45deg); }
            100% { transform: translateX(100%) translateY(100%) rotate(45deg); }
        }

        .header h1 {
            font-size: 3em;
            margin-bottom: 15px;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
            position: relative;
            z-index: 1;
        }

        .subtitle {
            font-size: 1.2em;
            opacity: 0.95;
            position: relative;
            z-index: 1;
        }

        .main-content {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 40px;
            margin-bottom: 40px;
        }

        .card {
            background: white;
            border-radius: 20px;
            padding: 30px;
            box-shadow: 0 8px 30px rgba(0,0,0,0.12);
            border: 3px solid #e5e7eb;
            transition: transform 0.3s ease, box-shadow 0.3s ease;
            position: relative;
            overflow: hidden;
        }

        .card:hover {
            transform: translateY(-5px);
            box-shadow: 0 15px 40px rgba(0,0,0,0.15);
        }

        .card::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            height: 4px;
            background: linear-gradient(90deg, #22c55e, #16a34a, #22c55e);
            background-size: 200% 100%;
            animation: gradient 3s ease infinite;
        }

        @keyframes gradient {
            0% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
            100% { background-position: 0% 50%; }
        }

        .card h2 {
            color: #16a34a;
            margin-bottom: 25px;
            font-size: 1.8em;
            display: flex;
            align-items: center;
            gap: 12px;
            font-weight: 700;
        }

        .form-group {
            margin-bottom: 20px;
            position: relative;
        }

        .form-group label {
            display: block;
            margin-bottom: 8px;
            font-weight: 600;
            color: #374151;
            font-size: 1.05em;
        }

        .form-group input, .form-group select {
            width: 100%;
            padding: 15px;
            border: 2px solid #d1d5db;
            border-radius: 12px;
            font-size: 16px;
            transition: all 0.3s ease;
            background: #f9fafb;
        }

        .form-group input:focus, .form-group select:focus {
            outline: none;
            border-color: #22c55e;
            background: white;
            box-shadow: 0 0 0 3px rgba(34, 197, 94, 0.1);
            transform: translateY(-2px);
        }

        .btn {
            background: linear-gradient(135deg, #22c55e, #16a34a);
            color: white;
            border: none;
            padding: 15px 30px;
            border-radius: 12px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            width: 100%;
            font-size: 16px;
            margin-top: 10px;
            position: relative;
            overflow: hidden;
        }

        .btn::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255,255,255,0.2), transparent);
            transition: left 0.5s;
        }

        .btn:hover::before {
            left: 100%;
        }

        .btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 10px 25px rgba(34, 197, 94, 0.4);
        }

        .btn:active {
            transform: translateY(-1px);
        }

        .btn-secondary {
            background: linear-gradient(135deg, #3b82f6, #2563eb);
        }

        .btn-secondary:hover {
            box-shadow: 0 10px 25px rgba(59, 130, 246, 0.4);
        }

        .btn-danger {
            background: linear-gradient(135deg, #ef4444, #dc2626);
        }

        .btn-danger:hover {
            box-shadow: 0 10px 25px rgba(239, 68, 68, 0.4);
        }

        .btn-warning {
            background: linear-gradient(135deg, #f59e0b, #d97706);
        }

        .btn-warning:hover {
            box-shadow: 0 10px 25px rgba(245, 158, 11, 0.4);
        }

        .btn-info {
            background: linear-gradient(135deg, #06b6d4, #0891b2);
        }

        .btn-info:hover {
            box-shadow: 0 10px 25px rgba(6, 182, 212, 0.4);
        }

        .stats-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(160px, 1fr));
            gap: 20px;
            margin: 25px 0;
        }

        .stat-item {
            background: linear-gradient(135deg, #f0fdf4, #dcfce7);
            padding: 20px;
            border-radius: 15px;
            text-align: center;
            border: 3px solid #22c55e;
            transition: all 0.3s ease;
            position: relative;
            overflow: hidden;
        }

        .stat-item::before {
            content: '';
            position: absolute;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
            background: radial-gradient(circle, rgba(34, 197, 94, 0.1) 0%, transparent 70%);
            transform: scale(0);
            transition: transform 0.3s ease;
        }

        .stat-item:hover::before {
            transform: scale(1);
        }

        .stat-item:hover {
            transform: scale(1.05);
            box-shadow: 0 10px 30px rgba(34, 197, 94, 0.3);
        }

        .stat-number {
            font-size: 2.2em;
            font-weight: bold;
            color: #16a34a;
            position: relative;
            z-index: 1;
        }

        .stat-label {
            font-size: 1em;
            color: #6b7280;
            margin-top: 8px;
            font-weight: 500;
            position: relative;
            z-index: 1;
        }

        .food-log {
            grid-column: 1 / -1;
        }

        .food-search {
            display: flex;
            gap: 15px;
            margin-bottom: 20px;
        }

        .food-search input {
            flex: 1;
        }

        .food-list {
            max-height: 300px;
            overflow-y: auto;
            border: 3px solid #e5e7eb;
            border-radius: 15px;
            margin-bottom: 20px;
            background: #f9fafb;
        }

        .food-item {
            padding: 15px;
            border-bottom: 2px solid #e5e7eb;
            display: flex;
            justify-content: space-between;
            align-items: center;
            cursor: pointer;
            transition: all 0.3s ease;
            position: relative;
        }

        .food-item::before {
            content: '';
            position: absolute;
            left: 0;
            top: 0;
            bottom: 0;
            width: 4px;
            background: #22c55e;
            transform: scaleY(0);
            transition: transform 0.3s ease;
        }

        .food-item:hover::before {
            transform: scaleY(1);
        }

        .food-item:hover {
            background: linear-gradient(90deg, #f0fdf4, #f9fafb);
            transform: translateX(5px);
        }

        .food-item:last-child {
            border-bottom: none;
        }

        .food-name {
            font-weight: 600;
            flex: 1;
            font-size: 1.1em;
        }

        .food-calories {
            color: #6b7280;
            font-size: 0.95em;
            font-weight: 500;
        }

        .add-food-form {
            background: linear-gradient(135deg, #f9fafb, #f3f4f6);
            padding: 25px;
            border-radius: 15px;
            margin-top: 20px;
            display: none;
            border: 2px solid #e5e7eb;
        }

        .add-food-form.active {
            display: block;
            animation: slideDown 0.3s ease;
        }

        @keyframes slideDown {
            from {
                opacity: 0;
                transform: translateY(-20px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .quantity-input {
            display: flex;
            gap: 15px;
            align-items: center;
            margin: 20px 0;
        }

        .today-log {
            margin-top: 30px;
        }

        .meal-section {
            margin-bottom: 25px;
            background: linear-gradient(135deg, #f8fafc, #f1f5f9);
            padding: 20px;
            border-radius: 15px;
            border: 2px solid #e2e8f0;
            position: relative;
            overflow: hidden;
        }

        .meal-section::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            height: 3px;
            background: linear-gradient(90deg, #22c55e, #16a34a);
        }

        .meal-title {
            font-weight: bold;
            color: #16a34a;
            margin-bottom: 15px;
            font-size: 1.3em;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .logged-food {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 12px 0;
            border-bottom: 1px solid #e5e7eb;
            transition: all 0.3s ease;
        }

        .logged-food:hover {
            background: rgba(34, 197, 94, 0.05);
            border-radius: 8px;
            padding-left: 10px;
            padding-right: 10px;
        }

        .logged-food:last-child {
            border-bottom: none;
        }

        .delete-btn {
            background: #ef4444;
            color: white;
            border: none;
            padding: 8px 12px;
            border-radius: 8px;
            cursor: pointer;
            font-size: 12px;
            transition: all 0.3s ease;
        }

        .delete-btn:hover {
            background: #dc2626;
            transform: scale(1.1);
        }

        .macro-bar {
            background: #e5e7eb;
            height: 25px;
            border-radius: 15px;
            overflow: hidden;
            margin: 15px 0;
            position: relative;
            box-shadow: inset 0 2px 4px rgba(0,0,0,0.1);
        }

        .macro-fill {
            height: 100%;
            border-radius: 15px;
            transition: width 0.8s ease;
            position: relative;
            overflow: hidden;
        }

        .macro-fill::after {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255,255,255,0.3), transparent);
            animation: progress-shine 2s infinite;
        }

        @keyframes progress-shine {
            0% { left: -100%; }
            100% { left: 100%; }
        }

        .protein-fill { 
            background: linear-gradient(90deg, #ef4444, #dc2626);
        }
        .carb-fill { 
            background: linear-gradient(90deg, #3b82f6, #2563eb);
        }
        .fat-fill { 
            background: linear-gradient(90deg, #f59e0b, #d97706);
        }

        .macro-text {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            font-size: 13px;
            font-weight: bold;
            color: white;
            text-shadow: 1px 1px 2px rgba(0,0,0,0.7);
            z-index: 2;
        }

        .meal-plan-container {
            margin-top: 30px;
            grid-column: 1 / -1;
        }

        .generated-meal {
            background: linear-gradient(135deg, #fef3c7, #fde68a);
            border: 2px solid #f59e0b;
            border-radius: 15px;
            padding: 20px;
            margin: 15px 0;
            position: relative;
            overflow: hidden;
        }

        .generated-meal::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            height: 3px;
            background: linear-gradient(90deg, #f59e0b, #d97706);
        }

        .meal-foods {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 15px;
            margin-top: 15px;
        }

        .food-suggestion {
            background: white;
            padding: 15px;
            border-radius: 10px;
            border: 2px solid #e5e7eb;
            transition: all 0.3s ease;
        }

        .food-suggestion:hover {
            transform: translateY(-3px);
            box-shadow: 0 8px 20px rgba(0,0,0,0.1);
        }

        .progress-ring {
            width: 120px;
            height: 120px;
            margin: 0 auto;
        }

        .progress-ring__circle {
            stroke: #e5e7eb;
            fill: transparent;
            stroke-width: 8;
            r: 52;
            cx: 60;
            cy: 60;
        }

        .progress-ring__progress {
            stroke: #22c55e;
            fill: transparent;
            stroke-width: 8;
            r: 52;
            cx: 60;
            cy: 60;
            stroke-dasharray: 326.73;
            stroke-dashoffset: 326.73;
            transform: rotate(-90deg);
            transform-origin: 50% 50%;
            transition: stroke-dashoffset 0.8s ease;
        }

        .notification {
            position: fixed;
            top: 20px;
            right: 20px;
            background: #22c55e;
            color: white;
            padding: 15px 25px;
            border-radius: 10px;
            box-shadow: 0 10px 30px rgba(34, 197, 94, 0.3);
            transform: translateX(400px);
            transition: transform 0.3s ease;
            z-index: 1000;
        }

        .notification.show {
            transform: translateX(0);
        }

        .loading {
            display: inline-block;
            width: 20px;
            height: 20px;
            border: 3px solid rgba(255,255,255,.3);
            border-radius: 50%;
            border-top-color: #fff;
            animation: spin 1s ease-in-out infinite;
        }

        @keyframes spin {
            to { transform: rotate(360deg); }
        }

        .tooltip {
            position: relative;
            cursor: help;
        }

        .tooltip::after {
            content: attr(data-tooltip);
            position: absolute;
            bottom: 100%;
            left: 50%;
            transform: translateX(-50%);
            background: #1f2937;
            color: white;
            padding: 8px 12px;
            border-radius: 6px;
            font-size: 12px;
            white-space: nowrap;
            opacity: 0;
            pointer-events: none;
            transition: opacity 0.3s;
            z-index: 1000;
        }

        .tooltip:hover::after {
            opacity: 1;
        }

        .accordion {
            margin: 20px 0;
        }

        .accordion-header {
            background: #f3f4f6;
            padding: 15px;
            border-radius: 10px;
            cursor: pointer;
            display: flex;
            justify-content: space-between;
            align-items: center;
            transition: all 0.3s ease;
        }

        .accordion-header:hover {
            background: #e5e7eb;
        }

        .accordion-content {
            max-height: 0;
            overflow: hidden;
            transition: max-height 0.3s ease;
            background: #f9fafb;
            border-radius: 0 0 10px 10px;
        }

        .accordion-content.open {
            max-height: 500px;
            padding: 20px;
        }

        .floating-action {
            position: fixed;
            bottom: 30px;
            right: 30px;
            width: 60px;
            height: 60px;
            background: linear-gradient(135deg, #22c55e, #16a34a);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-size: 24px;
            cursor: pointer;
            box-shadow: 0 10px 30px rgba(34, 197, 94, 0.4);
            transition: all 0.3s ease;
            z-index: 1000;
        }

        .floating-action:hover {
            transform: scale(1.1) rotate(360deg);
        }

        .modal {
            display: none;
            position: fixed;
            z-index: 2000;
            left: 0;
            top: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.5);
            backdrop-filter: blur(5px);
        }

        .modal-content {
            background: white;
            margin: 5% auto;
            padding: 30px;
            border-radius: 20px;
            width: 90%;
            max-width: 600px;
            position: relative;
            animation: modalSlideIn 0.3s ease;
        }

        @keyframes modalSlideIn {
            from {
                opacity: 0;
                transform: translateY(-50px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .close {
            position: absolute;
            right: 20px;
            top: 20px;
            font-size: 30px;
            cursor: pointer;
            color: #6b7280;
            transition: color 0.3s ease;
        }

        .close:hover {
            color: #ef4444;
        }

        .tabs {
            display: flex;
            margin-bottom: 20px;
            border-radius: 10px;
            overflow: hidden;
            background: #f3f4f6;
        }

        .tab {
            flex: 1;
            padding: 15px;
            text-align: center;
            cursor: pointer;
            transition: all 0.3s ease;
            background: #f3f4f6;
        }

        .tab.active {
            background: #22c55e;
            color: white;
        }

        .tab-content {
            display: none;
        }

        .tab-content.active {
            display: block;
            animation: fadeIn 0.3s ease;
        }

        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }

        @media (max-width: 768px) {
            .main-content {
                grid-template-columns: 1fr;
                gap: 20px;
            }
            
            .stats-grid {
                grid-template-columns: repeat(2, 1fr);
            }

            .header h1 {
                font-size: 2em;
            }

            .meal-foods {
                grid-template-columns: 1fr;
            }

            .container {
                padding: 10px;
            }
        }

        /* Custom scrollbar */
        ::-webkit-scrollbar {
            width: 8px;
        }

        ::-webkit-scrollbar-track {
            background: #f1f1f1;
            border-radius: 4px;
        }

        ::-webkit-scrollbar-thumb {
            background: #22c55e;
            border-radius: 4px;
        }

        ::-webkit-scrollbar-thumb:hover {
            background: #16a34a;
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>🌿 BYE BÉO PRO</h1>
            <p class="subtitle">Ứng dụng theo dõi dinh dưỡng thông minh với AI</p>
        </div>

        <div class="main-content">
            <!-- Thông tin cá nhân và tính toán -->
            <div class="card">
                <h2>👤 Thông tin cá nhân</h2>
                <div class="form-group">
                    <label class="tooltip" data-tooltip="Tuổi từ 16-80">Tuổi:</label>
                    <input type="number" id="age" value="25" min="16" max="80">
                </div>
                <div class="form-group">
                    <label>Giới tính:</label>
                    <select id="gender">
                        <option value="female">👩 Nữ</option>
                        <option value="male">👨 Nam</option>
                    </select>
                </div>
                <div class="form-group">
                    <label class="tooltip" data-tooltip="Cân nặng hiện tại">Cân nặng (kg):</label>
                    <input type="number" id="weight" value="60" step="0.1" min="30" max="200">
                </div>
                <div class="form-group">
                    <label class="tooltip" data-tooltip="Chiều cao không giày">Chiều cao (cm):</label>
                    <input type="number" id="height" value="165" step="0.1" min="120" max="220">
                </div>
                <div class="form-group">
                    <label class="tooltip" data-tooltip="Mức độ vận động hàng tuần">Mức độ hoạt động:</label>
                    <select id="activity">
                        <option value="1.2">😴 Ít vận động (công việc văn phòng)</option>
                        <option value="1.375">🚶 Nhẹ (1-3 ngày/tuần)</option>
                        <option value="1.55" selected>🏃 Vừa (3-5 ngày/tuần)</option>
                        <option value="1.725">💪 Nặng (6-7 ngày/tuần)</option>
                        <option value="1.9">🔥 Rất nặng (2 lần/ngày hoặc công việc nặng)</option>
                    </select>
                </div>
                <div class="form-group">
                    <label class="tooltip" data-tooltip="Mục tiêu giảm/tăng cân">Mục tiêu:</label>
                    <select id="goal">
                        <option value="-750">📉 Giảm cân nhanh (0.75kg/tuần)</option>
                        <option value="-500" selected>📊 Giảm cân (0.5kg/tuần)</option>
                        <option value="-250">📈 Giảm cân nhẹ (0.25kg/tuần)</option>
                        <option value="0">⚖️ Duy trì cân nặng</option>
                        <option value="250">📈 Tăng cân nhẹ (0.25kg/tuần)</option>
                        <option value="500">📊 Tăng cân (0.5kg/tuần)</option>
                        <option value="750">📉 Tăng cân nhanh (0.75kg/tuần)</option>
                    </select>
                </div>
                <div class="form-group">
                    <label class="tooltip" data-tooltip="Số bữa ăn trong ngày">Số bữa/ngày:</label>
                    <select id="meal-frequency">
                        <option value="3">🍽️ 3 bữa (Sáng, Trưa, Tối)</option>
                        <option value="4">🍽️ 4 bữa (+ Ăn vặt)</option>
                        <option value="5" selected>🍽️ 5 bữa (+ 2 bữa phụ)</option>
                        <option value="6">🍽️ 6 bữa (Ăn nhiều bữa nhỏ)</option>
                    </select>
                </div>
                <div class="form-group">
                    <label class="tooltip" data-tooltip="Tỷ lệ phân chia chất dinh dưỡng">Tỷ lệ Macro (% Carb : Protein : Fat):</label>
                    <select id="macro-ratio">
                        <option value="40-30-30" selected>⚖️ 40:30:30 (Cân bằng)</option>
                        <option value="50-25-25">🌾 50:25:25 (High Carb - Tăng cơ)</option>
                        <option value="30-40-30">🥩 30:40:30 (High Protein - Giảm mỡ)</option>
                        <option value="20-25-55">🥑 20:25:55 (Keto Diet)</option>
                        <option value="45-35-20">💪 45:35:20 (Athlete)</option>
                    </select>
                </div>
                <button class="btn" onclick="calculateNutrition()">
                    <span id="calc-btn-text">📊 Tính toán dinh dưỡng</span>
                </button>
                <button class="btn btn-secondary" onclick="generateMealPlan()" id="meal-plan-btn" disabled>
                    📋 Tạo thực đơn tự động
                </button>
                <button class="btn btn-warning" onclick="exportToPDF()">
                    📄 Xuất PDF
                </button>
                <button class="btn btn-info" onclick="shareResults()">
                    📤 Chia sẻ kết quả
                </button>
            </div>

            <!-- Hiển thị kết quả tính toán -->
            <div class="card">
                <h2>📊 Chỉ số dinh dưỡng</h2>
                <div class="stats-grid">
                    <div class="stat-item tooltip" data-tooltip="Chỉ số khối cơ thể">
                        <div class="stat-number" id="bmi">--</div>
                        <div class="stat-label">BMI</div>
                    </div>
                    <div class="stat-item tooltip" data-tooltip="Trao đổi chất cơ bản">
                        <div class="stat-number" id="bmr">--
