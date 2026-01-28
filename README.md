# Aufgabe: RAG-Assistent: „Fragen Sie unsere Dokumente”

## Kontext/Motivation
Chatbots können selbst dann selbstbewusst klingen, wenn sie keine Antwort wissen. RAG (Retrieval-Augmented Generation) verbessert die Zuverlässigkeit, indem es das Modell dazu zwingt, bestimmte Dokumente als Belege zu verwenden. Heute erstellen Sie einen lokalen Agenten, der Fragen anhand Ihrer eigenen Dateien beantwortet und die Antworten auf Discord veröffentlicht.

## Lernziele
Die Schüler können…
- RAG erklären: relevante Texte abrufen → Antworten auf der Grundlage von Quellen geben
- einen Workflow mit Datenaufnahme, Chunking, Abruf und Prompting erstellen
- Ollama über das KI-Agenten-/Chat-Modell integrieren
- Discord-Ausgaben verantwortungsbewusst nutzen
- Halluzinationen bewerten und Sicherheitsvorkehrungen hinzufügen



# CRL_n8n

1. Clone or download the repo.
2. The files inside are the knowledge for the RAG system
3. use n8n to extract the information and to query


RAG Beispiele: Wählen Sie zunächst eines der folgenden Beispiele aus und machen Sie sich mit der Funktionsweise vertraut.

Example 1:
https://n8n.io/workflows/2339-breakdown-documents-into-study-notes-using-templating-mistralai-and-qdrant/

Example 2: RAG Ollama
https://n8n.io/workflows/5148-local-chatbot-with-retrieval-augmented-generation-rag/


Your final n8n application should also send a message to a Discord server (as seen in the lecture)

### Answerable
- „Was ist Retrieval-Augmented Generation?“
- „Warum sind agentische Systeme riskant?“
- „Welche Probleme gibt es bei automatisierten Entscheidungen?“

### Not answerable (important!)
- „Wie programmiert man ein neuronales Netz?“
- „Welche KI benutzt Apple Vision Pro intern?“
- „Ist KI in Deutschland gesetzlich geregelt?“

#### Promp beispiele:
System prompt (strict, grounded):
Du bist ein Dokumenten-Assistent. Antworte nur mit Informationen aus den bereitgestellten Textauszügen.
Wenn die Antwort nicht in den Auszügen steht, sage klar: „Nicht in den Dokumenten gefunden.“
Nenne am Ende Quellen im Format: [Datei | Chunk-ID].
Erfinde keine Fakten.
#### chat prompt soll kontext geben und den Format der prompt geben Beispielweiser
"
Frage: {{question_text}}
Dokument-Auszüge:
[{{source_file}} | {{chunk_id}}] {{chunk_text}}
…
Aufgabe: Beantworte die Frage kurz (max. 8 Sätze) und nenne Quellen.
"
#### Discord antwort

Message format:
Answer
Sources
A “confidence” line (simple):
“hoch” if at least 2 chunks support it
“mittel” if 1 chunk
“niedrig” if “nicht gefunden”

#### Testaufgaben (müssen dokumentiert werden)
- Stellen Sie 3 Fragen, die anhand der Dokumente beantwortet werden können.
- Stellen Sie 3 Fragen, die nicht beantwortet werden kann.
- Erfassen Sie die Ergebnisse (Screenshots oder Kopieren und Einfügen).

#### Kurze Reflexion (Stichpunkte):
- Wo kann es zu Halluzinationen kommen?
- Wie hat sich die Qualität der Abfrage auf die Antworten ausgewirkt?
- Welche Sicherheitsregel haben Sie implementiert?

#### Nutz den Block
Read files from disk
https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.readwritefile/
