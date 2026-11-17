# Heartline · Heart Health Information Assistant

**UCS420 Cognitive Computing · Assignment 10 · Even-roll track**

[Open in Google Colab](https://colab.research.google.com/github/doraem-on/New_cogn/blob/main/assignment10/main.ipynb) · [View the executed notebook on GitHub](main.ipynb)

Choose **Runtime → Run all** in Colab. Type a question in the **Ask Heartline** form and run that cell again for each new question. The last five replies stay on screen. The notebook contains the corpus, knowledge base and model training code, so it needs no API key or data uploads. Use fictional examples when sharing saved outputs.

## A two-minute demonstration

| Ask | What to look for |
| --- | --- |
| How do I choose a blood pressure cuff? | A sourced answer about cuff fitting. Expand the explanation by enabling **show_reasoning**. |
| How should I log my BP readings? | The same intent retrieves a different entry about recording measurements. |
| What about my heart? | The assistant offers two possible topics and asks for clarification. |
| What cream should I use for eczema? | The assistant explains the scope of the heart-health guide. |
| Should I double my pills? I can't breathe. | Emergency escalation takes priority over the medication question. |

## Where to find each requirement

| Notebook section | Implementation |
| --- | --- |
| 1 · Corpus | 96 distinct labeled English queries, with 12 per intent |
| 2 · Knowledge | Four parent categories, eight intent leaves, 28 concepts and 16 directed relationships. Each of the 16 knowledge entries has a source through its topic. |
| 3 · Language and learning | Lowercase conversion, tokenization, stopword filtering and domain lemmatization. Word and phrase TF-IDF features feed logistic regression. |
| 4 · Evaluation | Five-fold stratified out-of-fold predictions, per-intent precision, recall and F1, accuracy, a confusion matrix and actual errors |
| 5 · Integrated assistant | Priority rules for emergencies, missing input, urgent BP readings, personal-care requests, unsupported queries and low confidence. Accepted queries retrieve a specific knowledge entry. |
| 6 · Scenario bench | All eight intents, a separately worded question, unsupported healthcare, ambiguity and an emergency, plus rule precedence and retrieval checks |
| 7 · Colab interface | Reusable question form, answer history, source links and a reasoning view |

## What the scores tell us

The classifier identified **81 of 96 held-out intents** (84.4% accuracy, 0.842 macro F1). Every question was held out once, with the TF-IDF vocabulary and classifier refit inside each fold. Stress had the lowest recall (7 of 12). Broad wording such as “How can I sit less at work?” crossed the boundary between activity and stress.

The scenario bench separately checks 18 requests against expected assistant routes, and verifies that two blood-pressure questions retrieve different information. The small, hand-authored corpus measures classroom behavior. Real users may phrase symptoms or combine topics in ways the rules miss. This educational prototype is unsuitable for clinical triage or personal treatment decisions.

## Run locally

Install Python 3.12 and run the following from this folder. The final cell also works in Jupyter by editing the question string and rerunning it.

```sh
python3.12 -m venv .venv
source .venv/bin/activate
python -m pip install numpy scikit-learn matplotlib jupyterlab ipykernel
python -m jupyterlab main.ipynb
```
