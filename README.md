# Kitchen Vision

Kitchen Vision is a Streamlit app that accepts a pantry photo and generates:

* Detected pantry items and categories
* 3 simple recipe suggestions (3-step each)
* Health score for each recipe
* Grocery list of missing items and suggested substitutions

This repository includes a mock mode so you can run the app without API keys.

---

## Quickstart (Local Setup)

1. Copy `.env.example` to `.env` and set:

```
KV_PROVIDER=mock
```

This runs the project in demo mode without API keys.

2. Create a virtual environment and install requirements:

```
python -m venv .venv
.venv\Scripts\activate
pip install -r requirements.txt
```

3. Run the Streamlit app:

```
streamlit run app.py
```

Then open your browser:

```
http://localhost:8501
```

---

## Using a Real AI Provider

### OpenAI

Set the provider in `.env`:

```
KV_PROVIDER=openai
OPENAI_API_KEY=your_api_key_here
```

Then implement provider calls in:

```
services/vision_service.py
```

You can also extend:

```
services/recipe_service.py
```

to generate richer AI recipes.

---

### GemeAI (Optional)

Set in `.env`:

```
KV_PROVIDER=gemeai
GEMEAI_API_KEY=your_api_key
GEMEAI_ENDPOINT=https://api.geme.ai
```

The adapter is already included in:

```
services/providers/gemeai_provider.py
```

---

## Docker

Build Docker image:

```
docker build -t kitchen-vision .
```

Run container:

```
docker run -p 8501:8501 --env-file .env kitchen-vision
```

---

## Deployment

### Streamlit Cloud

1. Push this repository to GitHub
2. Go to Streamlit Cloud
3. Connect your repository
4. Set secrets (API keys) in Streamlit dashboard

### Docker Deployment

Use the included `Dockerfile` to deploy to:

* AWS
* Render
* Railway
* Google Cloud

---

## Example Output

Example JSON response:

```
{
  "detected_items": ["rice", "pasta", "canned tomatoes", "olive oil", "salt", "eggs"],
  "categories": {
    "Dry Storage": ["rice", "pasta", "canned tomatoes", "olive oil", "salt"],
    "Cold Storage": ["eggs"],
    "Frozen": [],
    "Fresh Produce": []
  },
  "recipes": [
    {
      "title": "Pasta with Tomato Sauce",
      "ingredients": ["pasta", "canned tomatoes", "olive oil"],
      "steps": [
        "Prepare ingredients",
        "Cook ingredients",
        "Serve and enjoy"
      ],
      "time_minutes": 15,
      "difficulty": "Easy"
    }
  ],
  "missing": []
}
```

---

## Notes

* This project is designed to make **AI provider integration easy**.
* Providers like **OpenAI, Gemini, Azure AI** can be added easily.
* Follow the comments inside service files to extend functionality.

---

## Author

Kitchen Vision Project
