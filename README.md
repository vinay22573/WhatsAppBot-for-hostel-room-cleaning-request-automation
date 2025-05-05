## ✅ Project: WhatsApp-based Hostel Room Service Automation

---

### 📌 Problem Statement:

Students currently message a volunteer to request room cleaning (e.g., "H1,505 room cleaning"). The volunteer manually checks a sheet to identify which housekeeping staff is responsible and then forwards the message. This project aims to automate that manual lookup and message forwarding using a WhatsApp bot.

---

### 🎯 Goal:

When a student sends a WhatsApp message like "H1,505 room cleaning":

1. The bot parses the block and room number.
2. Looks up which housekeeper is assigned to that block/floor.
3. Sends the message directly to the housekeeper’s WhatsApp number.

---

### 💻 Fixed Tech Stack

#### 1. Frontend (User Interface)

* Platform/API: **Twilio WhatsApp Business API**

#### 2. Backend

* Language: **Python**
* Framework: **FastAPI**

#### 3. Database

* Type: **SQLite**
* ORM: **SQLModel**
* Data:

  * Room range mappings (e.g., H1-5XX → Ravi)
  * Housekeeper phone numbers
  * Optional: Message logs

#### 4. Message Routing

* Logic: Parse room number, find matching block/floor, fetch staff number, and send the message via Twilio API

#### 5. Deployment

* Platform: **Render.com**
* CI/CD: **GitHub + GitHub Actions**

---

### 📁 Folder Structure

```
hostel-bot/
├── app/
│   ├── main.py          # FastAPI app & webhook receiver
│   ├── models.py        # SQLModel definitions (RoomAssignment, Logs)
│   ├── db.py            # SQLite setup
│   ├── twilio_handler.py# Handles message send/receive via Twilio
│   └── parser.py        # Parses messages like 'H1,505 room cleaning'
├── .env                 # Twilio creds, config vars
├── README.md
└── requirements.txt
```

---

### 📊 Sample Room Assignment Table

| Block | Floor | Room Pattern | Housekeeper Name | Phone Number  |
| ----- | ----- | ------------ | ---------------- | ------------- |
| H1    | 5     | 5XX          | Ravi             | +91XXXXXXXXXX |
| H2    | 2     | 2XX          | Sonu             | +91YYYYYYYYYY |

Stored as `RoomAssignment` model in SQLite.

---

### 💬 Sample Flow

1. **Student Message:**

   ```
   H1,505 room cleaning
   ```

2. **Bot Actions:**

   * Parse block = H1, room = 505
   * Check database → H1, floor 5 → Assigned to *Ravi*
   * Forward message:

     ```
     Room 505 (H1) has requested cleaning.
     ```

     → Sent to Ravi's WhatsApp via Twilio

---

### ✅ Dependencies (requirements.txt)

```
fastapi
uvicorn
twilio
sqlmodel
python-dotenv
```

---

### 🔐 Security/Spam Protection (Optional Later)

* Allow requests only from registered numbers
* Log requests per user to prevent spamming

---

## 🚀 Future Phases

### 🔄 Phase 2: Additional Fixed Use Cases

* Handle other common facility messages like:

  * "H1,505 AC not working"
  * "H2,302 shower not working"
* Route these to the appropriate staff or forward them to the volunteer as fallback.

### 📈 Phase 3: Escalation & Auto-Identification

* Identify urgent tasks like "urgent room cleaning" or "AC emergency".
* Prioritize and escalate such messages automatically to a senior or main FMS coordinator.

### 🧠 Phase 4: Semantic Understanding (ML + NLP)

* Use NLP to interpret free-text student messages.
* Classify message intent and route accordingly.
* Redirect or auto-reply based on whether the use case is already automated or needs human intervention.
* Example tech: spaCy, scikit-learn or transformer models (e.g., BERT).

This phased approach will help evolve from static routing to a smart, intelligent WhatsApp-based FMS assistant.
