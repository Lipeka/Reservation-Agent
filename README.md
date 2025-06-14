
# 🍽️ GoodFoods Reservation Assistant

An AI-powered multi-venue reservation assistant that helps users book:
- 🏨 Hotel Rooms (Single/Double/Suite)
- 🍽️ Restaurant Tables (2/4/6 seaters)
- 🎉 Party Halls (20–500 people)

It uses NVIDIA’s LLaMA-3.1 8B Instruct model for natural conversation and Gradio for a chatbot-style UI.

---

## 🚀 Features

- 🔍 Conversational booking flow (room/table/hall)
- 🧠 Smart intent detection and dynamic field filling
- 🏙️ Venue filtering based on user preferences:
  - AC/Non-AC
  - Check-in time (12hr/24hr)
  - Price range
  - Food requirement and cuisine preference
- ✅ Final confirmation based on venue ID
- 🖥️ Built-in Gradio UI for demo and testing

---

## 🧱 Project Structure

```

📁 goodfoods-reservation/
├── app.py                      # Main Python script (CLI + Gradio UI)
├── synthetic\_room\_hotels.json # Synthetic dataset for hotel room venues
├── synthetic\_restaurant\_tables.json # Synthetic dataset for restaurant tables
├── synthetic\_banquet\_halls.json     # Synthetic dataset for party halls
└── README.md                  # This file

````

---

## 🔧 Setup Instructions

### 1. Clone this repo

```bash
git clone https://github.com/your-username/goodfoods-reservation.git
cd goodfoods-reservation
````

### 2. Install dependencies

```bash
pip install -r requirements.txt
```

If there's no `requirements.txt`, install manually:

```bash
pip install gradio openai pandas
```

### 3. Add your NVIDIA API Key

Update the API key in `app.py`:

```python
client = OpenAI(
    api_key="YOUR_NVIDIA_API_KEY",
    base_url="https://integrate.api.nvidia.com/v1"
)
```

> You can use free API keys from [NVIDIA API Playground](https://platform.nvidia.com/)

---

## 🧪 Run the Gradio UI

```bash
python app.py
```

> A browser window will open at `http://localhost:7860`

---

## 🎥 Sample Use Case Flow

1. User: *"I want to book a party hall for 200 people"*
2. Assistant detects `venue_type = "hall"`
3. Asks follow-up questions:

   * City?
   * Date/time?
   * Food required?
   * Price range?
4. Assistant suggests 3 matching venues with `ID`s
5. User types venue ID → Booking Confirmed ✅

---

## 🧠 Powered By

* **🧠 NVIDIA LLaMA-3.1 8B Instruct** (`meta/llama-3.1-8b-instruct`) via `integrate.api.nvidia.com`
* **🧩 Gradio** – Interactive chatbot UI
* **📊 pandas** – Handles JSON venue data

---

## 📄 Example JSON Input Files

Each JSON file (`synthetic_room_hotels.json`, `synthetic_restaurant_tables.json`, `synthetic_banquet_halls.json`) must contain synthetic data with fields like:

```json
[
  {
    "hotel_id": 101,
    "name": "Blue Star Residency",
    "city": "Chennai",
    "area": "T Nagar",
    "room_type": "double",
    "ac": true,
    "price": 2500,
    "checkin_type": "24hr",
    "party_size": 2,
    "food_available": true,
    "cuisines": ["South Indian", "Chinese"]
  }
]
```

---

## 📌 Future Enhancements

* 🧾 Booking summary receipt (JSON or PDF)
* 🗂️ Admin panel for venue CRUD operations
* 🌐 Multi-language support
* 📱 Deploy as a mobile PWA

---

## 📄 License

MIT License – free to use and modify
