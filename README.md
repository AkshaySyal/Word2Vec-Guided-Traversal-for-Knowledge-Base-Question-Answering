# Word2Vec-Guided-Traversal-for-Knowledge-Base-Question-Answering
This project implements a knowledge base question answering (KBQA) system that performs graph traversal (e.g., BFS) from a starting entity, selecting promising paths based on Word2Vec-based cosine similarity scores between relations and the query, to find answer entities, with performance evaluated using the F1 score.

# Problem Statement

<img width="1878" height="267" alt="image" src="https://github.com/user-attachments/assets/a3f86924-fe96-4d50-a7a4-72258669542c" />


# Solution Summary
- Developed a **Knowledge Base Question Answering (KBQA) system** to answer natural language questions using a **knowledge graph (KG)**.

- **Technical Workflow**:
  - Loaded KG as a Pandas DataFrame of triples: `start_node`, `relation`, `end_node`.
  - Transformed into an **adjacency matrix** for efficient graph traversal.
  - For each question (with a starting entity):
    - Initiated **Breadth-First Search (BFS)** from the starting entity.
    - Used `get_rel_score_word2vecbase`:
      - Leveraged a **pre-trained Word2Vec model**.
      - Computed cosine similarity between query and relation (edge).
      - Guided traversal toward **high-scoring, promising edges**.
    - Collected answer entities from promising paths.

- **Evaluation**:
  - Compared retrieved answers against gold answers.
  - Computed **F1 score** to account for varying number of correct answers.
  - Achieved **average F1 score: 0.4654** across question dataset.

- **Key Insights**:
  - Employed a **focused crawl strategy**:
    - Discarded low-scoring paths.
    - Prioritized paths with high relation-query similarity.
  - Found that:
    - All correct answers were within **two hops** of the start entity.
    - Each hop typically involved a **single relation** leading to multiple answers.
    - KG was **incomplete** — some correct answers were missing from the graph.

- **Conclusion**:
  - Demonstrated the value of **Word2Vec-guided graph traversal** for KBQA.
  - Showed that relation-aware BFS can extract relevant answers with moderate success, setting a foundation for future improvements.
