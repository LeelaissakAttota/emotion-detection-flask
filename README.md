# 😡😨😊 Emotion Detection App — IBM Watson NLP + Flask

![Language](https://img.shields.io/badge/Language-Python%203.11-3776AB?style=flat-square&logo=python&logoColor=white)
![Framework](https://img.shields.io/badge/Framework-Flask-000000?style=flat-square)
![NLP](https://img.shields.io/badge/NLP-IBM%20Watson%20Emotion%20API-052FAD?style=flat-square&logo=ibm&logoColor=white)
![Testing](https://img.shields.io/badge/Testing-unittest-2E7D32?style=flat-square)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen?style=flat-square)

---

## 📌 Project Overview

Flask web application that performs **real-time emotion analysis** on 
text using **IBM Watson NLP Emotion Prediction API**. Detects 5 
emotions — anger, disgust, fear, joy, and sadness — with confidence 
scores, then identifies the **dominant emotion** automatically.

Built as a final project for the **IBM AI & Python Development** 
certification, featuring a modular package structure, REST API 
endpoint, unit tests for all 5 emotions, and error handling for 
invalid inputs.

**Domain:** NLP — Emotion Detection  
**API:** IBM Watson NLP Emotion Aggregated Workflow  
**Backend:** Flask  

---

## 📂 Project Structure

```
oaqjp-final-project-emb-ai/
│
├── EmotionDetection/
│   ├── __init__.py              # Package init
│   └── emotion_detection.py    # Core IBM Watson NLP API wrapper
│
├── server.py                   # Flask routes (/emotionDetector + /)
├── templates/
│   └── index.html              # Web UI
├── static/
│   └── mywebscript.js          # Frontend AJAX calls
└── test_emotion_detection.py   # Unit tests (5 emotions)
```

---

## 🛠️ Tech Stack

| Component | Technology |
|---|---|
| Backend | Flask |
| NLP API | IBM Watson NLP Emotion Prediction |
| HTTP | requests + JSON |
| Testing | Python unittest |
| Frontend | HTML + JavaScript (AJAX) |

---

## 🔍 Core Emotion Detection Logic

```python
def emotion_detector(text_to_analyse):
    url = 'https://sn-watson-emotion.labs.skills.network/v1/watson.runtime.nlp.v1/NlpService/EmotionPredict'
    headers = {"grpc-metadata-mm-model-id": "emotion_aggregated-workflow_lang_en_stock"}
    data = {"raw_document": {"text": text_to_analyse}}

    response = requests.post(url, headers=headers, json=data)
    emotions = response.json()['document']['emotion']
    dominant_emotion = max(emotions, key=emotions.get)

    return {
        'anger': emotions['anger'],
        'disgust': emotions['disgust'],
        'fear': emotions['fear'],
        'joy': emotions['joy'],
        'sadness': emotions['sadness'],
        'dominant_emotion': dominant_emotion
    }
```

---

## 🌐 Flask REST Endpoint

```python
@app.route("/emotionDetector")
def emotion_detector_function():
    text = request.args.get('textToAnalyze')
    response = emotion_detector(text)

    # Returns formatted string with all scores + dominant emotion
    # e.g. "anger: 0.12, disgust: 0.05, fear: 0.08, joy: 0.73, sadness: 0.02.
    #       The dominant emotion is joy."
```

**Error Handling:**
- Empty input → returns `None` for all emotions + `"Invalid Input! Please try again."`
- Status 400 from Watson API → graceful null response

---

## ✅ Unit Tests (5 Emotions)

```python
class TestEmotionDetection(unittest.TestCase):
    def test_joy(self):
        result = emotion_detector("I am glad this happened")
        self.assertEqual(result['dominant_emotion'], 'joy')

    def test_anger(self):
        result = emotion_detector("I am really mad about this")
        self.assertEqual(result['dominant_emotion'], 'anger')

    def test_disgust(self):
        result = emotion_detector("I feel disgusted just hearing about this")
        self.assertEqual(result['dominant_emotion'], 'disgust')

    def test_sadness(self):
        result = emotion_detector("I am so sad about this")
        self.assertEqual(result['dominant_emotion'], 'sadness')

    def test_fear(self):
        result = emotion_detector("I am really afraid that this will happen")
        self.assertEqual(result['dominant_emotion'], 'fear')
```

---

## 🎓 Skills Demonstrated

- IBM Watson NLP Emotion Prediction API integration
- Flask web application with REST endpoint
- Modular Python package structure (`EmotionDetection/`)
- 5-emotion classification — anger, disgust, fear, joy, sadness
- Dominant emotion extraction via `max(emotions, key=emotions.get)`
- Input validation + error handling (empty input + API 400)
- Python `unittest` — test coverage for all 5 emotion classes
- Frontend AJAX integration with JavaScript

---

## 📜 Certifications

| Certification | Issuer | Platform |
|---|---|---|
| IBM Data Science Professional Certificate | IBM | Coursera |
| IBM Generative AI Professional Certificate | IBM | Coursera |
| IBM Agentic AI with RAG Certificate | IBM | Coursera |
| IBM RAG and Agentic AI Professional Certificate | IBM | Coursera |

---

## 🤝 Connect with Me

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Leela%20A-0077B5?style=flat-square&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/leela-a)
[![Gmail](https://img.shields.io/badge/Gmail-attotaleelaissak@gmail.com-D14836?style=flat-square&logo=gmail&logoColor=white)](mailto:attotaleelaissak@gmail.com)
[![GitHub](https://img.shields.io/badge/GitHub-Leelaissakattaota-181717?style=flat-square&logo=github&logoColor=white)](https://github.com/Leelaissakattaota)
