# 11-Git-Knownledge

# 11 câu hỏi phỏng vấn kinh khủng về Git sẽ khiến bạn phải bật khóc

Dựa theo 1 khảo sát nhà phát triển Stack Overflow gần đây, có hơn 70% nhà phát triển sử dụng Git, biến nó trở thành VCS được sử dụng nhiều nhất trên thế giới. Git được sử dụng phổ biến trong cả phát triển phần mềm  open-source cũng như thương mại, với những lợi ích to lớn cho những cá nhân, nhóm và các doanh nghiệp.

### Q1: Git fork là gì? Sự khác nhau giữa fork, branch và clone? (chủ đề : Git, độ khó 2 sao)

- 1 fork là 1 bản sao chép remote, phía server của 1 repository, khác biệt với bản gốc. 1 fork thực ra không phải là 1 khái niệm của Git, nó giống 1 ý tưởng cộng đồng/ xã hội hơn.
- 1 clone không phải là 1 fork, 1 clone là 1 bản sao chép trên local của 1 remote repo. Khi bạn clone, bạn thực ra chỉ đang sao chép toàn bộ mã nguồn repository, bao gồm taatts cả lịch sử và các nhánh.
- 1 branch là 1 kĩ thuật để xử lý các thay đổi trong cùng 1 repo để  cuối cùng gộp chúng vào phần code còn lại. 1 branch là 1 phần của 1 repo. Về khái niệm, nó đại diện cho 1 luồng phát triển.

### Q2: Sự khác biệt giữa 1 "pull request" và 1 "branch" là gì? 
- 1 branch chỉ là 1 phiên bản riêng biệt của code.
- 1 pull request là khi 1 ai đó lấy repo, tạo 1 nhánh riêng của họ, thực hiện 1 vài thay đổi, sau đó cố gắng merge nhánh đó vào (đưa những thay đổi của họ vào repo code của người khác)

### Q3: Sự khác biệt giữa "git pull" và "git fetch"?
 
- Khi bạn sử dụng lệnh pull, Git sẽ cố gắng tự động thực hiện công việc cho bạn. Nó còn phụ thuộc vào hoàn cảnh nữa, vì vậy Git sẽ gộp bất cứ pull commit nào vào nhánh và bạn đang làm việc. Lệnh pull sẽ tự động gộp các commit  mà không bắt bạn phải review nó trước. Nếu bạn không kiểm soát các nhánh của bạn 1 cách chặt chẽ, bạn sẽ thường xuyên gặp conflict.
- Khi bạn sử dụng lệnh fetch, Git sẽ gom bất cứ commit nào từ nhánh chỉ định mà không có trong branch hiện tại của bạn và lưu nó trong repo trên local của bạn. Tuy nhiên, nó sẽ không gộp chúng với branch hiện tại. Điều này  đặc biệt cần thiết khi bạn cần giữ repo của mình có code mới nhất, nhưng bạn lại đang làm 1 thứ gì đó mà có thể bị break khi bạn cập nhật các file của mình. Để tích hợp các commit vào nhánh master của mình, bạn có thể sử dụng lệnh merge

### Q4: Làm thế nào để revert về commit trước ở trong Git?
 Giả sử bạn có điều sau. Trong đó C là con trỏ HEAD của bạn và F là trạng thái các file của bạn.
 Để bỏ các thay đổi trong commit:
 git reset --hard HEAD~1
 Giờ B trở thành con trò HEAD của bạn. Vì bạn sử dụng --hard, tất cả các file của bạn sẽ trở về trạng  thái như ở commit B.
 Để quay lại commit những vẫn giữ các thay đổi của bạn:
  git reset HEAD~1
  Giờ chúng ta đã bảo Git chuyển con trỏ Head về commit B  và giữ nguyên các file  và git status sẽ hiện các thay đổi đã có ở C.
  Để quay lại commit những vẫn giữ các file và chỉ mục
  git reset --soft HEAD~1
  Khi bạn thực hiện git status bạn sẽ thây các file  cùng index như trước đó.
  
  ### Q5: "git cherry-pick" là gì?
  
  Câu lệnh cherry pick thường được sử dụng để đưa các commit cụ thể từ 1 nhánh  trong repo vào 1 nhánh khác. Nó thường được sử dụng để thực hiện các commit forward hoặc back port từ  1 nhánh bảo trì đến nhánh phát triển.
  
  Điều này trái ngược với  các cách khác như merge hay rebase  khi chỉ áp dụng 1 cách thông thường nhiều commit vào 1 nhánh khác.
  
  ### Q6: Giải thích lợi thế của Fork Workflow?
  
  Fork Workflow về cơ bản sẽ khác với các luồng làm việc Git khác. Thay vì sử dụng 1 repo đơn bên server như là 1 codebase trung tâm, nó cho phép mỗi người phát triển có repo bên server riêng của mình. Forking Workflow được thấy nhiều nhất trong các dự án opensource cộng đồng.
  
Lợi thế to lớn nhất của Forking Workflow là những người đóng góp có thể tích hợp mà không cần bất cứ ai để push lên 1 repo  trung tâm đơn lẻ, giúp cho việc có được 1 lịch sử dự án sạch đẹp. Các nhà phát triển sẽ push  lên các repo bên server của họ, và chỉ những người bảo trì dự án mới có thể push lên repo chính thức
  
  Khi các người phát triển sẵn sàng để  công bố các commit trên local, họ sẽ push các commit lên repo công khai của riêng họ - không phải cái chính thức. Sau đó họ sẽ gửi 1 pull request tới repo chính, để cho người bảo trì dự án biết có 1 cập nhật sẵn sàng được tích hợp.

