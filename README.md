
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Report an Issue</title>
  <style>
    * {
      box-sizing: border-box;
    }

    body {
      margin: 0;
      font-family: Arial, Helvetica, sans-serif;
      background: linear-gradient(135deg, #0f0f10, #1b1d21);
      color: #ffffff;
      min-height: 100vh;
      display: flex;
      align-items: center;
      justify-content: center;
      padding: 24px;
    }

    .container {
      width: 100%;
      max-width: 760px;
      background: rgba(255, 255, 255, 0.06);
      border: 1px solid rgba(255, 255, 255, 0.12);
      border-radius: 20px;
      backdrop-filter: blur(10px);
      box-shadow: 0 20px 60px rgba(0, 0, 0, 0.35);
      overflow: hidden;
    }

    .header {
      display: flex;
      align-items: center;
      gap: 16px;
      padding: 28px 28px 18px;
      border-bottom: 1px solid rgba(255, 255, 255, 0.08);
    }

    .header img {
      width: 64px;
      height: 64px;
      object-fit: contain;
      flex-shrink: 0;
    }

    .header-content {
      flex: 1;
      text-align: center;
      margin-right: 64px;
    }

    .header-content h1 {
      margin: 0;
      font-size: 2rem;
      font-weight: 700;
      letter-spacing: 0.2px;
    }

    .header-content p {
      margin: 10px auto 0;
      max-width: 560px;
      font-size: 0.98rem;
      line-height: 1.6;
      color: #d6d9df;
    }

    .form-area {
      padding: 28px;
    }

    .field {
      margin-bottom: 20px;
    }

    label {
      display: block;
      font-size: 0.95rem;
      font-weight: 600;
      margin-bottom: 8px;
      color: #f3f4f6;
    }

    select,
    input,
    textarea {
      width: 100%;
      border: 1px solid rgba(255, 255, 255, 0.14);
      background: rgba(255, 255, 255, 0.06);
      color: #ffffff;
      border-radius: 12px;
      padding: 14px 15px;
      font-size: 0.96rem;
      outline: none;
      transition: border-color 0.2s ease, background 0.2s ease;
    }

    select:focus,
    input:focus,
    textarea:focus {
      border-color: #7c9cff;
      background: rgba(255, 255, 255, 0.08);
    }

    select option {
      color: #111;
    }

    textarea {
      resize: vertical;
      min-height: 130px;
    }

    .hidden {
      display: none;
    }

    .helper-title {
      margin: 6px 0 16px;
      font-size: 1rem;
      font-weight: 700;
      color: #9fc0ff;
    }

    .button-row {
      display: flex;
      justify-content: flex-end;
      margin-top: 26px;
    }

    button {
      border: none;
      background: linear-gradient(135deg, #5865f2, #7289da);
      color: white;
      font-size: 0.96rem;
      font-weight: 700;
      padding: 14px 22px;
      border-radius: 12px;
      cursor: pointer;
      transition: transform 0.15s ease, opacity 0.2s ease;
    }

    button:hover {
      transform: translateY(-1px);
      opacity: 0.95;
    }

    button:disabled {
      cursor: not-allowed;
      opacity: 0.6;
      transform: none;
    }

    .status {
      margin-top: 18px;
      padding: 12px 14px;
      border-radius: 12px;
      font-size: 0.94rem;
      line-height: 1.5;
      display: none;
    }

    .status.success {
      display: block;
      background: rgba(34, 197, 94, 0.14);
      border: 1px solid rgba(34, 197, 94, 0.35);
      color: #bbf7d0;
    }

    .status.error {
      display: block;
      background: rgba(239, 68, 68, 0.14);
      border: 1px solid rgba(239, 68, 68, 0.35);
      color: #fecaca;
    }

    @media (max-width: 640px) {
      .header {
        flex-direction: column;
        text-align: center;
      }

      .header-content {
        margin-right: 0;
      }

      .header img {
        width: 56px;
        height: 56px;
      }

      .header-content h1 {
        font-size: 1.7rem;
      }

      .button-row {
        justify-content: stretch;
      }

      button {
        width: 100%;
      }
    }
  </style>
</head>
<body>
  <div class="container">
    <div class="header">
      <img
        src="https://media.discordapp.net/attachments/1478880251714080961/1480344311491989537/Screenshot_2026-03-07_203727-removebg-preview.png?ex=69affe53&is=69aeacd3&hm=e04694d7992ee925218f86b1b9c6cf8cf92ae5c9131e9cb7aa30e8ab087ef3e5&=&format=webp&quality=lossless&width=470&height=360"
        alt="Site Icon"
      />
      <div class="header-content">
        <h1>Report an issue</h1>
        <p>
          Share a problem you’d like to report or feedback about your experience.
          The information you provide will only be used to address your report.
        </p>
      </div>
    </div>

    <div class="form-area">
      <form id="reportForm">
        <div class="field">
          <label for="issueType">Select an issue</label>
          <select id="issueType" name="issueType" required>
            <option value="">Choose an option</option>
            <option value="Report an underage user">Report an underage user</option>
            <option value="Issue with application">Issue with application</option>
            <option value="Issue with Roblox game">Issue with Roblox game</option>
            <option value="Issue with Discord accessibility">Issue with Discord accessibility</option>
          </select>
        </div>

        <div id="detailsSection" class="hidden">
          <div class="helper-title" id="dynamicPrompt">
            How can we help you with this issue?
          </div>

          <div class="field">
            <label for="description">Description</label>
            <textarea
              id="description"
              name="description"
              placeholder="Please describe the issue in as much detail as possible..."
              required
            ></textarea>
          </div>

          <div class="field">
            <label for="discordUsername">Discord username</label>
            <input
              type="text"
              id="discordUsername"
              name="discordUsername"
              placeholder="e.g. username#1234 or username"
              required
            />
          </div>

          <div class="field">
            <label for="discordId">Discord ID</label>
            <input
              type="text"
              id="discordId"
              name="discordId"
              placeholder="Enter Discord ID"
              required
            />
          </div>
        </div>

        <div class="button-row">
          <button type="submit" id="submitBtn">Submit report</button>
        </div>

        <div id="statusBox" class="status"></div>
      </form>
    </div>
  </div>

  <script>
    const issueType = document.getElementById("issueType");
    const detailsSection = document.getElementById("detailsSection");
    const dynamicPrompt = document.getElementById("dynamicPrompt");
    const reportForm = document.getElementById("reportForm");
    const statusBox = document.getElementById("statusBox");
    const submitBtn = document.getElementById("submitBtn");

    issueType.addEventListener("change", () => {
      const selected = issueType.value.trim();

      if (selected) {
        detailsSection.classList.remove("hidden");
        dynamicPrompt.textContent = `How can we help you with ${selected}?`;
      } else {
        detailsSection.classList.add("hidden");
        dynamicPrompt.textContent = "How can we help you with this issue?";
      }

      statusBox.className = "status";
      statusBox.textContent = "";
    });

    reportForm.addEventListener("submit", async (e) => {
      e.preventDefault();

      const selectedIssue = issueType.value.trim();
      const description = document.getElementById("description").value.trim();
      const discordUsername = document.getElementById("discordUsername").value.trim();
      const discordId = document.getElementById("discordId").value.trim();

      if (!selectedIssue) {
        showStatus("Please select an issue first.", "error");
        return;
      }

      if (!description || !discordUsername || !discordId) {
        showStatus("Please fill in all required fields.", "error");
        return;
      }

      submitBtn.disabled = true;
      showStatus("Submitting report...", "success");

      const payload = {
        issueType: selectedIssue,
        description,
        discordUsername,
        discordId,
        submittedAt: new Date().toISOString()
      };

      try {
        // Replace this with your own backend endpoint.
        // Example: /api/report
        const response = await fetch("/api/report", {
          method: "POST",
          headers: {
            "Content-Type": "application/json"
          },
          body: JSON.stringify(payload)
        });

        if (!response.ok) {
          throw new Error("Server returned an error.");
        }

        reportForm.reset();
        detailsSection.classList.add("hidden");
        dynamicPrompt.textContent = "How can we help you with this issue?";
        showStatus("Your report has been submitted successfully.", "success");
      } catch (error) {
        showStatus(
          "Unable to submit the report right now. Please try again after connecting this form to your backend.",
          "error"
        );
      } finally {
        submitBtn.disabled = false;
      }
    });

    function showStatus(message, type) {
      statusBox.textContent = message;
      statusBox.className = `status ${type}`;
    }
  </script>
</body>
</html>
