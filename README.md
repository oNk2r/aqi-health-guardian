# 🌍 AQI Health Advisory System

A small web app that gives personalized health advice based on air quality. You enter your city, the AQI value and your health profile (for example, asthma), and it returns advice taken from WHO and EPA guidelines.

Built during the **AI for Sustainability Virtual Internship** (1M1B, AICTE, IBM SkillsBuild).

---

## How it works

This project uses **RAG (Retrieval-Augmented Generation) style retrieval**:

1. The WHO and EPA health guidelines are split into about 40 small chunks.
2. Each chunk is converted into an embedding (HuggingFace) and stored in ChromaDB.
3. When a user sends their AQI and health profile, the Flask backend searches ChromaDB for the most relevant chunks.
4. The backend puts those chunks together into a personalized advisory and sends it back as JSON.
5. The frontend shows the result in a color-coded layout.

```
User input (city, AQI, health profile)
        ↓
Flask API
        ↓
LangChain + ChromaDB (find relevant guidelines)
        ↓
Build the advisory
        ↓
JSON response → frontend display
```

The advice comes from real guidelines, not from a model making things up.

---

## Features

- Personalized advice for different profiles (asthma, elderly, children)
- AQI category and risk level
- Health guidance based on air quality
- Mask recommendations
- Outdoor activity advice
- Steps to reduce exposure

---

## Tech stack

| Part | Tools |
| --- | --- |
| Frontend | HTML, CSS, JavaScript |
| Backend | Python, Flask |
| RAG | LangChain, ChromaDB |
| Embeddings | HuggingFace (free, no API key needed) |
| Data | WHO Air Quality Guidelines, EPA Health Advisory Standards |

---

## Setup

You need Python 3.8 or higher. No API keys are needed.

```bash
# Clone the repository
git clone https://github.com/oNk2r/aqi-health-guardian.git
cd aqi-health-guardian

# Create and activate a virtual environment
python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Start the backend
python backend.py
```

The backend runs on `http://localhost:5000`.

Then open `frontend/index.html` in your browser.

---

## Example

**Input**
- City: Delhi
- AQI: 180
- Profile: Person with asthma

**Output**
```
AQI: 180 - Unhealthy

Health implications:
Some members of the general public may experience health effects;
sensitive groups may experience more serious effects.

Recommendations for you:
People with asthma should avoid long or heavy exertion.
Keep quick-relief medicine handy and follow your asthma action plan.

Outdoor activities:
Avoid long outdoor exertion. Consider indoor options.

Protective measures:
Wear an N95 mask if you must go outside. Use an air purifier indoors.

Mask recommendation:
N95 mask for everyone during outdoor exposure.
```

---

## Limitations

- **Not medical advice.** Please talk to a doctor for health decisions.
- **AQI is entered by the user.** The app does not read live data from air quality sensors or APIs.
- **Static knowledge.** The advice is based on a fixed set of guidelines (about 40 chunks).
- **No LLM.** The advice is built from retrieved guidelines only.

## Possible improvements

- Fetch live AQI for a city from an air quality API
- Add an LLM to phrase the answer, while still using the retrieved guidelines
- Add automated tests
- Support more health profiles

---

## Project structure

```
aqi-health-guardian/
├── frontend/
│   ├── index.html
│   ├── styles.css
│   └── script.js
├── data/
│   └── health_guidelines.txt
├── backend.py
├── requirements.txt
├── README.md
└── .gitignore
```

---

## Responsible AI

- **Fairness:** uses WHO and EPA standards that apply everywhere.
- **Transparency:** sources are named and AQI categories are explained.
- **Privacy:** no user data is stored and nothing is tracked.
- **Safety:** recommendations are cautious, with clear warnings for hazardous air.

## SDG alignment

- **Primary:** SDG 3, Good Health and Well-being
- **Secondary:** SDG 11 (Sustainable Cities), SDG 13 (Climate Action)

---