### Q7: Sự khác nhau giữa, Head, working tree và index, trong Git?

  - Working tree/working directory/workspace là 1 cây thư mục của (mà nguồn) các file bạn thấy và chỉnh sửa
  - Vùng index/stagin là 1 file nhị phân, đơn lẻ, và lớn ở trong /.git/index, nó liệt kê tất cả các file bên trong nhánh hiện tại, mã sha1 checksums của chúng, mốc thời gian và tên file - nó không phải là 1 thư mục khác với các bản sao chép các file.
  - HEAD là 1 sự tương quan với commit cuối cùng trong nhánh được check out hiện tại.
  
  ### Q8: Bạn có thể giải thích Gitflow Workflow không?

Gitflow Workflow sử dụng 2 nhánh song song dài hạn để lưu lịch sử của dự án, là master và develop:
- Master: luôn luôn sẵn sàng để triển khai thực tế, với mọi thứ được test và  thừa nhận (sẵn sản cho product)
--Hotfix các nhánh bảo trì hay "hotfix" được sử dụng để  nhanh chóng vá lỗi cho triển khai product. Các nhánh hotfix rất giống với các nhánh triển khai và các nhánh tính năng ngoại trừ việc nó base trên master thay vì develop
- Develop là 1 nhánh mà tất cả các nhánh tính năng được gộp với nơi tất cả các test được thực hiện. Chỉ khi mọi thứ được kiểm tra kĩ lưỡng và sửa thì nó mới có thể được gộp vào master
-- Tính năng Mỗi tính năng mới nên ở trong nhánh riêng của nó, có thể được push lên nhánh develop như nhánh cha của chúng  

### Q9: Khi nào chúng ta nên sử dụng git stash?

Câu lệnh git stash sẽ lấy tất cả các thay đổi chưa được commit(cả stage và chưa stage),  lưu chúng ở 1 chỗ khác để sau sử dụng lại, và khôi phục chúng vào thư mục làm việc của bạn.

Chúng ta có thể sử dụng stash khi chúng ta phát hiện ra rằng chúng ta quên gì đó trong commit cuối và đ bắt đầu làm việc trên cái tiếp theo tại cùng 1 nhánh đó:
### Q10:  Làm cách nào để xóa 1 file khỏi git mà không phải xóa chúng trong hệ thống file của bạn?

Nếu bạn không cẩn thận trong quá trình sử dụng git add, bạn có thể thêm những file bạn không muốn commit. Tuy nhiên, git rm sẽ xóa nó khỏi cả vùng staging của bạn(index), cũng như hệ thống file của bạn (working tree), mà có thể bạn lại không muốn điều này.

Vậy thì thay vào đó sử dụng git reset:

Điều này có nghĩa là git reset <path> trái ngược với git add <path>

### Q11: Khi nào sử dụng git rebase thay vì git merge?

Both of these commands are designed to integrate changes from one branch into another branch - they just do it in very different ways.

Consider before merge/rebase:

Cả 2 câu lệnh được thiết kế để tích hợp các thay đổi từ 1 nhánh vào 1 nhánh khác - chỉ là chúng thực hiện theo các cách rất khác nhau thôi.

Cân nhắc trước khi merge/rebase:

sau khi git merge master

sau khi git rebase master

Với rebase có thể nói là bạn đang sử dụng 1 nhánh khác  như 1 base mới cho công việc của bạn:

Khi nào thì sử dụng:
1/ Nếu bạn không chắc chắn, sử dụng merge.
2/Lựa chọn merge hay rebase  tùy thuộc vào việc bạn muốn lịch sử trông như thế nào

### Các khía cạnh khác cần cân nhắc:
- Có hay không 1 nhánh bạn đang gặp các thay đổi do việc chia sẽ với những nhà phát triển bên ngoài team bạn ( opensource, public)? Nếu có, đừng rebase. Rebase sẽ phá hủy nhánh mà các nhà phát triển này sẽ có các repo hỏng/không nhất quán trừ khi họ sử dụng git pull --rebase.
- Kĩ năng của team phát triển của bạn thế nào? Rebase là 1 quá trình  mang tính phá hoại. Có nghĩa là, nếu bạn không áp dụng 1 cách chính xác, bạn có thể làm mất các commit công việc và/hoặc phá hủy sự nhất quán với các repo của các nhà phát triển khác.
- Nhánh có thể hiện thông tin hữu ích không? 1 vài team sử dụng  mô hình nhánh-cho-mỗi-chức-năng, khi đó mỗi nhánh đại diện cho 1 tính nawgs (hoặc sửa lỗi, tính năng phụ, vv). Trong mô hình này các nhánh giúp việc định danh tập các commit liên quan. Trong trờng hợp mô hình nhánh-cho-mỗi-nhà-phát-triển mỗi nhánh không có bất kỳ thông tin thêm nào (commit đã có tác giả của nó) Khi đó rebase sẽ không có vấn đề gì.
- Bạn có muốn phục hồi merge vì bất kỳ lý do nào không? Phục hồi ( làm lại) 1 rebase là 1 việc tương đối kho và/hay không thể so sánh để khôi phục 1 merge (nếu rebase có xung đột) Nếu bạn nghĩ có thể bạn muốn phục hồi lại thì sử dụng merge.




  
