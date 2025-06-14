
# 🍽️ GoodFoods AI Reservation Assistant

An end-to-end conversational AI assistant for **restaurant table bookings**, **hotel room reservations**, and **banquet hall bookings** using an LLM-powered tool-calling architecture. Built using the **LLaMA-3.1 8B Instruct** model via NVIDIA's OpenAI-compatible API.

---

## 💡 Project Overview

**GoodFoods** is a fictional restaurant chain with multiple city locations. This assistant allows users to:
- Book **rooms** (single/double/suite with AC or non-AC)
- Reserve **restaurant tables** (2/4/6 people)
- Book **party halls** (20–500 pax) for events

The assistant dynamically determines:
- Venue type (`room`, `table`, or `hall`)
- Missing information via smart follow-up questions
- Matching venues from 100+ synthetic entries
- Final booking confirmation with booking ID

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

## 📁 Dataset Structure

Three synthetic JSON files:

* `synthetic_room_hotels.json`: `room_type`, `AC`, `price`, `food`, `cuisine`
* `synthetic_restaurant_tables.json`: `table_seats`, `AC`, `food`, `cuisine`
* `synthetic_banquet_halls.json`: `capacity`, `AC`, `food`, `price`, `cuisine`

Each entry includes:

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

---

## 🛠️ Tech Stack

* 🧠 **LLM**: `meta/llama-3.1-8b-instruct` via NVIDIA API
* 🌐 **Frontend**: Gradio (also supports CLI)
* 🐍 **Backend**: Python (no LangChain)
* 📦 **Data**: JSON-based synthetic datasets

---

## 🚀 How to Run

1. **Install dependencies**

```bash
pip install gradio openai pandas
```

2. **Set up NVIDIA API key**

```bash
export OPENAI_API_KEY="your-nvidia-api-key"
```

3. **Run the app**

```bash
python app.py
```

4. Or launch Gradio UI:

```bash
python gradio_ui.py
```

---

## 🧪 Sample Booking Flow

> **User**: I want to book a room in Chennai
> **Assistant**: How many people will stay?
> **User**: 2
> **Assistant**: Do you prefer a single, double, or suite room?
> **User**: Double
> **Assistant**: Do you want AC or non-AC?
> *(...)*
> **Assistant**: Based on your preferences, here are some options:

```
🔹 ID: H001 - GoodFoods Residency, ₹3200, Veg, AC, Indian  
🔹 ID: H017 - Grand Elite, ₹3400, AC, North Indian  
```

> To confirm your booking, enter the venue ID.

---

## 📊 Evaluation Rubric Alignment

| Requirement                            | Status |
| -------------------------------------- | ------ |
| LLM tool-calling (not hardcoded)       | ✅      |
| Venue type detection (room/table/hall) | ✅      |
| Follow-up questions per venue type     | ✅      |
| 50–100+ venue entries with metadata    | ✅      |
| Venue recommendation engine            | ✅      |
| Frontend via Gradio or Streamlit       | ✅      |
| No LangChain or external frameworks    | ✅      |
| Uses open LLaMA model (via NVIDIA)     | ✅      |

---

## 📌 Future Enhancements

* ✅ Add payment confirmation step
* ✅ Support multi-lingual booking
* ✅ Deploy via Hugging Face Spaces or Streamlit Cloud

---

## 🙌 Acknowledgments

* [Meta LLaMA-3.1 8B Instruct](https://ai.meta.com/llama)
* [NVIDIA AI Chat API](https://integrate.api.nvidia.com)
* [Gradio](https://gradio.app)

---

## 📄 License

MIT License. Free to use and modify for academic or commercial use.
