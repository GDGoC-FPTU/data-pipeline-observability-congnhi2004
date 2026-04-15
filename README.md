[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-2e0aaae1b6195c2367325f4f02e2d04e9abb55f0b24a779b69b11b9e10269abc.svg)](https://classroom.github.com/online_ide?assignment_repo_id=23573966&assignment_repo_type=AssignmentRepo)
# Day 10 Lab: Data Pipeline & Data Observability

**Student Email:** 26ai.nhintc@vinuni.edu.vn
**Name:** Nguyễn Trương Công Nhị

---

## Mo ta

Bài lab mô phỏng một agent đơn giản theo hướng RAG: đọc dữ liệu từ file CSV, lọc theo category electronics, sau đó chọn sản phẩm có giá cao nhất để trả lời. Tôi đã chạy thử với dữ liệu sạch để quan sát kết quả đúng, và với dữ liệu lỗi (garbage data) để phân tích sai lệch. Qua đó, tôi kiểm tra các vấn đề như trùng ID, sai kiểu dữ liệu, giá trị ngoại lai và giá trị thiếu, từ đó hiểu rõ cách chất lượng dữ liệu ảnh hưởng trực tiếp đến kết quả của agent.

---

## Cach chay (How to Run)

### Prerequisites
```bash
pip install pandas
```

### Chay ETL Pipeline
```bash
python solution.py
```

### Chay Agent Simulation (Stress Test)
```bash
# Chạy file Python để test agent với 2 loại dữ liệu
python agent_simulation.py

# Trong code đã có sẵn:
# - Test với CLEAN data (processed_data.csv)
# → Agent lọc electronics và trả kết quả hợp lý

# - Test với GARBAGE data (garbage_data.csv)
# → Agent vẫn chạy nhưng trả kết quả sai do dữ liệu lỗi
```

---

## Cau truc thu muc

```
├── solution.py              # ETL Pipeline script
├── processed_data.csv       # Output cua pipeline
├── experiment_report.md     # Bao cao thi nghiem
└── README.md                # File nay
```

---

## Ket qua

Tổng records đầu vào (garbage): 5
Records hợp lệ sau xử lý: 3 (Laptop, Chair, Monitor)
Records bị loại: 2
- 1 record do trùng ID (Banana)
- 1 record do sai kiểu dữ liệu (price = "ten dollars")
- 1 record do thiếu giá trị (Ghost Item) (có thể bị loại trong pipeline làm sạch)

→ Pipeline đã loại bỏ các dữ liệu lỗi và giữ lại 3 records sạch, đảm bảo agent hoạt động chính xác hơn.
