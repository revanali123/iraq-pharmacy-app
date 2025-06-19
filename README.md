<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>صيدليات العراق</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 20px;
            background: linear-gradient(135deg, #4CAF50, #2196F3);
            min-height: 100vh;
        }
        
        .container {
            max-width: 800px;
            margin: 0 auto;
            background: white;
            border-radius: 20px;
            padding: 30px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.2);
        }
        
        .header {
            text-align: center;
            margin-bottom: 40px;
        }
        
        .header h1 {
            color: #2E7D32;
            font-size: 2.5em;
            margin-bottom: 10px;
        }
        
        .header p {
            color: #666;
            font-size: 1.2em;
        }
        
        .search-box {
            background: #f5f5f5;
            padding: 20px;
            border-radius: 15px;
            margin-bottom: 30px;
        }
        
        .search-input {
            width: 100%;
            padding: 15px;
            font-size: 18px;
            border: 2px solid #ddd;
            border-radius: 10px;
            box-sizing: border-box;
        }
        
        .search-input:focus {
            border-color: #4CAF50;
            outline: none;
        }
        
        .map-section {
            background: linear-gradient(45deg, #E8F5E8, #E3F2FD);
            padding: 30px;
            border-radius: 20px;
            margin-bottom: 30px;
            text-align: center;
        }
        
        .map-title {
            font-size: 1.5em;
            color: #2E7D32;
            margin-bottom: 20px;
            font-weight: bold;
        }
        
        .iraq-map {
            width: 300px;
            height: 200px;
            background: #4CAF50;
            margin: 20px auto;
            border-radius: 15px;
            position: relative;
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-size: 1.2em;
            font-weight: bold;
        }
        
        .pharmacy-dot {
            position: absolute;
            width: 20px;
            height: 20px;
            background: #ff4444;
            border: 3px solid white;
            border-radius: 50%;
            cursor: pointer;
        }
        
        .pharmacy-dot.open {
            background: #4CAF50;
        }
        
        .dot1 { top: 30%; left: 40%; }
        .dot2 { top: 50%; left: 60%; }
        .dot3 { bottom: 20%; right: 30%; }
        
        .legend {
            display: flex;
            justify-content: center;
            gap: 30px;
            margin-top: 20px;
        }
        
        .legend-item {
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .legend-dot {
            width: 15px;
            height: 15px;
            border-radius: 50%;
            border: 2px solid white;
        }
        
        .legend-dot.green { background: #4CAF50; }
        .legend-dot.red { background: #ff4444; }
        
        .pharmacies-grid {
            display: grid;
            gap: 20px;
        }
        
        .pharmacy-card {
            background: white;
            border: 2px solid #e0e0e0;
            border-radius: 15px;
            padding: 25px;
            transition: all 0.3s;
        }
        
        .pharmacy-card:hover {
            border-color: #4CAF50;
            transform: translateY(-5px);
            box-shadow: 0 10px 25px rgba(0,0,0,0.1);
        }
        
        .pharmacy-card.open {
            border-left: 5px solid #4CAF50;
        }
        
        .pharmacy-card.closed {
            border-left: 5px solid #ff4444;
            opacity: 0.8;
        }
        
        .pharmacy-name {
            font-size: 1.4em;
            font-weight: bold;
            color: #2E7D32;
            margin-bottom: 10px;
        }
        
        .pharmacy-address {
            color: #666;
            margin-bottom: 15px;
            font-size: 1.1em;
        }
        
        .pharmacy-details {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 15px;
            margin-bottom: 15px;
        }
        
        .detail-item {
            display: flex;
            align-items: center;
            gap: 8px;
            font-size: 1em;
        }
        
        .status {
            padding: 8px 15px;
            border-radius: 20px;
            font-size: 0.9em;
            font-weight: bold;
            text-align: center;
        }
        
        .status.open {
            background: #E8F5E8;
            color: #2E7D32;
        }
        
        .status.closed {
            background: #FFEBEE;
            color: #C62828;
        }
        
        .medicines {
            margin-top: 15px;
        }
        
        .medicines h4 {
            color: #2E7D32;
            margin-bottom: 10px;
        }
        
        .medicine-tags {
            display: flex;
            flex-wrap: wrap;
            gap: 8px;
        }
        
        .medicine-tag {
            background: #E3F2FD;
            color: #1976D2;
            padding: 5px 12px;
            border-radius: 15px;
            font-size: 0.9em;
        }
        
        .phone-link {
            color: #2196F3;
            text-decoration: none;
            font-weight: bold;
        }
        
        .phone-link:hover {
            text-decoration: underline;
        }
        
        @media (max-width: 600px) {
            .container {
                padding: 20px;
                margin: 10px;
            }
            
            .pharmacy-details {
                grid-template-columns: 1fr;
            }
            
            .legend {
                flex-direction: column;
                align-items: center;
                gap: 15px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>⚕️ صيدليات العراق</h1>
            <p>اعثر على أقرب صيدلية ودواء بسهولة</p>
        </div>
        
        <div class="search-box">
            <h3 style="margin-bottom: 15px; color: #2E7D32;">🔍 البحث عن الأدوية</h3>
            <input type="text" 
                   class="search-input" 
                   placeholder="ابحث عن دواء... (مثال: بنادول، أسبرين)"
                   onkeyup="searchMedicines(this.value)">
            <div id="searchResults" style="margin-top: 15px;"></div>
        </div>
        
        <div class="map-section">
            <div class="map-title">🗺️ خريطة صيدليات العراق</div>
            <div class="iraq-map">
                العراق
                <div class="pharmacy-dot open dot1" onclick="showPharmacyInfo('صيدلية النور - بغداد')"></div>
                <div class="pharmacy-dot open dot2" onclick="showPharmacyInfo('صيدلية الشفاء - بغداد')"></div>
                <div class="pharmacy-dot closed dot3" onclick="showPharmacyInfo('صيدلية البصرة - مغلقة')"></div>
            </div>
            <div class="legend">
                <div class="legend-item">
                    <div class="legend-dot green"></div>
                    <span>مفتوحة الآن</span>
                </div>
                <div class="legend-item">
                    <div class="legend-dot red"></div>
                    <span>مغلقة</span>
                </div>
            </div>
        </div>
        
        <div class="pharmacies-grid">
            <div class="pharmacy-card open">
                <div class="pharmacy-name">صيدلية النور</div>
                <div class="pharmacy-address">📍 شارع الرشيد، بغداد، العراق</div>
                <div class="pharmacy-details">
                    <div class="detail-item">
                        <span>🕐</span>
                        <span>8:00 ص - 11:00 م</span>
                    </div>
                    <div class="detail-item">
                        <span>📞</span>
                        <a href="tel:+96412345678" class="phone-link">+964 1 234 5678</a>
                    </div>
                </div>
                <div class="status open">مفتوحة الآن</div>
                <div class="medicines">
                    <h4>💊 الأدوية المتوفرة:</h4>
                    <div class="medicine-tags">
                        <span class="medicine-tag">بنادول</span>
                        <span class="medicine-tag">أسبرين</span>
                        <span class="medicine-tag">أموكسيسيلين</span>
                        <span class="medicine-tag">فيتامين د</span>
                        <span class="medicine-tag">أوميجا 3</span>
                    </div>
                </div>
            </div>
            
            <div class="pharmacy-card open">
                <div class="pharmacy-name">صيدلية الشفاء</div>
                <div class="pharmacy-address">📍 حي الجادرية، بغداد، العراق</div>
                <div class="pharmacy-details">
                    <div class="detail-item">
                        <span>🕐</span>
                        <span>24/7 - مفتوحة دائماً</span>
                    </div>
                    <div class="detail-item">
                        <span>📞</span>
                        <a href="tel:+96413456789" class="phone-link">+964 1 345 6789</a>
                    </div>
                </div>
                <div class="status open">مفتوحة 24/7</div>
                <div class="medicines">
                    <h4>💊 الأدوية المتوفرة:</h4>
                    <div class="medicine-tags">
                        <span class="medicine-tag">إنسولين</span>
                        <span class="medicine-tag">أدوية الضغط</span>
                        <span class="medicine-tag">مضادات حيوية</span>
                        <span class="medicine-tag">فيتامين ب12</span>
                        <span class="medicine-tag">مسكنات</span>
                    </div>
                </div>
            </div>
            
            <div class="pharmacy-card closed">
                <div class="pharmacy-name">صيدلية البصرة الحديثة</div>
                <div class="pharmacy-address">📍 كورنيش البصرة، البصرة، العراق</div>
                <div class="pharmacy-details">
                    <div class="detail-item">
                        <span>🕐</span>
                        <span>9:00 ص - 10:00 م</span>
                    </div>
                    <div class="detail-item">
                        <span>📞</span>
                        <a href="tel:+96440123456" class="phone-link">+964 40 123 456</a>
                    </div>
                </div>
                <div class="status closed">مغلقة الآن</div>
                <div class="medicines">
                    <h4>💊 الأدوية المتوفرة:</h4>
                    <div class="medicine-tags">
                        <span class="medicine-tag">أدوية القلب</span>
                        <span class="medicine-tag">أدوية الأطفال</span>
                        <span class="medicine-tag">فيتامينات</span>
                        <span class="medicine-tag">مكملات غذائية</span>
                    </div>
                </div>
            </div>
            
            <div class="pharmacy-card open">
                <div class="pharmacy-name">صيدلية أربيل المركزية</div>
                <div class="pharmacy-address">📍 شارع 60 متر، أربيل، العراق</div>
                <div class="pharmacy-details">
                    <div class="detail-item">
                        <span>🕐</span>
                        <span>8:30 ص - 11:30 م</span>
                    </div>
                    <div class="detail-item">
                        <span>📞</span>
                        <a href="tel:+96466789012" class="phone-link">+964 66 789 012</a>
                    </div>
                </div>
                <div class="status open">مفتوحة الآن</div>
                <div class="medicines">
                    <h4>💊 الأدوية المتوفرة:</h4>
                    <div class="medicine-tags">
                        <span class="medicine-tag">أدوية السكري</span>
                        <span class="medicine-tag">مضادات الالتهاب</span>
                        <span class="medicine-tag">فيتامينات متنوعة</span>
                        <span class="medicine-tag">أدوية الضغط</span>
                    </div>
                </div>
            </div>
            
            <div class="pharmacy-card open">
                <div class="pharmacy-name">صيدلية الموصل الطبية</div>
                <div class="pharmacy-address">📍 ساحة الساعة، الموصل، العراق</div>
                <div class="pharmacy-details">
                    <div class="detail-item">
                        <span>🕐</span>
                        <span>7:00 ص - 12:00 ص</span>
                    </div>
                    <div class="detail-item">
                        <span>📞</span>
                        <a href="tel:+96460456789" class="phone-link">+964 60 456 789</a>
                    </div>
                </div>
                <div class="status open">مفتوحة الآن</div>
                <div class="medicines">
                    <h4>💊 الأدوية المتوفرة:</h4>
                    <div class="medicine-tags">
                        <span class="medicine-tag">مسكنات قوية</span>
                        <span class="medicine-tag">أدوية عصبية</span>
                        <span class="medicine-tag">مضادات حيوية</span>
                        <span class="medicine-tag">أسبرين</span>
                    </div>
                </div>
            </div>
        </div>
        
        <div style="text-align: center; margin-top: 40px; padding: 20px; background: #f5f5f5; border-radius: 15px;">
            <h3 style="color: #2E7D32;">📞 للطوارئ</h3>
            <p>في حالة الطوارئ الطبية، اتصل بالرقم: <strong style="color: #C62828;">115</strong></p>
            <p style="margin-top: 15px; color: #666; font-size: 0.9em;">
                © 2025 تطبيق صيدليات العراق - خدمة مجانية لمساعدة المواطنين
            </p>
        </div>
    </div>

    <script>
        function showPharmacyInfo(name) {
            alert("🏥 " + name + "\n\nللمزيد من المعلومات، تصفح القائمة أدناه أو اتصل بالصيدلية مباشرة.");
        }
        
        function searchMedicines(query) {
            const resultsDiv = document.getElementById('searchResults');
            
            if (!query || query.trim() === '') {
                resultsDiv.innerHTML = '';
                return;
            }
            
            query = query.toLowerCase().trim();
            
            const pharmacies = [
                {
                    name: 'صيدلية النور',
                    address: 'شارع الرشيد، بغداد',
                    phone: '+964 1 234 5678',
                    medicines: ['بنادول', 'أسبرين', 'أموكسيسيلين', 'فيتامين د', 'أوميجا 3'],
                    status: 'مفتوحة'
                },
                {
                    name: 'صيدلية الشفاء',
                    address: 'حي الجادرية، بغداد',
                    phone: '+964 1 345 6789',
                    medicines: ['إنسولين', 'أدوية الضغط', 'مضادات حيوية', 'فيتامين ب12', 'مسكنات'],
                    status: 'مفتوحة 24/7'
                },
                {
                    name: 'صيدلية أربيل المركزية',
                    address: 'شارع 60 متر، أربيل',
                    phone: '+964 66 789 012',
                    medicines: ['أدوية السكري', 'مضادات الالتهاب', 'فيتامينات متنوعة', 'أدوية الضغط'],
                    status: 'مفتوحة'
                },
                {
                    name: 'صيدلية الموصل الطبية',
                    address: 'ساحة الساعة، الموصل',
                    phone: '+964 60 456 789',
                    medicines: ['مسكنات قوية', 'أدوية عصبية', 'مضادات حيوية', 'أسبرين'],
                    status: 'مفتوحة'
                }
            ];
            
            const results = [];
            
            for (let pharmacy of pharmacies) {
                for (let medicine of pharmacy.medicines) {
                    if (medicine.toLowerCase().includes(query)) {
                        results.push({
                            pharmacy: pharmacy,
                            medicine: medicine
                        });
                        break;
                    }
                }
            }
            
            if (results.length > 0) {
                let html = '<div style="background: #E8F5E8; padding: 15px; border-radius: 10px; border: 2px solid #4CAF50;">';
                html += '<h4 style="color: #2E7D32; margin-bottom: 10px;">🎯 نتائج البحث عن "' + query + '":</h4>';
                
                for (let result of results) {
                    html += '<div style="background: white; padding: 10px; margin-bottom: 10px; border-radius: 8px; border-left: 3px solid #4CAF50;">';
                    html += '<strong style="color: #2E7D32;">' + result.pharmacy.name + '</strong><br>';
                    html += '<small style="color: #666;">📍 ' + result.pharmacy.address + '</small><br>';
                    html += '<small style="color: #666;">📞 ' + result.pharmacy.phone + '</small><br>';
                    html += '<small style="color: #2196F3;">✅ ' + result.pharmacy.status + '</small>';
                    html += '</div>';
                }
                
                html += '</div>';
                resultsDiv.innerHTML = html;
            } else {
                resultsDiv.innerHTML = '<div style="background: #FFEBEE; padding: 15px; border-radius: 10px; border: 2px solid #ff4444; text-align: center; color: #C62828;">❌ لم يتم العثور على الدواء "' + query + '" في الصيدليات المتاحة</div>';
            }
        }
        
        console.log("✅ تطبيق صيدليات العراق جاهز!");
    </script>
</body>
</html>
