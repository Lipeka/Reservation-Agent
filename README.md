
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

### ✅ **Key Business Problems and Opportunities (Beyond Basic Reservation)**

| Business Problem                                         | Opportunity                                                                                                                |
| -------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| **1. High no-show rates or last-minute cancellations**   | Introduce automated confirmation/reminder flow via WhatsApp/SMS/email using the LLM agent.                                 |
| **2. Fragmented customer data across multiple branches** | Use the centralized reservation bot to unify customer profiles across all locations. Enables targeted marketing.           |
| **3. Difficulty in upselling during booking**            | AI agent can intelligently upsell higher-priced rooms, buffet packages, add-ons (decor, cake, live music) based on intent. |
| **4. Limited insights on user demand trends**            | All conversation data becomes usable for analytics (e.g. peak time analysis, cuisine demand heatmaps).                     |
| **5. Manual handling of bulk/banquet inquiries**         | Automate bulk booking qualification and data capture, reducing load on staff and speeding up lead response.                |
| **6. Inconsistent service across locations**             | LLM standardizes customer experience regardless of outlet. Brand reliability improves.                                     |

---

### ✅ **Success Metrics (Measurable KPIs)**

| Metric                           | Target Value (first 3–6 months) | Purpose                                        |
| -------------------------------- | ------------------------------- | ---------------------------------------------- |
| 🟢 Booking Completion Rate       | ≥ **80%**                       | Measures drop-offs; higher means smooth bot UX |
| 🟢 Avg. Booking Time             | ≤ **3 mins**                    | Indicates efficiency of form-filling with LLM  |
| 🟢 No-show Reduction             | ↓ by **15–20%**                 | Through reminders & confirmations              |
| 🟢 Manual Ops Load Reduction     | ↓ by **50%**                    | Time saved by AI over phone-based booking      |
| 🟢 Avg. Order Value              | ↑ by **10–15%**                 | Due to upselling from AI                       |
| 🟢 Conversion Rate of Hall Leads | ≥ **40%**                       | Indicator of lead qualification accuracy       |

---

### ✅ **Potential ROI (Return on Investment)**

| Component                             | ROI Driver                              | ROI Estimate                     |
| ------------------------------------- | --------------------------------------- | -------------------------------- |
| 💰 **Staff Cost Reduction**           | Automate 60–70% of routine queries      | \~\$5K–\$15K/month saved         |
| 💡 **Improved Occupancy Rate**        | Less drop-offs + better matching        | 10–20% occupancy increase        |
| 📈 **Higher Customer Lifetime Value** | Unified profiles + personalized promos  | 1.5x revenue per repeat customer |
| 📊 **Lead Conversion Boost**          | Faster banquet response = more bookings | +30–50 new event leads/month     |

---

### ✅ **Vertical Expansion Opportunities**

| Sector / Vertical                     | How the AI Agent Adapts                                                |
| ------------------------------------- | ---------------------------------------------------------------------- |
| 🛎️ **Hotel Chains**                  | Room, suite booking with check-in types, meal plan upselling           |
| 🏥 **Clinics/Hospitals**              | Appointment booking based on department, doctor availability, symptoms |
| 🎓 **Educational Institutions**       | Scheduling campus visits, event reservations, open house slots         |
| 🏢 **Corporate Offices / Co-working** | Conference room booking, food ordering, space allocation               |
| 🧘 **Wellness & Spa Centers**         | Treatment slot booking with therapists, packages, reminders            |

---

### ✅ **2–3 Unique Competitive Advantages**

1. **🎯 Intent-first, Tool-based Architecture**

   * LLM dynamically infers user needs and triggers modular booking logic via tool calling.
   * No hardcoding = scalable across different domains or venues with just schema swaps.

2. **💬 Multi-turn Memory with JSON State Engine**

   * Intelligent follow-up flow that remembers context and fills only the missing details.
   * Clean UX even for complex flows like hall bookings or filtered cuisine-based preferences.

3. **📦 3-in-1 Booking System (Room, Table, Hall)**

   * Most competitors only solve for one type. This system handles all with separate logic trees and matching filters – boosting operational coverage from day one.

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
