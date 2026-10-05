\# Bài 4: Mô phỏng quy trình Hotfix và Gitflow



\## Thông tin sinh viên



\- Họ tên: Đoàn Trung Nguyên

\- Mã sinh viên: B24DTCN435

\- Lớp: HN-K24-CNTT4



\## 1. Bối cảnh



Nhánh main chứa phiên bản production v1.0.0.

Nhánh develop có tính năng dashboard đang phát triển, chưa thể release.



Lỗi được mô phỏng bằng cấu hình EXPOSE\_USER\_DATA=true trong security.conf.

Bản vá đổi cấu hình thành EXPOSE\_USER\_DATA=false.



Đây là bài thực hành Gitflow với dữ liệu mô phỏng, không phải ứng dụng

xử lý dữ liệu người dùng thực tế.



\## 2. Vai trò các nhánh



\- main: lưu phiên bản production.

\- develop: tích hợp các tính năng đang phát triển.

\- hotfix/v1.0.1: sửa lỗi khẩn cấp, được tạo trực tiếp từ main.



Hotfix tách từ main để không mang tính năng chưa hoàn thành trên develop

vào bản phát hành khẩn cấp.



\## 3. Quy trình thực hiện



1\. Tạo phiên bản đầu tiên trên main và gắn tag v1.0.0.

2\. Tạo develop, thêm file new-feature.txt mô phỏng tính năng đang làm dở.

3\. Chuyển về main và tạo hotfix/v1.0.1.

4\. Sửa security.conf để tắt việc lộ dữ liệu mô phỏng.

5\. Kiểm tra cấu hình và commit bản vá.

6\. Gộp hotfix vào main bằng git merge --no-ff.

7\. Tạo annotated tag v1.0.1 trên commit release của main.

8\. Gộp hotfix vào develop bằng git merge --no-ff.

9\. Kiểm tra develop chứa bản vá và vẫn giữ tính năng đang phát triển.

10\. Xóa nhánh hotfix cục bộ sau khi đã tích hợp vào cả hai nhánh.



\## 4. Các lệnh tích hợp chính



&#x20;   git switch main

&#x20;   git switch -c hotfix/v1.0.1



Sau khi sửa lỗi và commit:



&#x20;   git switch main

&#x20;   git merge --no-ff hotfix/v1.0.1 -m "merge: release hotfix v1.0.1"

&#x20;   git tag -a v1.0.1 -m "Release Hotfix 1.0.1"



Đồng bộ bản vá về develop:



&#x20;   git switch develop

&#x20;   git merge --no-ff hotfix/v1.0.1 -m "merge: sync hotfix v1.0.1 into develop"



Dọn nhánh:



&#x20;   git branch -d hotfix/v1.0.1



\## 5. Kết quả kiểm tra



\- main và develop đều chứa EXPOSE\_USER\_DATA=false.

\- main không chứa new-feature.txt.

\- develop vẫn chứa new-feature.txt.

\- Tag v1.0.1 trỏ vào commit release trên main.

\- Kiểm tra hotfix là tổ tiên của develop trả về mã thoát 0.

\- Nhánh hotfix cục bộ đã được xóa sau khi tích hợp.



Các lệnh kiểm tra:



&#x20;   git branch -a

&#x20;   git tag

&#x20;   git log --graph --oneline --all



\## 6. Đồ thị lịch sử



!\[Đồ thị Gitflow và Hotfix](gitflow-graph.png)



Ảnh được chụp sau khi hoàn tất hai lần merge, trước khi commit báo cáo.

Báo cáo và ảnh được bổ sung trên develop.



\## 7. Giải thích



Gộp hotfix vào main giúp phát hành bản sửa lỗi khẩn cấp mà không đưa

tính năng đang làm dở lên production.



Gộp cùng hotfix vào develop giúp các phiên bản tương lai giữ bản vá,

tránh đưa lỗi cũ trở lại.



Tùy chọn --no-ff tạo merge commit để thể hiện rõ các lần tích hợp.



Annotated tag v1.0.1 đánh dấu chính xác commit của bản phát hành hotfix.

