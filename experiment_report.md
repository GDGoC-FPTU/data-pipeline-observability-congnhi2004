# Experiment Report: Data Quality Impact on AI Agent

**Student ID:** AI20K-2A202600505
**Name:** Nguyễn Trương Công Nhị
**Date:** 15/04/2026

---

## 1. Ket qua thi nghiem

Chay `agent_simulation.py` voi 2 bo du lieu va ghi lai ket qua:

| Scenario                          | Agent Response                                                   | Accuracy (1-10) | Notes         |
| --------------------------------- | ---------------------------------------------------------------- | --------------- | ------------- |
| Clean Data (`processed_data.csv`) | Based on my data, the best choice is Laptop at $1200.            | 10              | Giá cao nhất  |
| Garbage Data (`garbage_data.csv`) | Based on my data, the best choice is Nuclear Reactor at $999999. | 1               | Giá cao nhất  |

---

## 2. Phan tich & nhan xet

### Tai sao Agent tra loi sai khi dung Garbage Data?

(Viet nhan xet cua ban o day — it nhat 50 tu)
- Dựa vào code, tôi thấy được agent sẽ lọc các cate là electronics và chọn sản phẩm có giá cao nhất, và trong Garbage Data sản phẩm Nuclear Reactor thuộc cate là electronics nhưng bị lỗi giá 99999 nên Agent trả lời sai.
(Hay phan tich cac van de nhu Duplicate IDs, wrong data types, outliers, null values
va giai thich tai sao chung anh huong den ket qua cua Agent.)
- **Duplicate IDs**: ID trùng (id=1) làm mất tính duy nhất, dễ gây sai khi xử lý.
- **Sai kiểu dữ liệu**: `"ten dollars"` khiến cột `price` không còn là số, có thể gây lỗi hoặc so sánh sai khi tìm max.
- **Outliers**: giá `999999` của _Nuclear Reactor_ làm agent chọn sai vì logic = giá cao nhất.
- **Null values**: dòng thiếu `id` và `category` bị bỏ qua hoặc gây lỗi khi lọc.

---

## 3. Ket luan

**Quality Data > Quality Prompt?** (Dong y hay khong? Giai thich ngan gon.)

(Viet ket luan cua ban o day)
Dữ liệu chất lượng kém (sai kiểu, thiếu, outlier) sẽ làm agent suy luận sai dù prompt tốt. Prompt chỉ điều khiển cách xử lý, còn **dữ liệu quyết định đầu vào**. Nếu input sai → output chắc chắn sai.