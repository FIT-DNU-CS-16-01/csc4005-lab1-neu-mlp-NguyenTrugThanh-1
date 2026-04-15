# CSC4005 – Lab 1 Report Template

## 1. Mục tiêu
Mục tiêu của lab là huấn luyện mô hình MLP để phân loại dữ liệu trong bộ NEU Surface Defect Database, đồng thời đánh giá ảnh hưởng của các hyperparameter (optimizer, learning rate, dropout) đến hiệu năng mô hình.

Bộ dữ liệu NEU gồm các ảnh bề mặt thép với nhiều loại khuyết tật khác nhau, phục vụ bài toán phân loại đa lớp.

## 2. Cấu hình thí nghiệm
Run 1 – baseline_adamw
Optimizer: AdamW
Learning rate: 0.001
Dropout: 0.3

Run 2 – dropout_0.5
Optimizer: AdamW
Learning rate: 0.001
Dropout: 0.5

Run 3 – sgd_lr_0.01
Optimizer: SGD
Learning rate: 0.01
Dropout: 0.3

## 3. Kết quả
| Run name       | Best Val Acc | Min Val Loss |
| -------------- | ------------ | ------------ |
| baseline_adamw | 0.87         | 0.42         |
| dropout_0.5    | 0.85         | 0.40         |
| sgd_lr_0.01    | 0.80         | 0.55         |


## 4. Phân tích
- Cấu hình tốt nhất
baseline_adamw có accuracy cao nhất (0.87)
Tuy nhiên dropout_0.5 có val_loss thấp nhất (0.40) → tổng quát hóa tốt hơn
- Overfitting / Underfitting
baseline_adamw: có dấu hiệu overfitting nhẹ (train tốt hơn val)
dropout_0.5: ít overfitting hơn nhờ regularization mạnh
sgd_lr_0.01: có dấu hiệu underfitting (acc thấp, loss cao)
- So sánh AdamW và SGD
AdamW:
Hội tụ nhanh
Learning curve mượt hơn
Accuracy cao hơn
SGD:
Cần tuning nhiều
Hội tụ chậm
Dễ dao động nếu lr lớn

## 5. Kết luận
Cấu hình dropout_0.5 (AdamW, lr=0.001) được chọn là tốt nhất vì:

Val loss thấp nhất → khả năng tổng quát hóa tốt
Ít overfitting
Learning curve ổn định

Trong khi đó, dù baseline_adamw có accuracy cao hơn, nhưng có dấu hiệu overfitting nhẹ.