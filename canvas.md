# 🧠 AI Product Canvas — MoMo AI Financial Assistant

## 🎯 Canvas

| | Value | Trust | Feasibility |
|--|------|-------|------------|
| **Câu hỏi guide** | User nào? Pain gì? AI giải quyết gì mà cách hiện tại không giải được? | Khi AI sai thì user bị ảnh hưởng thế nào? User biết AI sai bằng cách nào? User sửa bằng cách nào? | Cost bao nhiêu/request? Latency bao lâu? Risk chính là gì? |
| **Trả lời** | **User:** Người dùng MoMo có nhu cầu quản lý chi tiêu cá nhân  <br><br> **Pain:**  <br> - Không nhớ mình tiêu tiền vào đâu  <br> - Ngại nhập chi tiêu thủ công  <br> - Không có insight rõ ràng  <br><br> **AI giải quyết:**  <br> - Tự động ghi chép giao dịch (auto log)  <br> - Tự động phân loại (auto classify)  <br> - Tổng hợp & báo cáo chi tiêu  <br><br> 👉 Khác biệt: giảm effort nhập liệu & tổng hợp mà cách manual không làm nổi | **Khi AI sai:**  <br> - Sai category → report sai → user hiểu sai tài chính  <br><br> **User biết sai khi:**  <br> - Tình cờ xem lại giao dịch / thấy bất hợp lý  <br><br> **User sửa:**  <br> - Vào transaction → sửa category (~3–4 bước)  <br><br> ❗ Vấn đề:  <br> - Không explain  <br> - Không alert  <br> - User thường không sửa → data degrade  <br><br> **4 paths UX:**  <br> - AI đúng: silent success  <br> - AI không chắc: vẫn auto classify  <br> - AI sai: khó phát hiện  <br> - Mất tin: không có fallback | **Architecture:** hybrid system  <br> - Rule-based (regex, keyword)  <br> - ML classifier (tabular / embedding)  <br> - Optional LLM cho parsing  <br><br> **Model cụ thể:**  <br> - Classification: Logistic Regression / LightGBM / XGBoost  <br> - Embedding: fastText / sentence-transformer  <br> - LLM (optional): GPT-4o mini / Llama 3 8B  <br><br> **Dependencies:**  <br> - Transaction DB (merchant, amount, time)  <br> - User history (label trước đó)  <br> - Keyword / note text  <br> - Mapping table (merchant → category)  <br><br> **Cost / request:**  <br> - Rule + ML: ~0.0001 – 0.001 USD  <br> - LLM parsing: ~0.0005 – 0.002 USD  <br><br> 👉 1M req/day ≈ 100 – 2000 USD/day  <br><br> **Latency:**  <br> - ML: <50ms  <br> - Rule: <100ms  <br> - LLM: 300ms – 1s  <br><br> **Risk:**  <br> - Data thiếu (ngoài MoMo)  <br> - Silent error → mất trust  <br> - Feedback loop yếu  <br> - LLM cost scale |

---

## ⚙️ Automation hay Augmentation?

☐ Automation  
☑ Augmentation — AI gợi ý, user quyết định cuối cùng  

**Justify:**  
- Sai mà user không biết → nguy hiểm (hiểu sai tài chính)  
- Quyết định tài chính là high-stakes  
👉 AI nên gợi ý + confirm, không auto hoàn toàn  

---

## 🔁 Learning Signal

| # | Câu hỏi | Trả lời |
|--|--------|--------|
| 1 | User correction đi vào đâu? | Khi user sửa category → lưu mapping (merchant / người nhận / keyword → category) |
| 2 | Product thu signal gì để biết tốt lên hay tệ đi? | - Tỷ lệ user sửa (correction rate)  <br> - Tỷ lệ auto classify đúng (proxy)  <br> - Engagement feature |
| 3 | Data thuộc loại nào? | ☑ User-specific  <br> ☑ Human-judgment  <br> ☑ Real-time  <br> ☐ Domain-specific  <br> ☐ Khác: — |

---

## 📊 Marginal Value

- Data có **marginal value cao** vì:
  - Hành vi chi tiêu mang tính cá nhân  
  - Model chung không biết trước  
- Nhưng:
  - Nếu user không sửa → không có learning signal  
  - Các sản phẩm khác cũng có thể thu data tương tự  

👉 Giá trị nằm ở **feedback loop (user → AI học)**  

