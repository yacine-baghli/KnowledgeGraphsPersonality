# Hybrid Knowledge Graph & Generative Personality Model

This project is a Python-based proof-of-concept (built in a Jupyter Notebook) that demonstrates how to create a "hybrid" Knowledge Graph (KG) by merging factual data with abstract personality insights. It then uses this unified graph in a RAG-like pattern to power a "Contextual-Generative Model" that simulates human behavior.

## 🚀 Features

Factual Extraction: Uses spacy's dependency parser to extract simple, factual (Subject, Predicate, Object) triples from text.

Abstract/Personality Extraction: Uses the Gemini 2.5 Pro model in a "model-in-the-loop" step to read text and infer abstract personality traits and behaviors.

Unified Knowledge Graph: Merges both factual and abstract triples into a single networkx graph, creating a rich, unified "brain" for a given subject.

RAG-on-KG: Implements a query_kg_for_persona function to "retrieve" a complete, structured "Persona Profile" from the graph.

Behavioral Simulation: Implements a generate_behavioral_response function that "augments" a new generative prompt with the retrieved profile, allowing it to simulate realistic behavior in new situations.

## 🛠️ How It Works (The Pipeline)

This project works in two main phases: 1. Graph Construction and 2. Generative Simulation.

Input Text: A block of unstructured text (our DOCUMENT_TEXT) is provided.

Factual Extraction: The text is processed by spacy. We use dependency parsing to find simple (Subject, Verb, Object) relations (e.g., ('Alex', 'reports_to', 'Dr. Kassir')).

Personality Extraction: The same text is fed to the Gemini 2.5 Pro model with a highly-specific prompt. The LLM acts as a psychologist, returning a JSON list of abstract triples (e.g., ('Alex', 'has_trait', 'Creative')).

Graph Unification: All triples are loaded into a single networkx.MultiDiGraph. This automatically merges all information onto a single node (e.g., the "Alex" node now has both factual and personality edges).

Retrieval (RAG): We use our query_kg_for_persona function to query the graph for a subject. This "retrieves" all connected facts and traits, formatting them into a "Persona Profile."

Augmented Generation (RAG): This "Persona Profile" is combined with a new, user-provided "Situation." This complete context is "augmented" into a final prompt and sent to Gemini to "generate" a realistic behavioral simulation.

## ⚙️ Setup & Installation

Follow these steps to set up your environment.

Clone or Download:
Get the project files (specifically the .ipynb notebook).

Create a Virtual Environment (Recommended):

python -m venv venv
source venv/bin/activate  # On Windows, use `venv\Scripts\activate`


Install Requirements:
Use the provided requirements.txt file (if available).

pip install -r requirements.txt


(If you don't have a requirements.txt file, install these manually: pip install spacy networkx matplotlib google-generativeai)

Download SpaCy Model:
You need the en_core_web_sm model for spacy's parser.

python -m spacy download en_core_web_sm


Set Your API Key:
The script requires a Google AI API Key for the Gemini model. Find the following line in the notebook and add your key:

genai.configure(api_key="YOUR_API_KEY_HERE")


## ▶️ How to Run

Start Jupyter:
From your terminal (with the virtual environment activated), run:

jupyter notebook


Open the Notebook:
Open the .ipynb file in your browser.

Run All Cells:
The easiest way to see the full pipeline is to select "Cell" > "Run All" from the top menu.

Check the Output:
The notebook is designed to be run from top to bottom. The final cells will:

Print the extracted factual and personality triples.

Display the final, color-coded Knowledge Graph using matplotlib.

Print the "Persona Profile" retrieved for each subject.

Print the final "Simulation" showing how the subject (e.g., "Alex") reacted to the test SITUATION.

## 🧪 Experimenting

You can easily test the model with your own data:

Change the Input: Modify the DOCUMENT_TEXT variable (e.g., in Section 2) with your own text.

Change the Test: Modify the SITUATION variable (e.g., in Section 10) to see how your subjects react to different scenarios.
