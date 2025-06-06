#  AI Customer Support Agent - An Agentic Multimodal RAG Application 

A **Flask-based chatbot** powered by **RAG (Retrieval-Augmented Generation)** for customer support, featuring **multimodal inputs (text, image, speech)** 🅰, **multilingual magic** 🌍, **dynamic FAQ uploads** , **query analytics** 📊, and **ticket escalation** via **RabbitMQ** 🐇. The UI rocks a sleek, cosmic dark theme with sparkling animations .

---

##  Demo Video Link :

[Link](https://drive.google.com/file/d/11sBW-u0XXArfYTVrJadwa-Ock5k261JB/view?usp=sharing)

---

##  Features

- **RAG Chatbot:** Answers queries using FAISS + Cohere’s free API.
- **Text-to-Speech (TTS):** Speaks responses when speech mode is enabled.
- **Image-to-Text:** Upload images (PNG/JPEG) to extract text with pytesseract and display them in chat.
- **Speech Input:** Ask questions via speech recognition (English, Spanish, French).
- **Multilingual:** Supports English, Spanish, and French with Google Translator.
- **Dynamic FAQs:** Upload new `faq.txt` files to update responses instantly.
- **Analytics Sidebar:** Tracks query frequency live with theme cards (Order Tracking, Returns, Support Contact, Other).
- **Escalation System:** Routes complex queries to RabbitMQ and logs them in `tickets.json`.
- **Cosmic UI:** Dark gradient background, neon chat bubbles, sparkly animations, and clear input labels .

---

## Prerequisites

- Python 3.8+ (tested with 3.12)
- RabbitMQ
- macOS/Linux (tested on macOS)
- Tesseract OCR (`brew install tesseract`)
- Cohere API key from [https://cohere.com/](https://cohere.com/)

---

## ⚙️ Setup

### Clone the Repository:
```bash
git clone <your-repo-url>
cd ai-customer-support-agent
```

### Create Virtual Environment:
```bash
python3 -m venv venv
source venv/bin/activate
```

### Install Dependencies:
```bash
pip install cohere==4.50 flask==2.3.3 langchain-community==0.2.0 langchain-huggingface==0.0.3 langgraph==0.2.0 faiss-cpu==1.8.0 deep-translator==1.11.4 pika==1.3.2 sentence-transformers==2.6.1 httpx==0.23.0 langchain-core==0.2.0 pydantic==2.7.0 pydantic-core==2.18.1 Pillow==10.3.0 pytesseract==0.3.10
```

### Configure API Key:
- Sign up at  [https://dashboard.cohere.ai/](https://dashboard.cohere.ai/), grab your free API key.
- In `app.py`, replace:
```python
co = cohere.Client("your-cohere-api-key")
```
with your actual API key.

### Set Secret Key:
```bash
python3 -c "import secrets; print(secrets.token_urlsafe(32))"
```
Replace the secret key in `app.py`:
```python
app.secret_key = "your-new-generated-key"
```

### Install Tesseract:
```bash
brew install tesseract
tesseract --version
```

### Start RabbitMQ:
```bash
rabbitmq-server
```

###  Run the App:
```bash
export TOKENIZERS_PARALLELISM=false
python3 app.py
```
Then open  [http://127.0.0.1:5000/](http://127.0.0.1:5000/)

---

##  Usage

-  **Text Queries:** Type questions like _“How do I track my order?”_ in the “Type Your Question” field.
-  **Image Queries:** Upload PNG/JPEG images (e.g., receipts) via “Upload Image with Your Question”. Images appear in the chat, with extracted text processed for responses.
-  **Speech Queries:** Enable “Ask via Speech”, click 🎤, and speak your question (e.g., _“What is the return policy?”_).
-  **Language Toggle:** Choose English, Spanish, or French.
-  **FAQ Upload:** Upload a new `faq.txt` file to refresh FAQs.
-  **Clear Chat:** Reset conversation history.
-  **Query Analytics:** View live query counts in the sidebar (theme cards).
-  **Escalation:** Complex queries route to RabbitMQ and log in `tickets.json`.
-  **TTS:** Enable “Ask via Speech” to hear responses for text, image, or speech queries.

---

##  Project Structure

|  File               |  Description                                                     |
|:---------------------|:------------------------------------------------------------------|
| `app.py`              | Flask app with RAG, Cohere, RabbitMQ, image-to-text, and speech integration. |
| `templates/index.html`| Chat interface with text, image, and speech inputs.                |
| `static/style.css`    | Cosmic UI styling with neon effects and sparkles .               |
| `static/uploads/`     | Stores uploaded images for chat display.                          |
| `faq.txt`             | Sample FAQs database .                                          |
| `tickets.json`        | Logs for escalated queries .                                    |
| `query_counts.json`   | JSON analytics for query frequency .                            |

---

## Troubleshooting
### Chat or Images Not Displaying?
- Check terminal logs and browser DevTools (F12 → Console, Network).
- Verify images in `static/uploads/`.
- Clear browser cache:  
  Chrome → Settings → Privacy and Security → Clear Browsing Data → Cached images and files.

### Image-to-Text Issues?
- Ensure images have clear, printed text.
- Test Tesseract:
```bash
echo "Test" > test.txt
convert -size 200x100 xc:white -font DejaVu-Sans -pointsize 20 -fill black -annotate +15+55 'Test' test.png
python -c "from PIL import Image; import pytesseract; print(pytesseract.image_to_string(Image.open('test.png')))"
```
- Install ImageMagick:
```bash
brew install imagemagick
```

### Speech Recognition Issues?
- Ensure browser supports SpeechRecognition (Chrome recommended).
- Check DevTools → Console for errors like _“Speech recognition error”_.

###  Cohere API Errors?
- Verify API key at  [https://dashboard.cohere.ai/](https://dashboard.cohere.ai/).
- Test:
```bash
python -c "import cohere; co = cohere.Client('your-cohere-api-key'); print(co.check_api_key())"
```

###  RabbitMQ Issues?
- Ensure it’s running:
```bash
rabbitmqctl status
```

###  Analytics Not Updating?
- Check `query_counts.json` for theme counts.
- Verify `app.py` logs for `save_analytics()`.


