# Smart Blood Donation System

A web-based platform for intelligent blood donor-recipient matching and real-time hospital blood inventory management, built for Odisha, India.

## Features

- **AI-powered donor-recipient matching** based on blood type compatibility, distance, urgency, and donor reliability.
- **Real-time hospital blood inventory** dashboard with live updates via WebSockets.
- **Appointment scheduling** for blood donations.
- **Secure phone number reveal** for donor privacy.
- **SMS notifications** (Twilio integration, trial mode by default).
- **Admin authentication** for hospital inventory updates (JWT-based).

## Project Structure

```
.
├── app.py                   # Main Flask app
├── matching.py              # AI matching logic
├── donors.csv               # Donor data
├── recipients.csv           # Recipient data
├── hospitals.csv            # Hospital inventory data
├── appointments.csv         # Scheduled appointments
├── train_model.py           # Model training script
├── generate_training_data.py# Synthetic data generator
├── generate_key.py          # JWT secret generator
├── hospital_client.py       # Example hospital API client
├── index.html               # Main web UI
├── hospital_inventory.html  # Hospital inventory dashboard
├── requirements.txt         # Python dependencies
├── .env                     # Environment variables (Twilio, JWT secret)
└── README.md                # Project documentation
```

## Setup

1. **Clone the repository** and install dependencies:
    ```sh
    pip install -r requirements.txt
    ```

2. **Configure environment variables** in `.env`:
    ```
    TWILIO_SID=your_twilio_sid
    TWILIO_AUTH_TOKEN=your_twilio_auth_token
    TWILIO_PHONE=your_twilio_phone
    JWT_SECRET=your_jwt_secret
    ```

3. **Generate synthetic data** (optional, will overwrite CSVs):
    ```sh
    python generate_training_data.py
    ```

4. **Train the AI model**:
    ```sh
    python train_model.py
    ```

5. **Run the Flask app**:
    ```sh
    python app.py
    ```
    Or with Gunicorn (for production):
    ```sh
    gunicorn app:app
    ```

6. **Access the web UI**:
    - Main page: [http://127.0.0.1:5000/](http://127.0.0.1:5000/)
    - Hospital inventory: [http://127.0.0.1:5000/hospital_inventory](http://127.0.0.1:5000/hospital_inventory)

## Usage

- **Find donors:** Enter recipient details on the main page and view AI-ranked donor matches on the map.
- **Contact donors:** Reveal donor phone numbers securely (valid for 5 minutes).
- **Schedule appointments:** Book donation slots and notify donors.
- **Hospital inventory:** View and update blood stock in real time (requires hospital login).

## API Endpoints

- `POST /match` — Find matching donors for a recipient.
- `POST /hospital/login` — Authenticate hospital and get JWT.
- `POST /hospital/update` — Update hospital inventory (JWT required).
- `GET /hospitals` — Get all hospital inventory data.
- `POST /reveal_phone` — Reveal donor phone number (token required).
- `POST /schedule_appointment` — Schedule a donation appointment.
- `POST /donation_history` — Get donor's donation history.

## Notes

- **Twilio SMS** is in trial/mock mode by default. To enable real SMS, set `TWILIO_TRIAL_MODE = False` in `app.py` and use verified numbers.
- **Hospital login**: Default credentials are `hospital1` / `password123` (see `REGISTERED_HOSPITALS` in `app.py`).

## License

MIT License

---

Built for Odisha's healthcare needs.
