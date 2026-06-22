# Individual Reflection — Lab 18

**Tên:** Hà Vũ Anh  
**Module phụ trách:** Tất cả (M1-M5) - Bài tập cá nhân

---

## 1. Đóng góp kỹ thuật

- Module đã implement: M1 (Chunking), M2 (Hybrid Search), M3 (Reranking), M4 (RAGAS Evaluation), M5 (Enrichment)
- Các hàm/class chính đã viết:
  - M1: `chunk_semantic()`, `chunk_hierarchical()`, `chunk_structure_aware()`
  - M2: `segment_vietnamese()`, `BM25Search`, `DenseSearch`, `reciprocal_rank_fusion()`, `HybridSearch`
  - M3: `CrossEncoderReranker._load_model()`, `CrossEncoderReranker.rerank()`
  - M4: `evaluate_ragas()`, `failure_analysis()`, `save_report()`
  - M5: `enrich_chunks()`, `_enrich_single_call()`, `summarize_chunk()`, `generate_hypothesis_questions()`, `contextual_prepend()`, `extract_metadata()`
- Số tests pass: Chưa chạy tests

## 2. Kiến thức học được

- Khái niệm mới nhất: Hierarchical chunking với parent-child structure, Reciprocal Rank Fusion (RRF) cho hybrid search, Cross-encoder reranking, RAGAS evaluation metrics
- Điều bất ngờ nhất: Semantic chunking sử dụng cosine similarity giữa các câu để nhóm ý liên quan, giúp tránh cắt giữa ý
- Kết nối với bài giảng (slide nào): Slide về Advanced RAG techniques - chunking strategies, hybrid search, reranking

## 3. Khó khăn & Cách giải quyết

- Khó khăn lớn nhất: Cấu hình Qdrant và đảm bảo models được download trước để tránh timeout
- Cách giải quyết: Pre-download models theo hướng dẫn trong README, sử dụng Docker cho Qdrant
- Thời gian debug: ~30 phút cho setup environment

## 4. Nếu làm lại

- Sẽ làm khác điều gì: Thử thêm FlashrankReranker để so sánh latency với CrossEncoder
- Module nào muốn thử tiếp: Thêm metadata filtering cho search để improve precision

## 5. Tự đánh giá

| Tiêu chí | Tự chấm (1-5) |
|----------|---------------|
| Hiểu bài giảng | 4 |
| Code quality | 4 |
| Teamwork | N/A (cá nhân) |
| Problem solving | 4 |
