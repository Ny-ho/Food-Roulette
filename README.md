# 🎰 Food Roulette

An asynchronous, full-stack web application designed to solve the age-old question: **"Where should we eat?"**

Food Roulette integrates multiple real-world mapping and location APIs (Foursquare, OpenStreetMap) to discover local restaurants based on your GPS coordinates, allowing you to select your favorites and let a "Slot Machine" algorithm randomly decide your fate.

---

## 📸 Previews


### 1. Finding Local Restaurants
<img width="1919" height="968" alt="Screenshot 2026-05-19 210052" src="https://github.com/user-attachments/assets/18afb646-c969-4110-bccb-ba4b8486212d" />

*Users can auto-detect their location via GPS, and filter results dynamically by Cuisine or Rating.*

### 2. The Roulette Spin
<img width="693" height="692" alt="Screenshot 2026-05-19 210122" src="https://github.com/user-attachments/assets/1f837491-854a-4a60-8926-0c7ec9bd4c2d" />

*A custom-built Slot Machine animation builds suspense before revealing the chosen restaurant.*

### 3. The Final Result
<img width="1915" height="945" alt="Screenshot 2026-05-19 210231" src="https://github.com/user-attachments/assets/888f0c7d-9015-4af6-adb1-4b2c798a0e12" />

*Displays the winning location, a randomly generated 'Chef's Choice' dish/drink, and a direct deep-link to Google Maps for navigation.*

---

## 🚀 Features

* **Multi-API Fallback System:** Prioritizes high-quality Foursquare data. If Foursquare fails, hits rate limits, or lacks regional coverage, it automatically falls back to an OpenStreetMap (Overpass API) architecture with reverse-geocoding.
* **Asynchronous Performance:** Built with FastAPI and `asyncio.gather`. Concurrent reverse-geocoding fetches 30+ addresses simultaneously, reducing load times drastically.
* **Zero-Dependency Frontend:** The UI is built entirely with Vanilla JavaScript and pure CSS. No heavy React bundles, resulting in lightning-fast initial load times.
* **Fault-Tolerant UX:** Features explicit form validation, preventing "silent failures" or confusing location guesses if the user forgets to input data.

---

## 🛠️ Tech Stack

* **Backend:** Python, FastAPI, Uvicorn, Httpx (Async HTTP requests)
* **Frontend:** Vanilla HTML, CSS, JavaScript (No frameworks)
* **APIs Used:** 
  * Foursquare Places API v3
  * OpenStreetMap (Overpass API)
  * Nominatim (Reverse Geocoding)

---

## 💻 How to Run Locally

1. **Clone the repository**
   ```bash
   git clone https://github.com/YourUsername/food-roulette.git
   cd food-roulette
   ```

2. **Set up environment variables**
   Copy the example file and configure your API keys (optional, the app will fallback to OpenStreetMap if left blank).
   ```bash
   cp .env.example .env
   ```

3. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

4. **Run the server**
   ```bash
   uvicorn main:app --reload
   ```

5. **Open in Browser**
   Navigate to `http://localhost:8000`

---

## 🧠 Architectural Decisions (For Interviewers)

* **Why not use Google Places API exclusively?** 
  Google Places is expensive. This project demonstrates how to build a robust, cost-effective system by layering free APIs and using graceful degradation (Foursquare → OpenStreetMap).
* **Why the explicit input validation?**
  Originally, the backend used an IP-Geolocation service to silently guess the user's city if inputs were empty. I replaced this with strict frontend validation to prevent "magic behavior" and ensure the user always understands why a specific location was searched.
