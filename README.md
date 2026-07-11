# 🏦 Banking Information System

A web-based **Banking Information System** built with **Python (Flask)** and **SQLite**, developed as a B.Tech academic project. It allows users to register, log in, and manage a personal bank account — including deposits, withdrawals, and transaction history — through a clean browser-based interface.

---

## 📌 Features

- **User Registration & Login** — secure authentication with hashed passwords (Werkzeug)
- **Auto-generated Bank Account** — every new user gets a unique 10-digit account number
- **Deposit Funds** — add money to your account
- **Withdraw Funds** — withdraw money with balance validation (no overdraw allowed)
- **Transaction History** — view all past deposits/withdrawals with timestamps
- **Dashboard** — quick overview of balance and recent activity
- **Session-based Auth** — powered by Flask-Login, routes are protected for logged-in users only
- **Flash Messages** — instant feedback for success/error actions

---

## 🛠️ Tech Stack

| Layer          | Technology                          |
|----------------|--------------------------------------|
| Backend        | Python 3, Flask                     |
| Database       | SQLite (via Flask-SQLAlchemy ORM)   |
| Authentication | Flask-Login, Werkzeug password hashing |
| Frontend       | HTML5, CSS3, Vanilla JavaScript, Jinja2 templates |

---

## 📂 Project Structure

```
banking-information-system/
├── app.py                  # Main Flask application (routes/views)
├── config.py                # App configuration (secret key, DB URI)
├── models.py                 # Database models: User, Account, Transaction
├── requirements.txt          # Python dependencies
├── .env.example               # Example environment variables
├── README.md
├── .github/workflows/ci.yml   # GitHub Actions CI (basic build check)
├── instance/                  # SQLite database is generated here (git-ignored)
├── static/
│   ├── css/style.css          # Stylesheet
│   └── js/script.js           # Client-side scripts
└── templates/
    ├── base.html               # Shared layout (navbar, flash messages)
    ├── login.html
    ├── register.html
    ├── dashboard.html
    ├── deposit.html
    ├── withdraw.html
    └── transactions.html
```

---

## 🗄️ Database Schema

**users**
| Column         | Type     | Notes                    |
|----------------|----------|---------------------------|
| id             | Integer  | Primary Key                |
| full_name      | String   |                             |
| email          | String   | Unique                     |
| password_hash  | String   | Hashed, never stored in plain text |
| created_at     | DateTime |                             |

**accounts**
| Column          | Type    | Notes                          |
|-----------------|---------|----------------------------------|
| id              | Integer | Primary Key                      |
| account_number  | String  | Unique, auto-generated (10 digits) |
| user_id         | Integer | Foreign Key → users.id           |
| balance         | Float   | Default 0.0                      |
| created_at      | DateTime|                                    |

**transactions**
| Column        | Type     | Notes                         |
|---------------|----------|---------------------------------|
| id            | Integer  | Primary Key                     |
| account_id    | Integer  | Foreign Key → accounts.id       |
| type          | String   | `deposit` or `withdraw`         |
| amount        | Float    |                                  |
| balance_after | Float    | Snapshot of balance post-transaction |
| timestamp     | DateTime |                                  |

---

## 🚀 Getting Started (Run Locally)

### 1. Prerequisites

- Python **3.9+** installed ([download here](https://www.python.org/downloads/))
- `pip` (comes bundled with Python)
- (Optional) `git` if cloning from GitHub

Check your Python version:
```bash
python --version
```

### 2. Clone or Download the Project

If using Git:
```bash
git clone https://github.com/<your-username>/banking-information-system.git
cd banking-information-system
```

Or simply extract the provided ZIP file and `cd` into the folder.

### 3. Create a Virtual Environment (recommended)

**Windows:**
```bash
python -m venv venv
venv\Scripts\activate
```

**macOS / Linux:**
```bash
python3 -m venv venv
source venv/bin/activate
```

You should see `(venv)` appear in your terminal prompt once activated.

### 4. Install Dependencies

```bash
pip install -r requirements.txt
```

### 5. (Optional) Configure Environment Variables

Copy the example env file and customize it:
```bash
cp .env.example .env
```
Then edit `.env` and set your own `SECRET_KEY`. This step is optional for local testing — the app has a default development key — but recommended before deploying anywhere public.

### 6. Run the Application

```bash
python app.py
```

You should see output similar to:
```
 * Running on http://127.0.0.1:5000
 * Debug mode: on
```

The database tables and the `instance/banking.db` SQLite file are created **automatically** the first time you run the app — no manual database setup needed.



## Running Tests / Verifying the Setup

A quick sanity check using Flask's built-in test client (no browser needed):

```bash
python -c "
from app import app, create_tables
create_tables()
client = app.test_client()
r = client.get('/login')
print('App is working!' if r.status_code == 200 else 'Something went wrong.')
"
```

--

## Possible Future Enhancements

These are good next steps if you want to extend this for a final-year project or add complexity:

- Fund transfers between two users' accounts
- Multiple account types (Savings / Current) with interest calculation
- Admin panel for managing all users and accounts
- Email/OTP-based two-factor authentication
- Downloadable PDF account statements
- REST API endpoints (for a mobile app front-end)
- Deployment guide (Render / Railway / PythonAnywhere)

---

## ⚠️ Disclaimer

This project is built for **academic/educational purposes only** and is **not** intended for real financial transactions or production banking use. It does not implement bank-grade security, encryption standards, or regulatory compliance required for real-world financial systems.


## 🙋 Author

Built by A.S.NAFEESA HAJIRA as a B.Tech academic projecT as it is part of my internship.

