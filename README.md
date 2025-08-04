
<html>
<head>
  <meta charset="UTF-8">
  <title>نموذج المناوبة</title>
  <style>
    body { font-family: Arial; direction: rtl; padding: 20px; }
    input, select, textarea { width: 100%; margin-bottom: 10px; padding: 8px; }
    label { font-weight: bold; }
    button { padding: 10px 20px; font-size: 16px; }
  </style>
</head>
<body>

  <h2>نموذج تقرير المناوبة</h2>

  <label>التاريخ:</label>
  <input type="text" id="date" readonly>

  <label>الفترة:</label>
  <select id="shift">
    <option value="صباحية">صباحية</option>
    <option value="مسائية">مسائية</option>
  </select>

  <label>عدد الفرق الأساسية:</label>
  <input type="number" id="mainTeams">

  <label>عدد فرق الأوفر لاب:</label>
  <input type="number" id="overlapTeams">

  <label>عدد الفرق غير المتوفرة:</label>
  <input type="number" id="unavailableTeams">

  <label>سبب عدم توفر الفرق:</label>
  <textarea id="unavailableReason"></textarea>

  <label>بلاغات التدخل:</label>
  <div id="interventions">
    <input type="text" class="intervention" placeholder="اكتب بلاغ تدخل">
  </div>
  <button onclick="addIntervention()">➕ إضافة بلاغ</button><br><br>

  <label>عدد المركبات العاملة:</label>
  <input type="number" id="activeVehicles">

  <label>عدد مركبات الاحتياط:</label>
  <input type="number" id="reserveVehicles">

  <label>عدد المركبات المتعطلة:</label>
  <input type="number" id="brokenVehicles">

  <label>ملاحظات المركبات المتعطلة وموقعها:</label>
  <textarea id="brokenNotes"></textarea>

  <label>ملاحظات عامة:</label>
  <textarea id="generalNotes"></textarea>

  <label>اسم المناوب الأول:</label>
  <input type="text" id="staff1">

  <label>اسم المناوب الثاني:</label>
  <input type="text" id="staff2">

  <br>
  <button onclick="sendWhatsApp()">📤 إرسال عبر واتساب</button>

  <script>
    // تعبئة التاريخ تلقائيًا
    document.getElementById("date").value = new Date().toLocaleDateString('ar-EG');

    function addIntervention() {
      var div = document.createElement("div");
      div.innerHTML = '<input type="text" class="intervention" placeholder="اكتب بلاغ تدخل">';
      document.getElementById("interventions").appendChild(div);
    }

    function sendWhatsApp() {
      let text = "📋 تقرير المناوبة:\n";
      text += "📅 التاريخ: " + document.getElementById("date").value + "\n";
      text += "🕒 الفترة: " + document.getElementById("shift").value + "\n";
      text += "✅ عدد الفرق الأساسية: " + document.getElementById("mainTeams").value + "\n";
      text += "🔄 عدد فرق الأوفر لاب: " + document.getElementById("overlapTeams").value + "\n";
      text += "❌ عدد الفرق غير المتوفرة: " + document.getElementById("unavailableTeams").value + "\n";
      text += "📝 سبب عدم التوفر: " + document.getElementById("unavailableReason").value + "\n";

      let interventions = document.querySelectorAll(".intervention");
      text += "🚨 بلاغات التدخل:\n";
      interventions.forEach((input, index) => {
        if (input.value.trim() !== "")
          text += (index + 1) + "- " + input.value + "\n";
      });

      text += "🚗 عدد المركبات العاملة: " + document.getElementById("activeVehicles").value + "\n";
      text += "🅿️ عدد مركبات الاحتياط: " + document.getElementById("reserveVehicles").value + "\n";
      text += "🛠️ عدد المركبات المتعطلة: " + document.getElementById("brokenVehicles").value + "\n";
      text += "📍 ملاحظات وتعطلات المركبات: " + document.getElementById("brokenNotes").value + "\n";
      text += "🗒️ ملاحظات عامة: " + document.getElementById("generalNotes").value + "\n";
      text += "👥 أسماء المناوبين:\n";
      text += "1- " + document.getElementById("staff1").value + "\n";
      text += "2- " + document.getElementById("staff2").value + "\n";

      var url = "https://wa.me/?text=" + encodeURIComponent(text);
      window.open(url, '_blank');
    }
  </script>

</body>
</html>
