# Style-Genie 
Style Genie is a fashion recommendation system. It uses a combination of machine learning and natural language processing to generate personalized fashion recommendations based on user input.

## Style-Genie File Structure

- repo  https://github.com/style-genie/
- overview https://github.com/ji-podhead/docs/blob/main/frontend/FRONTEND_README.md

### Main Components:

1.  Backend (backend/server):
    *   AI Agent: Manages user sessions and workflows using AI models.
    *   API Endpoints: Handles requests from the frontend.
    *   Database Interaction: Interacts with the PostgreSQL database.

2.  Frontend (frontend/stylectai):
    *   React Components: Provides UI elements for user interaction.
    *   Next.js Pages: Defines application routes and page structure.
    *   Image Uploader: Handles image uploads.
    *   User Form: Collects user input.

3.  Frontend (frontend/streamlit):
    *   Streamlit App: Alternative frontend for data visualization and interaction.

4.  Database (backend/postgres):
    *   PostgreSQL: Stores user data, session information, and other application data.

5.  Tools (tools/):
    *   Scraper: Used for scraping data from external sources.
    *   Pinecone: Used for interacting with the Pinecone vector database.


# Agent505
- repo  https://github.com/agent505/
- overview https://github.com/ji-podhead/docs/blob/main/agent505/README_EXTRA.md

Agent505 is a platform for building and managing AI agents that can interact with users through websockets. It uses FastAPI, Pydantic, Uvicorn, and other libraries to provide a flexible and scalable environment for developing and deploying AI-powered applications.

## Agent505 File Structure

```
Agent505/
├── .env.sample
├── main.py
├── pyproject.toml
├── requirements.txt
├── setup.py
├── src/
│   ├── __init__.py
│   ├── server.py
│   └── session.py
└── stylegenie.egg-info/
    ├── dependency_links.txt
    ├── PKG-INFO
    ├── requires.txt
    ├── SOURCES.txt
    └── top_level.txt
```
