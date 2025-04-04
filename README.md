
<!DOCTYPE html>
<html lang="hi">
<head>
  <meta charset="UTF-8">
  <title>गुमनाम SMS भेजें</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    body {
      font-family: 'Segoe UI', sans-serif;
      background-color: #f7f7f7;
      padding: 20px;
    }
    .container {
      max-width: 400px;
      margin: auto;
      background: white;
      padding: 20px;
      border-radius: 12px;
      box-shadow: 0 2px 12px rgba(0,0,0,0.1);
    }
    h2 {
      text-align: center;
      color: #333;
    }
    input, textarea, button {
      width: 100%;
      margin: 10px 0;
      padding: 10px;
      font-size: 16px;
      border: 1px solid #ccc;
      border-radius: 6px;
    }
    button {
      background-color: #007bff;
      color: white;
      border: none;
      cursor: pointer;
    }
    button:hover {
      background-color: #0056b3;
    }
    #status {
      text-align: center;
      margin-top: 10px;
      font-weight: bold;
    }
  </style>
</head>
<body>
  <div class="container">
    <h2>गुमनाम SMS भेजें</h2>
    <input type="text" id="number" placeholder="मोबाइल नंबर">
    <textarea id="message" rows="4" placeholder="संदेश लिखें..."></textarea>
    <button onclick="sendSMS()">भेजें</button>
    <p id="status"></p>
  </div>

  <script>
    function sendSMS() {
      const number = document.getElementById('number').value.trim();
      const message = document.getElementById('message').value.trim();
      const status = document.getElementById('status');
      if (!number || !message) {
        status.innerText = "कृपया नंबर और संदेश भरें।";
        return;
      }
      fetch('https://www.fast2sms.com/dev/bulkV2', {
        method: 'POST',
        headers: {
          'authorization': 'jU0XuV9lkqLdDGsxWyPJ6Ai74gEY5z2KNehvZC1bOIo3rQfa8nWox1CBpquEcnkiyfgv5bNOLDwRjaQI',
          'Content-Type': 'application/json'
        },
        body: JSON.stringify({
          route: 'q',
          message: message,
          language: 'unicode',
          flash: 0,
          numbers: number
        })
      })
      .then(res => res.json())
      .then(data => {
        if (data.return) {
          status.innerText = "✅ SMS सफलतापूर्वक भेजा गया!";
        } else {
          status.innerText = "❌ SMS भेजने में त्रुटि हुई।";
        }
        console.log(data);
      })
      .catch(err => {
        status.innerText = "⚠️ नेटवर्क या API त्रुटि।";
        console.error(err);
      });
    }
  </script>
</body>
</html>
