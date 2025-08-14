```mermaid
graph TD
    %% Input Layer
    A[Input Layer] -->|Risk Controls (PDF)| B[Document Ingestion]
    A -->|Audit Logs (CSV)| C[Data Ingestion]
    
    %% Processing Layer
    B --> D[Document Indexing<br>(FAISS Vector Store)]
    D -->|Embedding-based Retrieval| E[Retrieval-Augmented Generation (RAG)]
    C --> F[Log Parsing<br>(pandas)]
    E -->|Relevant Controls| G[Exception Detection]
    F -->|Log Entries| G
    G -->|LLM Analysis| H[Reasoning Loop<br>(LangChain Agent)]
    H -->|Optional: Sub-Agents| I[Multi-Agent Coordination<br>(e.g., Retrieval, Analysis)]
    
    %% Output Layer
    H --> J[Report Generation<br>(LLM + Prompt Template)]
    J --> K[Summary Report<br>(Markdown/Streamlit UI)]
    
    %% Monitoring
    H -->|Log Outputs| L[Monitoring & Logging<br>(agent.log)]
    
    %% Annotations
    classDef layer fill:#e6f3ff,stroke:#1e90ff,stroke-width:2px;
    class A,B,C,D,E,F,G,H,I,J,K,L layer;
    
    %% Data Flow Descriptions
    linkStyle 0,1 stroke:#ff4500,stroke-width:2px;
    linkStyle 2,3,4,5,6,7,8 stroke:#228b22,stroke-width:2px;
    
    %% Notes
    subgraph Notes
        N1[Key Components:<br>- LLM: OpenAI/xAI for reasoning<br>- LangChain: Orchestrates chains/agents<br>- FAISS: Enables RAG for document search<br>- Streamlit: Optional UI for demo]
        N2[Data Flow:<br>1. Ingest PDF/CSV<br>2. Index & retrieve controls<br>3. Analyze logs vs. controls<br>4. Generate report<br>5. Log for audit]
    end
```

## Diagram Explanation
- **Input Layer**: Accepts `Risk_Controls.pdf` (via PyPDF2) and `Audit_Logs.csv` (via pandas).
- **Processing Layer**:
  - **Document Indexing**: Converts PDF to a FAISS vector store for semantic search.
  - **RAG**: Retrieves relevant controls to ground LLM analysis.
  - **Log Parsing**: Processes CSV into structured data.
  - **Exception Detection**: Combines rule-based checks (e.g., Amount > $10,000) with LLM reasoning.
  - **Reasoning Loop**: LangChain agent iterates (e.g., ReAct pattern) to refine analysis.
  - **Multi-Agent (Optional)**: Sub-agents for retrieval, analysis, or reporting (Step 4).
- **Output Layer**: Generates a structured report (Markdown) and displays via Streamlit (optional).
- **Monitoring**: Logs agent actions for audit trails (Step 4).
- **Visual Cues**:
  - Blue boxes highlight modular components.
  - Orange arrows show input data flow; green arrows show processing/output flow.
  - Notes summarize tools and workflow for clarity.

## Usage
- **Render**: Use a Mermaid-compatible tool (e.g., GitHub, Mermaid Live Editor, or Colab with a Mermaid plugin) to visualize.
- **Download**: Save as `Agent_Architecture_Diagram.md` for inclusion in training materials or slides.
- **Customization**: Learners can edit the diagram in Mermaid syntax to reflect their use case (e.g., add a database input).