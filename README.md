<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>TikTok Issue Report</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <style>
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      font-family: system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
    }

    body {
      min-height: 100vh;
      background: #0f0f10;
      color: #fff;
      display: flex;
      align-items: center;
      justify-content: center;
      padding: 20px;
    }

    .container {
      display: flex;
      max-width: 900px;
      width: 100%;
      background: #18181b;
      border-radius: 18px;
      box-shadow: 0 18px 40px rgba(0, 0, 0, 0.6);
      overflow: hidden;
    }

    .sidebar {
      background: radial-gradient(circle at top left, #ff0050, #000);
      padding: 30px 20px;
      display: flex;
      align-items: center;
      justify-content: center;
      min-width: 180px;
    }

    .sidebar img {
      max-width: 120px;
      width: 100%;
      height: auto;
      display: block;
    }

    .content {
      padding: 30px 28px 26px;
      flex: 1;
    }

    .title {
      font-size: 1.6rem;
      font-weight: 700;
      margin-bottom: 8px;
    }

    .subtitle {
      font-size: 0.9rem;
      color: #a1a1aa;
      line-height: 1.4;
      margin-bottom: 20px;
    }

    .form-group {
      margin-bottom: 16px;
    }

    .form-group label {
      display: block;
      font-size: 0.9rem;
      margin-bottom: 6px;
    }

    select,
    input,
    textarea {
      width: 100%;
      border-radius: 10px;
      border: 1px solid #27272a;
      background: #09090b;
      color: #f4f4f5;
      padding: 10px 12px;
      font-size: 0.9rem;
      outline: none;
      transition: border 0.15s ease, box-shadow 0.15s ease, background 0.15s ease;
    }

    select:focus,
    input:focus,
    textarea:focus {
      border-color: #ff0050;
      box-shadow: 0 0 0 1px #ff0050;
      background: #020617;
    }

    textarea {
      min-height: 100px;
      resize: vertical;
    }

    .button-row {
      display: flex;
      justify-content: flex-end;
      margin-top: 10px;
    }

    button {
      border: none;
      border-radius: 999px;
      padding: 10px 20px;
      font-size: 0.9rem;
      font-weight: 600;
      cursor: pointer;
      background: linear-gradient(135deg, #ff0050, #ff2e93);
      color: #fff;
      box-shadow: 0 10px 25px rgba(255, 0, 80, 0.4);
      transition: transform 0.1s ease, box-shadow 0.1s ease, opacity 0.1s ease;
    }

    .status {
      margin-top: 10px;
      font-size: 0.85rem;
    }

    .status.success {
      color: #4ade80;
    }

    .status.error {
      color: #f97373;
    }
  </style>
</head>
<body>
  <div class="container">
    <aside class="sidebar">
      <img
        src="https://media.discordapp.net/attachments/1478880251714080961/1480344311491989537/Screenshot_2026-03-07_203727-removebg-preview.png"
        alt="TikTok style icon"
      />
    </aside>

    <main class="content">
      <h1 class="title">Report an issue</h1>
      <p class="subtitle">
        Share a problem you’d like to report or feedback about your TikTok experience.
        The information you provide will only be used to address your report.
      </p>

      <form id="reportForm">
        <div class="form-group">
          <label for="issueType">Issue type</label>
          <select id="issueType" required>
            <option value="" disabled selected>Select an option</option>
            <option value="Report an underage user">Report an underage user</option>
            <option value="Issue with application">Issue with application</option>
            <option value="Issue with roblox Game">Issue with roblox Game</option>
            <option value="Issue with Discord accessibility">Issue with Discord accessibility</option>
          </select>
        </div>

        <div class="form-group">
          <label id="descriptionLabel">How can we help you?</label>
          <textarea id="description" required></textarea>
        </div>

        <div class="form-group">
          <label>Discord username</label>
          <input id="discordUsername" required />
        </div>

        <div class="form-group">
          <label>Discord ID</label>
          <input id="discordId" required />
        </div>

        <div class="button-row">
          <button type="submit">Submit report</button>
        </div>

        <div id="statusMessage" class="status"></div>
      </form>
    </main>
  </div>

  <script>
    const WEBHOOK_URL =
      "https://discord.com/api/webhooks/1480715076817125396/GRB2w2qmU8OBUyCt2id79w3l7EKzv21pBT_arz3ZK3f6xwuPlgZHQZS-B4C3R5Ei1vUl";

    const form = document.getElementById("reportForm");
    const issueTypeSelect = document.getElementById("issueType");
    const descriptionLabel = document.getElementById("descriptionLabel");
    const statusMessage = document.getElementById("statusMessage");

    issueTypeSelect.addEventListener("change", () => {
      descriptionLabel.textContent =
        "How can we help you with " + issueTypeSelect.value + "?";
    });

    form.addEventListener("submit", async (e) => {
      e.preventDefault();

      const issueType = issueTypeSelect.value;
      const description = document.getElementById("description").value.trim();
      const discordUsername = document.getElementById("discordUsername").value.trim();
      const discordId = document.getElementById("discordId").value.trim();

      const payload = {
        content: "<@&1479931827195219998>",
        embeds: [
          {
            title: "📢 New Issue Report Submitted",
            color: 16711680,
            fields: [
              { name: "Issue Type", value: issueType, inline: false },
              { name: "Description", value: description, inline: false },
              { name: "Discord Username", value: discordUsername, inline: true },
              { name: "Discord ID", value: discordId, inline: true }
            ],
            timestamp: new Date().toISOString()
          }
        ]
      };

      try {
        const res = await fetch(WEBHOOK_URL, {
          method: "POST",
          headers: { "Content-Type": "application/json" },
          body: JSON.stringify(payload)
        });

        if (!res.ok) throw new Error("Webhook error");

        statusMessage.textContent = "Your report has been submitted successfully.";
        statusMessage.className = "status success";
        form.reset();
        descriptionLabel.textContent = "How can we help you?";
      } catch (err) {
        statusMessage.textContent = "Failed to send report. Try again later.";
        statusMessage.className = "status error";
      }
    });
  </script>
</body>
</html>
