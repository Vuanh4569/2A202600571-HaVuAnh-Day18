# Failure Analysis — Lab 18: Production RAG

**Nhóm:** Cá nhân  
**Thành viên:** Hà Vũ Anh (M1-M5)

---

## RAGAS Scores

| Metric | Naive Baseline | Production | Δ |
|--------|---------------|------------|---|
| Faithfulness | 0.0 | NaN | - |
| Answer Relevancy | 0.0 | NaN | - |
| Context Precision | 0.0 | NaN | - |
| Context Recall | 0.0 | NaN | - |

**Lưu ý:** RAGAS evaluation gặp vấn đề với asyncio/timeout, trả về NaN. Pipeline đã chạy thành công qua tất cả các bước (chunking, enrichment, indexing, reranking, LLM generation) nhưng RAGAS metrics không thể tính toán được.

## Bottom-5 Failures

### #1
- **Question:** Nhân viên được nghỉ bao nhiêu ngày khi kết hôn?
- **Expected:** 3 ngày phép kết hôn
- **Got:** NaN (RAGAS failed)
- **Worst metric:** faithfulness
- **Error Tree:** RAGAS evaluation failed → asyncio/timeout issue →
- **Root cause:** RAGAS metrics require proper async event loop and OPENAI_API_KEY for evaluation
- **Suggested fix:** Cấu hình OPENAI_API_KEY trong .env, hoặc sử dụng synchronous evaluation mode

### #2
- **Question:** Bảo hiểm sức khỏe PVI có hạn mức bao nhiêu cho nhân viên?
- **Expected:** 50 triệu/năm
- **Got:** NaN (RAGAS failed)
- **Worst metric:** faithfulness
- **Error Tree:** RAGAS evaluation failed →
- **Root cause:** Same as above
- **Suggested fix:** Same as above

### #3
- **Question:** Phụ cấp ăn trưa hàng tháng là bao nhiêu?
- **Expected:** 1.5 triệu
- **Got:** NaN (RAGAS failed)
- **Worst metric:** faithfulness
- **Error Tree:** RAGAS evaluation failed →
- **Root cause:** Same as above
- **Suggested fix:** Same as above

### #4
- **Question:** Nhân viên được nghỉ bao nhiêu ngày phép năm?
- **Expected:** 15 ngày (v2024)
- **Got:** NaN (RAGAS failed)
- **Worst metric:** faithfulness
- **Error Tree:** RAGAS evaluation failed →
- **Root cause:** Same as above
- **Suggested fix:** Same as above

### #5
- **Question:** Thâm niên bao nhiêu năm thì được cộng thêm ngày phép?
- **Expected:** 5 năm
- **Got:** NaN (RAGAS failed)
- **Worst metric:** faithfulness
- **Error Tree:** RAGAS evaluation failed →
- **Root cause:** Same as above
- **Suggested fix:** Same as above

## Case Study (cho presentation)

**Question chọn phân tích:** Nhân viên được nghỉ bao nhiêu ngày phép năm?

**Error Tree walkthrough:**
1. Output đúng? → Không thể đánh giá do RAGAS failed
2. Context đúng? → Pipeline đã retrieve context từ hierarchical chunking
3. Query rewrite OK? → Query được segment bằng underthesea
4. Fix ở bước: Cấu hình OPENAI_API_KEY và fix RAGAS async issue

**Nếu có thêm 1 giờ, sẽ optimize:**
- Fix RAGAS evaluation để có metrics thực tế
- Thử các chunking strategies khác (semantic, structure-aware)
- Tune RRF parameter k
- Thêm metadata filtering cho search
