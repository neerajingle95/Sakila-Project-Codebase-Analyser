# 🧠 SakilaProject Codebase Analyzer (LLM-Powered)

This project analyzes the [SakilaProject](https://github.com/janjakovacevic/SakilaProject) GitHub codebase using a Large Language Model (LLM) to extract structured knowledge from Java, SQL, XML, and configuration files. It produces a JSON summary describing the purpose, method signatures, and complexity of each component.

## 🚀 Objectives

- Analyze a real-world multi-language codebase
- Use an LLM to generate structured summaries
- Output results in a clean JSON format
- Handle token limits through efficient chunking
- Showcase LLM orchestration using LangChain + Together.ai

---

## 📐 Approach & Architecture

```
[ Sakila Codebase ]
        ↓
[ File Reader: .java/.sql/.xml ]
        ↓
[ Chunking with LangChain ]
        ↓
[ Prompt → Together.ai LLM ]
        ↓
[ JSON Knowledge Output ]
```

### Methodology

1. **Code Loading**: Reads `.java`, `.sql`, `.xml`, `.properties` files recursively.
2. **Chunking**: Breaks content into 1500-character chunks using `RecursiveCharacterTextSplitter`.
3. **Prompting**: Sends code chunks with a system prompt requesting summaries and method metadata.
4. **LLM Integration**: Uses Together.ai's Mistral 7B via LangChain's `ChatOpenAI` wrapper.
5. **Parsing & Aggregation**: Parses JSON response from each chunk and merges by file.
6. **Output**: Writes all structured knowledge into `sakila_structured_knowledge.json`.

---

## 🛠️ Tech Stack

| Component     | Description                             |
|---------------|-----------------------------------------|
| LLM           | Together.ai - `mistralai/Mistral-7B-Instruct-v0.1` |
| Framework     | [LangChain](https://github.com/langchain-ai/langchain) |
| Tokenization  | `tiktoken` (via LangChain)              |
| Env Mgmt      | `python-dotenv`                         |
| File Support  | `.java`, `.sql`, `.xml`, `.properties`  |
| Output        | `sakila_structured_knowledge.json`      |

---

## ✅ Best Practices Applied

- **Token-aware chunking** to prevent LLM overflow
- **Structured prompting** to enforce consistent LLM output
- **Error-handled parsing** for malformed outputs
- **File-agnostic design** to support multiple languages
- **Secure API key handling** with `.env`

---

## 📁 Sample Output Format

```json
{
  "SakilaProject/src/CustomerDao.java": {
    "summary": "Handles database access for customer records.",
    "methods": [
      {
        "name": "getCustomerById",
        "signature": "public Customer getCustomerById(int id)",
        "description": "Fetches customer data from the database using the ID."
      }
    ],
    "complexity_notes": "Straightforward DAO pattern; no nested logic."
  }
}
```

---

## ⚠️ Assumptions & Limitations

- Assumes readable and reasonably commented source code
- LLM output must be valid JSON for parsing (malformed ones are skipped)
- Project is scoped to `.java`, `.sql`, `.xml`, `.properties`
- Does not currently compute static complexity (e.g., cyclomatic)

---

## 💻 How to Run

1. Clone this project and the SakilaProject codebase:
   ```bash
   git clone https://github.com/janjakovacevic/SakilaProject.git
   ```

2. Create a `.env` file with your Together API key:
   ```
   TOGETHER_API_KEY=your_actual_key_here
   ```

3. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

4. Run the main script:
   ```bash
   python analyze_codebase.py
   ```

---

## 🔮 Future Enhancements

- Add support for `.py`, `.yaml`, `.json` files
- Integrate `radon` for code complexity analysis
- Add RAG layer using vector DB (e.g., FAISS or Chroma)
- Create a Streamlit UI for visual inspection
- Add retry logic for failed JSON parses

---

## 👨‍💻 Author

**Neeraj Ingle**  
Senior Data Engineer | GenAI Practitioner  
📫 Open to collaborations in LLMOps, Data QA, and RAG systems
