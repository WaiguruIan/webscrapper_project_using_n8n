# webscrapper_project_using_n8n

# 🎵 Spotify Release Monitor: A Stateful Data Pipeline
### *Turning "App-Break Disappointment" into Automated Intelligence*

## 📖 The "Why" (The Motivation)
We’ve all been there: you open your modded version of Spotify, ready to play that one specific song, only to find the app is non-functional because a mandatory mod-update was released. The cycle was always the same: **app breaks → manual browser check → download → fix.**

I built this project to eliminate the "Manual Update Trap." I was tired of "winging it" and checking APKMody daily just to see if I was still on the latest version. This tool shifts the burden from the human to the machine, providing proactive notifications so I can update **before** the app stops working.

---

## 🚀 Technical Highlights
This isn't just a scraper; it's a resilient monitoring system designed to handle real-world web obstacles.

* **Stateful Memory Management:** To avoid "Notification Fatigue," I implemented a persistent memory layer using **Google Sheets**. The system compares live web data against stored states and only triggers an alert if a version transition is detected.
* **Resilient Web Scraping:** Using **ScraperAPI**, the workflow bypasses anti-bot firewalls and handles IP rotation automatically, ensuring 100% uptime even when hosted on shared cloud environments.
* **Data Normalization Engine:** Integrated a custom **JavaScript layer** to sanitize and format disparate date strings (e.g., matching "February 19, 2026" to ISO database standards), ensuring bulletproof logic comparisons.
* **Nairobi-Synced Scheduling:** Optimized for **UTC+3 (Nairobi Time)** to ensure the 1-hour polling cycle aligns with local peak usage.

---

## 🛠️ Tech Stack
| Component | Technology |
| :--- | :--- |
| **Orchestration** | n8n (Low-code Automation) |
| **Scraping Layer** | ScraperAPI (Proxy & Fingerprint Management) |
| **Persistence** | Google Sheets API (State Database) |
| **Alerting** | ntfy.sh (Mobile Push Notifications) |
| **Logic** | JavaScript (Data Sanitization) |

---

## 🔧 Engineering Challenges Solved
### **The "Date Mismatch" Bug**
**Challenge:** The website provided dates in human-readable format ("February 19"), while the database stored them differently, causing the filter to trigger false-positive notifications every hour.
**Solution:** I engineered a "Matchmaker" expression using `.toString().trim()` and a ternary logic gate to normalize the strings before they hit the comparison node.

### **The Shared-IP Block**
**Challenge:** Running on a shared cloud instance led to frequent "403 Forbidden" errors.
**Solution:** I decoupled the request from the server IP by routing traffic through a residential proxy layer (ScraperAPI) and implementing a **Retry-on-Fail** policy (3 attempts, 60s intervals).

---

## 📂 Deployment
1. Import `spotify-updater-workflow.json` into n8n.
2. Connect Google Sheets OAuth2 credentials.
3. Configure `ntfy` topic for mobile alerts.

---
**Author:** Ian Waiguru 
*Built for personal satisfaction and 24/7 music reliability.*
