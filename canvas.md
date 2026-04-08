# 🧠 AI Product Canvas — MoMo AI Financial Assistant

## 🎯 Canvas

| | Value | Trust | Feasibility |
|--|------|-------|------------|
| **Câu hỏi guide** | User nào? Pain gì? AI giải quyết gì mà cách hiện tại không giải được? | Khi AI sai thì user bị ảnh hưởng thế nào? User biết AI sai bằng cách nào? User sửa bằng cách nào? | Cost bao nhiêu/request? Latency bao lâu? Risk chính là gì? |
| **Trả lời** | **User:** Người dùng MoMo có nhu cầu quản lý chi tiêu cá nhân  <br><br> **Pain:**  <br> - Không nhớ mình tiêu tiền vào đâu  <br> - Ngại nhập chi tiêu thủ công  <br> - Không có insight rõ ràng  <br><br> **AI giải quyết:**  <br> - Tự động ghi chép giao dịch (auto log)  <br> - Tự động phân loại (auto classify)  <br> - Tổng hợp & báo cáo chi tiêu  <br><br> 👉 Khác biệt: giảm effort nhập liệu & tổng hợp mà cách manual không làm nổi | **Khi AI sai:**  <br> - Sai category → report sai → user hiểu sai tài chính  <br><br> **User biết sai khi:**  <br> - Tình cờ xem lại giao dịch / thấy bất hợp lý  <br><br> **User sửa:**  <br> - Vào transaction → sửa category (~3–4 bước)  <br><br> ❗ Vấn đề:  <br> - Không explain  <br> - Không alert  <br> - User thường không sửa → data degrade  <br><br> **4 paths UX:**  <br> - AI đúng: silent success (không confirm)  <br> - AI không chắc: vẫn auto classify, không hỏi  <br> - AI sai: user khó phát hiện, sửa có friction  <br> - Mất tin: không có fallback rõ ràng | **Cost:** ~0.0005 – 0.002 USD/lượt GPT-4o-mini  <br><br> **Latency:** rất thấp (<1s, real-time)  <br><br> **Risk:**  <br> - Data thiếu (ngoài MoMo không nhập)  <br> - Silent error → mất trust  <br> - User không feedback → model không cải thiện |

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

