
# 🏨 GoodFoods Conversational Reservation Agent

An **end-to-end GenAI assistant** built using the `LLaMA-3.1 8B Instruct` model (via NVIDIA API), capable of handling **hotel room reservations**, **restaurant table bookings**, and **banquet hall event planning** through natural language conversation.

Built without LangChain using a custom tool-calling architecture, the agent interprets user intent, asks smart follow-ups, and returns tailored venue recommendations from synthetic datasets.

---

## 💡 Project Overview

GoodFoods is a fictional multi-location restaurant and hospitality chain. This conversational AI assistant enables:

| Use Case              | Options Supported                                        |
|-----------------------|----------------------------------------------------------|
| 🛏️ Room Booking        | Single, Double, Suite; AC/Non-AC; food/cuisine; 12/24 hr |
| 🍽️ Table Reservation   | 2, 4, or 6 seats; AC/Non-AC; Veg/Non-Veg; cuisine         |
| 🎉 Banquet Hall Booking | 20–500 pax; price, food, cuisine, AC, decor (optional)     |

The assistant dynamically extracts booking **intent**, fills required **fields** through conversation, and presents relevant **venue suggestions** from curated synthetic datasets.

---
## ✅ Features

| Feature                          | Description |
|----------------------------------|-------------|
| 🧠 **LLM Intent & Slot Filling** | Determines booking type and extracts parameters via structured prompting |
| 🧰 **Tool Calling Architecture** | Uses LLM to decide and update fields in JSON dynamically |
| 🏢 **Venue Recommendations**     | Filters and returns top venue matches based on user preferences |
| 💬 **Conversational Agent**      | Gradio/CLI chatbot interface that mimics natural interaction |
| 🧾 **Synthetic Datasets**        | 3 JSONs with 100+ records including price, food, capacity, AC, cuisine |
| 🚫 **No LangChain / External Frameworks** | Pure Python + OpenRouter/NVIDIA API integration |

---

## 🧱 System Architecture

```mermaid
graph TD
  User -->|Text prompt| UI[Gradio or CLI]
  UI --> LLM
  LLM -->|Intent + slot filling| ToolCalling[Field Updater]
  ToolCalling --> VenueFilter[Venue Recommender]
  VenueFilter --> BookingResponse
  BookingResponse --> UI
````

---

## 🚀 Setup Instructions

### 1. Clone the repository
```bash
git clone https://github.com/yourusername/goodfoods-genai-reservation.git
cd goodfoods-genai-reservation
````

### 2. Install dependencies

```bash
pip install -r requirements.txt
# or manually
pip install gradio pandas openai
```

### 3. Set up NVIDIA API key

```bash
export OPENAI_API_KEY="your-nvidia-api-key"
```

### 4. Add synthetic dataset files

Place these files in the root directory:

* `synthetic_room_hotels.json`
* `synthetic_restaurant_tables.json`
* `synthetic_banquet_halls.json`

### 5. Run the app

```bash
python app.py
# Or to launch the Gradio UI
python gradio_ui.py
```

---

## 🧠 Prompt Engineering Approach

### System Roles

* **LLM decides venue type** (room/table/hall)
* **LLM handles slot filling** via dynamic JSON-based prompts
* **No rigid logic trees**, enabling flexible multi-turn dialog

### 📤 Sample Prompts

**1. Intent Detection**

```json
You are an assistant that extracts booking intent from user input.
Return only this JSON:
{
  "venue_type": "room" | "table" | "hall"
}
```

**2. Slot Filling Prompt**

```json
You are helping to fill the field '{field}' in this booking info:
{current_state_json}
Only return updated JSON for that field.
```

---

## 🏗️ Tool-Calling Architecture

✅ LLM selects which parameter to ask next
✅ All fields stored and updated in a centralized JSON object
✅ Venue matcher uses semantic + rule-based filtering

No LangChain or external orchestration framework is used.

---

## 📁 Dataset Structure

Each JSON file contains structured metadata like:

```json
{
  "id": "H001",
  "name": "GoodFoods Grand Residency",
  "city": "Chennai",
  "room_type": "Suite",
  "AC": "Yes",
  "food": "Veg",
  "cuisine": "Indian",
  "price": 3500
}
```

### Files:

* `synthetic_room_hotels.json`: room\_type, AC, city, cuisine, price
* `synthetic_restaurant_tables.json`: table size, cuisine, AC, veg/non-veg
* `synthetic_banquet_halls.json`: pax capacity, AC, price, cuisine, decor

---

## ✨ Example User Journeys

### 🛏️ Hotel Room Booking

> User: I want to book a suite for 2 people
> → Bot: Which city are you looking in?
> → Bot: Do you want 12hr or 24hr check-in?
> → Bot: AC or non-AC?
> → Bot: Food preference and cuisine?
> → ✅ Venue options with IDs
> → ✅ Final confirmation with venue ID

---

### 🍽️ Table Reservation

> User: Can I get a table for 4 in Coimbatore tonight?
> → Bot: AC/Non-AC preference
> → Bot: Cuisine type
> → ✅ Recommends table options
> → ✅ Booking confirmed

---

### 🎉 Banquet Hall Booking

> User: I need a hall for 150 people this weekend
> → Bot: City and event date
> → Bot: Budget and food type
> → Bot: Cuisine and decor needs
> → ✅ Venue shortlisting and booking ID

---

## 📈 Business Strategy Summary

### Pain Point

Traditional web forms are slow, inflexible, and not conversation-friendly.

### Value Delivered

* ✅ One unified conversational interface for multiple venue types
* ✅ Intelligent field collection and venue matching
* ✅ Potential for upselling (food add-ons, decor, services)
* ✅ Insightful analytics on demand patterns per location

---

## 📋 Assumptions

* User queries are in English with clear intent
* Venue inventory is static (no live availability or pricing)
* Payment, notification, or loyalty modules are not integrated

---

## ❌ Limitations

* No real-time booking sync with backend systems
* No cancellation/modification workflows
* Not yet mobile-optimized for production deployment

---

## 🔮 Future Enhancements

| Feature                           | Status |
| --------------------------------- | ------ |
| 💳 Payment & invoice integration  | 🔜     |
| 🌍 Multi-language interface       | 🔜     |
| 📱 Mobile-first UI (React Native) | 🔜     |
| 🔗 Live backend API connectivity  | 🔜     |
| 🔁 Booking change/cancel support  | 🔜     |

---

## 📊 Evaluation Rubric Compliance

| Requirement                             | Status |
| --------------------------------------- | ------ |
| LLM tool-calling (dynamic JSON logic)   | ✅      |
| Venue-type detection                    | ✅      |
| Slot-filling with follow-up questions   | ✅      |
| 50–100+ venue entries with metadata     | ✅      |
| Multi-type booking system               | ✅      |
| Pure Python (no LangChain, clean logic) | ✅      |
| NVIDIA API (LLaMA-3.1 8B) integration   | ✅      |
| Gradio or CLI interface                 | ✅      |


---

## 📄 License

This project is licensed under the MIT License — free for academic and commercial use with attribution.
