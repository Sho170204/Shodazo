<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Mobile Info Checker</title>
  <style>
    /* General Styles */
    body {
      font-family: 'Arial', sans-serif;
      margin: 0;
      padding: 0;
      background: linear-gradient(to bottom, #8ec5fc, #e0c3fc);
      display: flex;
      justify-content: center;
      align-items: center;
      min-height: 100vh;
      color: #333;
    }

    /* Card Container */
    .container {
      background: white;
      border-radius: 10px;
      box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);
      padding: 20px;
      text-align: center;
      max-width: 400px;
      width: 90%;
    }

    /* Header */
    h1 {
      font-size: 24px;
      color: #4a90e2;
      margin-bottom: 20px;
    }

    /* Device Info Section */
    .info {
      font-size: 18px;
      margin: 10px 0;
      padding: 10px;
      background: #f7f7f7;
      border-radius: 8px;
      box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
    }

    .info span {
      font-weight: bold;
      color: #555;
    }

    /* Footer */
    .footer {
      margin-top: 20px;
      font-size: 14px;
      color: #888;
    }

    .footer a {
      color: #4a90e2;
      text-decoration: none;
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>📱 Mobile Info Checker</h1>
    <div class="info">📲 <span>Device Name:</span> <span id="device-name">Loading...</span></div>
    <div class="info">🤖 <span>Android Version:</span> <span id="android-version">Loading...</span></div>
    <div class="info">💻 <span>SoC:</span> <span id="soc">Loading...</span></div>
    <div class="info">📦 <span>Storage Capacity:</span> <span id="storage">Loading...</span></div>
    <div class="footer">
      Made with 💙 by <a href="#">Your Name</a>
    </div>
  </div>

  <script>
    // Function to fetch device information
    function getDeviceInfo() {
      // Detect Device Name using User-Agent
      const userAgent = navigator.userAgent || "Unknown Device";
      const deviceName = userAgent;

      // Detect Android Version using Regex
      const androidVersionMatch = /Android (\d+\.\d+)/.exec(userAgent);
      const androidVersion = androidVersionMatch ? androidVersionMatch[1] : "Not an Android device";

      // Detect SoC (Browser cannot fetch hardware-specific details)
      const soc = "Unavailable (Browser cannot access hardware)";

      // Detect Approximate Storage Capacity (via Navigator API)
      const storageEstimate = navigator.storage && navigator.storage.estimate
        ? navigator.storage.estimate()
        : Promise.resolve({ quota: null });

      // Update HTML content
      document.getElementById("device-name").textContent = deviceName;
      document.getElementById("android-version").textContent = androidVersion;
      document.getElementById("soc").textContent = soc;

      // Fetch and display storage details
      storageEstimate.then((storage) => {
        const quota = storage.quota ? (storage.quota / (1024 * 1024 * 1024)).toFixed(2) : "Unknown";
        document.getElementById("storage").textContent = quota + " GB";
      });
    }

    // Execute the function on page load
    getDeviceInfo();
  </script>
</body>
</html>
