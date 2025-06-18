<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>صيدليات العراق</title>
    <meta name="description" content="تطبيق صيدليات العراق - اعثر على أقرب صيدلية ودواء في العراق">
    <link rel="icon" href="data:image/svg+xml,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'><text y='.9em' font-size='90'>⚕️</text></svg>">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            color: #333;
        }
        
        .container {
            max-width: 400px;
            margin: 0 auto;
            background: white;
            min-height: 100vh;
            box-shadow: 0 0 20px rgba(0,0,0,0.1);
        }
        
        .header {
            background: linear-gradient(135deg, #16a34a, #2563eb);
            color: white;
            padding: 20px;
            text-align: center;
        }
        
        .header h1 {
            font-size: 24px;
            margin-bottom: 5px;
        }
        
        .header p {
            font-size: 14px;
            opacity: 0.9;
        }
        
        .main-content {
            padding: 20px;
        }
        
        .search-section {
            margin-bottom: 30px;
        }
        
        .search-box {
            position: relative;
            margin-bottom: 20px;
        }
        
        .search-input {
            width: 100%;
            padding: 15px 50px 15px 15px;
            border: 2px solid #e5e7eb;
            border-radius: 12px;
            font-size: 16px;
            outline: none;
            transition: border-color 0.3s;
        }
        
        .search-input:focus {
            border-color: #2563eb;
        }
        
        .search-icon {
            position: absolute;
            left: 15px;
            top: 50%;
            transform: translateY(-50%);
            color: #9ca3af;
        }
        
        .map-section {
            background: linear-gradient(135deg, #dbeafe, #dcfce7);
            border-radius: 20px;
            padding: 30px;
            margin-bottom: 30px;
            position: relative;
            min-height: 400px;
        }
        
        .map-title {
            text-align: center;
            background: white;
            display: inline-block;
            padding: 10px 20px;
            border-radius: 25px;
            font-weight: bold;
            color: #16a34a;
            position: absolute;
            top: -15px;
            left: 50%;
            transform: translateX(-50%);
            box-shadow: 0 4px 10px rgba(0,0,0,0.1);
        }
        
        .iraq-map {
            width: 250px;
            height: 300px;
            background: linear-gradient(135deg, #22c55e, #15803d);
            margin: 40px auto 0;
            border-radius: 20px;
            position: relative;
            clip-path: polygon(20% 10%, 80% 5%, 95% 30%, 90% 70%, 70% 95%, 30% 90%, 5% 60%, 10% 20%);
            box-shadow: 0 8px 25px rgba(34, 197, 94, 0.3);
        }
        
        .city-label {
            position: absolute;
            font-size: 12px;
            font-weight: bold;
            color: #064e3b;
            text-shadow: 0 1px 2px rgba(255,255,255,0.8);
        }
        
        .baghdad { top: 45%; right: 45%; font-size: 14px; }
        .basra { bottom: 15%; right: 35%; }
        .erbil { top: 20%; right: 40%; }
        .mosul { top: 25%; right: 45%; }
        
        .pharmacy-dot {
            position: absolute;
            width: 16px;
            height: 16px;
            border-radius: 50%;
            border: 3px solid white;
            cursor: pointer;
            transition: all 0.3s;
            box-shadow: 0 2px 8px rgba(0,0,0,0.3);
        }
        
        .pharmacy-dot:hover {
            transform: scale(1.3);
        }
        
        .pharmacy-dot.open {
            background: #22c55e;
            animation: pulse 2s infinite;
        }
        
        .pharmacy-dot.closed {
            background: #ef4444;
        }
        
        .pharmacy-dot.h24::after {
            content: '';
            position: absolute;
            top: -2px;
            right: -2px;
            width: 8px;
            height: 8px;
            background: #fbbf24;
            border-radius: 50%;
            border: 1px solid white;
        }
        
        @keyframes pulse {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.7; }
        }
        
        .dot1 { top: 42%; right: 45%; }
        .dot2 { top: 45%; right: 48%; }
        .dot3 { bottom: 18%; right: 38%; }
        .dot4 { top: 22%; right: 42%; }
        .dot5 { top: 27%; right: 47%; }
        
        .legend {
            background: white;
            padding: 15px;
            border-radius: 12px;
            margin-top: 20px;
            box-shadow: 0 4px 10px rgba(0,0,0,0.1);
        }
        
        .legend h4 {
            text-align: center;
            margin-bottom: 10px;
            color: #374151;
        }
        
        .legend-item {
            display: flex;
            align-items: center;
            margin-bottom: 8px;
            font-size: 14px;
        }
        
        .legend-dot {
            width: 12px;
            height: 12px;
            border-radius: 50%;
            margin-left: 10px;
            border: 2px solid white;
            box-shadow: 0 1px 3px rgba(0,0,0,0.3);
        }
        
        .legend-dot.open { background: #22c55e; }
        .legend-dot.closed { background: #ef4444; }
        .legend-dot.h24 {
            background: #22c55e;
            position: relative;
        }
        .legend-dot.h24::after {
            content: '';
            position: absolute;
            top: -1px;
            right: -1px;
            width: 6px;
            height: 6px;
            background: #fbbf24;
            border-radius: 50%;
            border: 1px solid white;
        }
        
        .pharmacies-list {
            margin-top: 30px;
        }
        
        .pharmacy-card {
            background: white;
            border-radius: 15px;
            padding: 20px;
            margin-bottom: 15px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.1);
            border-left: 5px solid #22c55e;
            transition: transform 0.3s;
        }
        
        .pharmacy-card:hover {
            transform: translateY(-2px);
        }
        
        .pharmacy-card.closed {
            border-left-color: #ef4444;
            opacity: 0.8;
        }
        
        .pharmacy-name {
            font-size: 18px;
            font-weight: bold;
            color: #1f2937;
            margin-bottom: 8px;
        }
        
        .pharmacy-address {
            color: #6b7280;
            font-size: 14px;
            margin-bottom: 10px;
        }
        
        .pharmacy-info {
            display: flex;
            justify-content: space-between;
            align-items: center;
            flex-wrap: wrap;
            gap: 10px;
        }
        
        .pharmacy-hours {
            font-size: 14px;
            color: #374151;
        }
        
        .pharmacy-status {
            padding: 5px 12px;
            border-radius: 20px;
            font-size: 12px;
            font-weight: bold;
        }
        
        .status-open {
            background: #dcfce7;
            color: #166534;
        }
        
        .status-closed {
            background: #fee2e2;
            color: #991b1b;
        }
        
        .pharmacy-phone {
            color: #2563eb;
            text-decoration: none;
            font-weight: 500;
            font-size: 14px;
        }
        
        .pharmacy-phone:hover {
            text-decoration: underline;
        }
        
        .medicines-list {
            margin-top: 10px;
            display: flex;
            flex-wrap: wrap;
            gap: 5px;
        }
        
        .medicine-tag {
            background: #dbeafe;
            color: #1e40af;
            padding: 3px 8px;
            border-radius: 8px;
            font-size: 12px;
        }
        
        .footer {
            background: #f9fafb;
            padding: 20px;
            text-align: center;
            color: #6b7280;
            border-top: 1px solid #e5e7eb;
        }
        
        .search-results {
            background: #fef3c7;
            border: 1px solid #f59e0b;
            border-radius: 12px;
            padding: 15px;
            margin-bottom: 20px;
        }
        
        .search-results h3 {
            color: #92400e;
            margin-bottom: 10px;
        }
        
        .no-results {
            text-align: center;
            color: #6b7280;
            font-style: italic;
        }
        
        @media (max-width: 480px) {
            .container {
                max-width: 100%;
            }
            
            .main-content {
                padding: 15px;
            }
            
            .iraq-map {
                width: 200px;
                height: 250px;
            }
            
            .pharmacy-info {
                flex-direction: column;
                align-items: stretch;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>⚕️ صيدليات العراق</h1>
            <p>أسرع طريقة للعثور على الدواء</p>
        </div>
        
        <div class="main-content">
            <div class="search-section">
                <h2 style="margin-bottom: 15px; color: #374151;">🔍 البحث عن الأدوية</h2>
                <div class="search-box">
                    <input type="text" class="search-input" id="searchInput" placeholder="ابحث عن دواء (مثال: بنادول، أسبرين...)">
                    <span class="search-icon">🔍</span>
                </div>
                <div id="searchResults"></div>
            </div>
            
            <div class="map-section">
                <div class="map-title">🗺️ خريطة العراق</div>
                
                <div class="iraq-map">
                    <div class="city-label baghdad">بغداد</div>
                    <div class="city-label basra">البصرة</div>
                    <div class="city-label erbil">أربيل</div>
                    <div class="city-label mosul">الموصل</div>
                    
                    <div class="pharmacy-dot open dot1" title="صيدلية النور - بغداد"></div>
                    <div class="pharmacy-dot open h24 dot2" title="صيدلية الشفاء 24/7 - بغداد"></div>
                    <div class="pharmacy-dot closed dot3" title="صيدلية البصرة الحديثة - البصرة"></div>
                    <div class="pharmacy-dot open dot4" title="صيدلية أربيل المركزية - أربيل"></div>
                    <div class="pharmacy-dot open dot5" title="صيدلية الموصل الطبية - الموصل"></div>
                </div>
                
                <div class="legend">
                    <h4>🎨 دليل الألوان</h4>
                    <div class="legend-item">
                        <div class="legend-dot open"></div>
                        <span>صيدلية مفتوحة</span>
                    </div>
                    <div class="legend-item">
                        <div class="legend-dot closed"></div>
                        <span>صيدلية مغلقة</span>
                    </div>
                    <div class="legend-item">
                        <div class="legend-dot h24"></div>
                        <span>مفتوحة 24/7</span>
                    </div>
                </div>
            </div>
            
            <div class="pharmacies-list">
                <h2 style="margin-bottom: 20px; color: #374151;">🏥 دليل الصيدليات</h2>
                
                <div class="pharmacy-card">
                    <div class="pharmacy-name">صيدلية النور</div>
                    <div class="pharmacy-address">📍 شارع الرشيد، بغداد</div>
                    <div class="pharmacy-info">
                        <div class="pharmacy-hours">🕐 8:00 ص - 11:00 م</div>
                        <div class="pharmacy-status status-open">مفتوحة الآن</div>
                    </div>
                    <div class="pharmacy-info" style="margin-top: 10px;">
                        <a href="tel:+96412345678" class="pharmacy-phone">📞 +964 1 234 5678</a>
                        <div style="font-size: 12px; color: #f59e0b;">⭐ 4.5</div>
                    </div>
                    <div class="medicines-list">
                        <span class="medicine-tag">بنادول</span>
                        <span class="medicine-tag">أسبرين</span>
                        <span class="medicine-tag">أموكسيسيلين</span>
                        <span class="medicine-tag">فيتامين د</span>
                        <span class="medicine-tag">أوميجا 3</span>
                    </div>
                </div>
                
                <div class="pharmacy-card">
                    <div class="pharmacy-name">صيدلية الشفاء 24/7</div>
                    <div class="pharmacy-address">📍 حي الجادرية، بغداد</div>
                    <div class="pharmacy-info">
                        <div class="pharmacy-hours">🕐 24/7</div>
                        <div class="pharmacy-status status-open">مفتوحة الآن</div>
                    </div>
                    <div class="pharmacy-info" style="margin-top: 10px;">
                        <a href="tel:+96413456789" class="pharmacy-phone">📞 +964 1 345 6789</a>
                        <div style="font-size: 12px; color: #f59e0b;">⭐ 4.8</div>
                    </div>
                    <div class="medicines-list">
                        <span class="medicine-tag">إنسولين</span>
                        <span class="medicine-tag">ضغط الدم</span>
                        <span class="medicine-tag">مضاد حيوي</span>
                        <span class="medicine-tag">بنادول</span>
                        <span class="medicine-tag">فيتامين ب12</span>
                    </div>
                </div>
                
                <div class="pharmacy-card closed">
                    <div class="pharmacy-name">صيدلية البصرة الحديثة</div>
                    <div class="pharmacy-address">📍 كورنيش البصرة، البصرة</div>
                    <div class="pharmacy-info">
                        <div class="pharmacy-hours">🕐 9:00 ص - 10:00 م</div>
                        <div class="pharmacy-status status-closed">مغلقة</div>
                    </div>
                    <div class="pharmacy-info" style="margin-top: 10px;">
                        <a href="tel:+96440123456" class="pharmacy-phone">📞 +964 40 123 456</a>
                        <div style="font-size: 12px; color: #f59e0b;">⭐ 4.2</div>
                    </div>
                    <div class="medicines-list">
                        <span class="medicine-tag">أدوية القلب</span>
                        <span class="medicine-tag">مسكنات</span>
                        <span class="medicine-tag">أدوية الأطفال</span>
                        <span class="medicine-tag">فيتامينات</span>
                    </div>
                </div>
                
                <div class="pharmacy-card">
                    <div class="pharmacy-name">صيدلية أربيل المركزية</div>
                    <div class="pharmacy-address">📍 شارع 60 متر، أربيل</div>
                    <div class="pharmacy-info">
                        <div class="pharmacy-hours">🕐 8:30 ص - 11:30 م</div>
                        <div class="pharmacy-status status-open">مفتوحة الآن</div>
                    </div>
                    <div class="pharmacy-info" style="margin-top: 10px;">
                        <a href="tel:+96466789012" class="pharmacy-phone">📞 +964 66 789 012</a>
                        <div style="font-size: 12px; color: #f59e0b;">⭐ 4.6</div>
                    </div>
                    <div class="medicines-list">
                        <span class="medicine-tag">أدوية السكري</span>
                        <span class="medicine-tag">مضادات الالتهاب</span>
                        <span class="medicine-tag">فيتامينات</span>
                        <span class="medicine-tag">أدوية الضغط</span>
                    </div>
                </div>
                
                <div class="pharmacy-card">
                    <div class="pharmacy-name">صيدلية الموصل الطبية</div>
                    <div class="pharmacy-address">📍 الساعة، الموصل</div>
                    <div class="pharmacy-info">
                        <div class="pharmacy-hours">🕐 7:00 ص - 12:00 ص</div>
                        <div class="pharmacy-status status-open">مفتوحة الآن</div>
                    </div>
                    <div class="pharmacy-info" style="margin-top: 10px;">
                        <a href="tel:+96460456789" class="pharmacy-phone">📞 +964 60 456 789</a>
                        <div style="font-size: 12px; color: #f59e0b;">⭐ 4.3</div>
                    </div>
                    <div class="medicines-list">
                        <span class="medicine-tag">مسكنات قوية</span>
                        <span class="medicine-tag">أدوية عصبية</span>
                        <span class="medicine-tag">مضادات حيوية</span>
                        <span class="medicine-tag">أسبرين</span>
                    </div>
                </div>
            </div>
        </div>
        
        <div class="footer">
            <p>© 2025 تطبيق صيدليات العراق - جميع الحقوق محفوظة</p>
            <p style="margin-top: 5px; font-size: 12px;">للاستفسارات: info@iraq-pharmacy.com</p>
        </div>
    </div>

    <script>
        // البحث عن الأدوية
        const searchInput = document.getElementById('searchInput');
        const searchResults = document.getElementById('searchResults');
        
        const pharmacies = [
            {
                name: 'صيدلية النور',
                address: 'شارع الرشيد، بغداد',
                medicines: ['بنادول', 'أسبرين', 'أموكسيسيلين', 'فيتامين د', 'أوميجا 3'],
                status: 'مفتوحة',
                phone: '+964 1 234 5678'
            },
            {
                name: 'صيدلية الشفاء 24/7',
                address: 'حي الجادرية، بغداد',
                medicines: ['إنسولين', 'ضغط الدم', 'مضاد حيوي', 'بنادول', 'فيتامين ب12'],
                status: 'مفتوحة',
                phone: '+964 1 345 6789'
            },
            {
                name: 'صيدلية البصرة الحديثة',
                address: 'كورنيش البصرة، البصرة',
                medicines: ['أدوية القلب', 'مسكنات', 'أدوية الأطفال', 'فيتامينات'],
                status: 'مغلقة',
                phone: '+964 40 123 456'
            },
            {
                name: 'صيدلية أربيل المركزية',
                address: 'شارع 60 متر، أربيل',
                medicines: ['أدوية السكري', 'مضادات الالتهاب', 'فيتامينات', 'أدوية الضغط'],
                status: 'مفتوحة',
                phone: '+964 66 789 012'
            },
            {
                name: 'صيدلية الموصل الطبية',
                address: 'الساعة، الموصل',
                medicines: ['مسكنات قوية', 'أدوية عصبية', 'مضادات حيوية', 'أسبرين'],
                status: 'مفتوحة',
                phone: '+964 60 456 789'
            }
        ];
        
        searchInput.addEventListener('input', function() {
            const query = this.value.trim().toLowerCase();
            
            if (query === '') {
                searchResults.innerHTML = '';
                return;
            }
            
            const results = pharmacies.filter(pharmacy => {
                return pharmacy.medicines.some(medicine => 
                    medicine.toLowerCase().includes(query)
                ) || pharmacy.name.toLowerCase().includes(query);
            });
            
            if (results.length > 0) {
                let html = '<div class="search-results">';
                html += '<h3>🎯 نتائج البحث عن "' + query + '":</h3>';
                
                results.forEach(pharmacy => {
                    const matchingMedicines = pharmacy.medicines.filter(medicine => 
                        medicine.toLowerCase().includes(query)
                    );
                    
                    html += '<div style="margin-bottom: 15px; padding: 10px; background: white; border-radius: 8px; border-left: 3px solid #22c55e;">';
                    html += '<strong>' + pharmacy.name + '</strong><br>';
                    html += '<small style="color: #6b7280;">📍 ' + pharmacy.address + ' | 📞 ' + pharmacy.phone + '</small><br>';
                    html += '<small style="color: #2563eb;">💊 الأدوية المتوفرة: ' + matchingMedicines.join(', ') + '</small>';
                    html += '</div>';
                });
                
                html += '</div>';
                searchResults.innerHTML = html;
            } else {
                searchResults.innerHTML = '<div class="search-results"><div class="no-results">لم يتم العثور على نتائج للبحث "' + query + '"</div></div>';
            }
        });
        
        // تفاعل النقاط على الخريطة
        document.querySelectorAll('.pharmacy-dot').forEach(dot => {
            dot.addEventListener('click', function() {
                const title = this.getAttribute('title');
                alert('🏥 ' + title + '\n\nاضغط على الهاتف للاتصال أو تصفح القائمة أدناه للمزيد من المعلومات.');
            });
        });
        
        console.log('✅ تطبيق صيدليات العراق جاهز للاستخدام!');
    </script>
</body>
</html>
