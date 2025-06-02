# Hướng dẫn Git và GitHub cho Thành viên Mới

Chào mừng bạn đến với đội! Tài liệu này được thiết kế để giúp bạn nhanh chóng làm quen và sử dụng thành thạo Git cũng như GitHub theo quy trình làm việc chuẩn của chúng ta.

## Phần 1: Giới thiệu - Git là gì và Tại sao chúng ta sử dụng nó?

### Git là gì?
Git là một hệ thống quản lý phiên bản phân tán (Distributed Version Control System - DVCS) mạnh mẽ và phổ biến nhất hiện nay. Nó giúp chúng ta theo dõi mọi thay đổi trong mã nguồn của dự án theo thời gian. Hãy tưởng tượng Git như một "cỗ máy thời gian" cho code, cho phép bạn quay lại các phiên bản cũ hơn, xem ai đã thay đổi gì, khi nào, và tại sao.

### Tại sao chúng ta sử dụng Git?
Việc áp dụng Git mang lại nhiều lợi ích cốt lõi cho dự án của chúng ta:
* **Theo dõi lịch sử thay đổi:** Mọi thay đổi đều được ghi lại, giúp dễ dàng tìm ra lỗi hoặc hiểu rõ quá trình phát triển.
* **Làm việc nhóm hiệu quả:** Nhiều người có thể cùng làm việc trên một dự án mà không làm ảnh hưởng lẫn nhau, nhờ vào cơ chế nhánh (branching) và trộn (merging).
* **Khả năng phục hồi:** Dễ dàng khôi phục lại các phiên bản cũ nếu có sự cố xảy ra.
* **Phân nhánh linh hoạt:** Cho phép thử nghiệm các tính năng mới một cách độc lập mà không ảnh hưởng đến mã nguồn chính.
* **Hỗ trợ quy trình làm việc chuyên nghiệp:** Git là nền tảng cho các quy trình phát triển hiện đại như Git Flow, CI/CD.

### Git vs. GitHub
* **Git:** Là công cụ dòng lệnh (command-line tool) được cài đặt và chạy trên máy tính cá nhân của bạn. Nó thực hiện việc quản lý phiên bản.
* **GitHub:** Là một nền tảng dịch vụ dựa trên web (platform/service) cung cấp không gian lưu trữ từ xa (remote repositories) cho các dự án Git. Ngoài ra, GitHub còn cung cấp các công cụ hỗ trợ làm việc nhóm như Pull Requests, Issue Tracking, Code Review, Actions (CI/CD), v.v.

Nói một cách đơn giản, Git là công cụ, còn GitHub là nơi chúng ta lưu trữ và cộng tác trên các dự án sử dụng Git.

## Phần 2: Cài đặt và Cấu hình ban đầu

### Cài đặt Git
* **Windows:**
    1.  Truy cập [git-scm.com](https://git-scm.com/download/win) và tải về bộ cài đặt.
    2.  Chạy file cài đặt và làm theo các bước hướng dẫn (đa phần có thể để tùy chọn mặc định).
    3.  Sau khi cài đặt, mở Git Bash (hoặc Command Prompt/PowerShell) và gõ `git --version` để kiểm tra.
* **macOS:**
    * **Cách 1 (Khuyến nghị):** Cài đặt Homebrew (nếu chưa có) bằng cách chạy lệnh sau trong Terminal:
        ```bash
        /bin/bash -c "$(curl -fsSL [https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh](https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh))"
        ```
        Sau đó cài Git:
        ```bash
        brew install git
        ```
    * **Cách 2:** Git thường được cài đặt sẵn cùng với Xcode Command Line Tools. Thử gõ `git --version` trong Terminal. Nếu chưa có, hệ thống sẽ gợi ý bạn cài đặt Command Line Tools.
* **Linux (Debian/Ubuntu):**
    Mở Terminal và chạy lệnh:
    ```bash
    sudo apt update
    sudo apt install git
    ```
    Kiểm tra cài đặt: `git --version`.

### Cấu hình Git lần đầu
Sau khi cài đặt, bạn cần cấu hình thông tin cá nhân cho Git. Thông tin này sẽ được gắn với mỗi commit bạn tạo ra.
Mở Terminal (hoặc Git Bash) và chạy các lệnh sau, thay thế bằng thông tin của bạn:
```bash
git config --global user.name "Ten Cua Ban"
git config --global user.email "emailcuaban@example.com"

Bạn có thể kiểm tra lại cấu hình bằng lệnh:

git config --list

Thiết lập xác thực qua SSH với GitHub
Sử dụng SSH key giúp bạn kết nối và xác thực với GitHub mà không cần nhập username và password mỗi lần.

Kiểm tra SSH key hiện có:

ls -al ~/.ssh

Nếu bạn thấy các file như id_rsa.pub hoặc id_ed25519.pub thì bạn đã có key. Nếu không, hãy tạo mới.

Tạo SSH key mới (nếu chưa có):
Sử dụng thuật toán Ed25519 (khuyến nghị):

ssh-keygen -t ed25519 -C "emailcuaban@example.com"

Hoặc RSA:

ssh-keygen -t rsa -b 4096 -C "emailcuaban@example.com"

Khi được hỏi "Enter a file in which to save the key", nhấn Enter để chấp nhận vị trí mặc định.
Khi được hỏi "Enter passphrase", bạn có thể nhập một mật khẩu để bảo vệ key hoặc để trống (không khuyến nghị cho bảo mật cao).

Thêm SSH key vào ssh-agent:

eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519 # Hoặc ~/.ssh/id_rsa nếu bạn dùng RSA

Thêm SSH key vào tài khoản GitHub của bạn:
a.  Sao chép nội dung public key của bạn. Ví dụ với Ed25519:
bash cat ~/.ssh/id_ed25519.pub 
(Trên Windows, bạn có thể dùng clip < ~/.ssh/id_ed25519.pub trong Git Bash để copy).
b.  Truy cập GitHub, vào Settings (góc trên bên phải, click vào avatar của bạn).
c.  Trong menu bên trái, chọn SSH and GPG keys.
d.  Click New SSH key hoặc Add SSH key.
e.  Đặt một Title dễ nhớ cho key (ví dụ: "My Laptop").
f.  Dán nội dung public key đã sao chép vào ô Key.
g.  Click Add SSH key.

Kiểm tra kết nối:

ssh -T git@github.com

Bạn có thể thấy một cảnh báo về authenticity of host. Gõ yes. Nếu thành công, bạn sẽ thấy thông báo: "Hi username! You've successfully authenticated, but GitHub does not provide shell access."

Phần 3: Các khái niệm Git cốt lõi
Repository (Kho chứa - Repo): Là nơi lưu trữ toàn bộ mã nguồn và lịch sử thay đổi của dự án. Có hai loại:

Local Repository: Bản sao của kho chứa trên máy tính cá nhân của bạn.

Remote Repository: Bản sao của kho chứa được lưu trữ trên một server từ xa (ví dụ: GitHub).

Commit (Phiên bản lưu): Một "ảnh chụp" (snapshot) các thay đổi của bạn tại một thời điểm nhất định. Mỗi commit có một mã định danh duy nhất (SHA-1 hash) và một thông điệp mô tả những thay đổi đó.

Branch (Nhánh): Một dòng phát triển độc lập. Nhánh cho phép bạn làm việc trên các tính năng hoặc sửa lỗi mà không ảnh hưởng đến mã nguồn chính. Nhánh mặc định thường là main hoặc master.

Merge (Trộn nhánh): Hành động gộp các thay đổi từ một nhánh này sang một nhánh khác.

Pull Request (PR) (Yêu cầu kéo - trên GitHub): Một đề xuất chính thức để merge các thay đổi từ một nhánh (thường là nhánh feature) vào một nhánh khác (thường là develop hoặc main). PR là nơi diễn ra quá trình code review và thảo luận trước khi merge.

Remote (Kho chứa từ xa): Một tham chiếu đến repository trên server (ví dụ: origin thường là tên mặc định cho remote trỏ đến GitHub).

HEAD: Con trỏ trỏ đến commit hiện tại trong nhánh hiện tại. Thường thì HEAD trỏ đến commit mới nhất của nhánh bạn đang làm việc.

Staging Area (Index): Khu vực chuẩn bị. Trước khi commit, bạn cần add các thay đổi vào Staging Area. Chỉ những thay đổi trong Staging Area mới được đưa vào commit tiếp theo.

Phần 4: Mô hình Phân nhánh (Branching Model - Git Flow)
Đây là xương sống của quy trình làm việc với Git trong team của chúng ta. Git Flow giúp quản lý dự án một cách có tổ chức, đặc biệt hữu ích cho các dự án có nhiều phiên bản và cần sự ổn định.

Sơ đồ tổng quan:

main (master) ----o----o----o----o----o----o (tags: v1.0, v1.1, v2.0)
 \              /    / \    / \  /
  \            /    /   \  /   \/
   develop ---o----o----o----o----o----o----o
       |    / | \  /      |  / | \  /
       |   /  |  \/        | /  |  \/
       |  /   |  /\        |/   |  /\
feature/* | release/* hotfix/*

1. main (hoặc master)
Mục đích: Chứa mã nguồn đã được phát hành (production-ready), ổn định và sẵn sàng cho môi trường production. Mỗi commit trên main phải phản ánh một phiên bản đã được phát hành ra ngoài.

Quy tắc:

KHÔNG BAO GIỜ commit trực tiếp lên nhánh main.

Chỉ được merge code vào main từ các nhánh release/* (sau khi đã hoàn tất quá trình chuẩn bị release) hoặc hotfix/* (để vá lỗi khẩn cấp trên production).

Mỗi commit trên main phải được đánh dấu bằng một tag (ví dụ: v1.0.0, v1.0.1). Tag này đại diện cho một phiên bản cụ thể của sản phẩm.

2. develop
Mục đích: Nhánh tích hợp chính cho các tính năng mới. Nó chứa code của phiên bản sắp phát hành (next release). Đây là nhánh mà các thay đổi từ các nhánh feature/* được gộp vào.

Quy tắc:

Tất cả các nhánh feature/* phải được merge vào develop (thông qua Pull Request).

Khi develop đã tích lũy đủ các tính năng cần thiết cho một phiên bản mới và được coi là tương đối ổn định (sau khi qua các bước QA cơ bản), một nhánh release/* sẽ được tạo ra từ develop.

Nhánh này có thể không ổn định trong quá trình phát triển tích cực, vì vậy không nên triển khai trực tiếp từ develop lên production.

3. feature/*
Mục đích: Dùng để phát triển các tính năng mới (new features) hoặc các cải tiến (enhancements). Mỗi tính năng nên được phát triển trên một nhánh feature riêng biệt.

Quy tắc:

Luôn được tạo ra (branched off) từ nhánh develop.

Sau khi hoàn thành và được review, sẽ được merge trở lại vào develop thông qua một Pull Request.

Không bao giờ tương tác trực tiếp với main.

Nên được xóa sau khi đã merge thành công vào develop.

Quy tắc đặt tên: feature/ten-tinh-nang-ngan-gon (ví dụ: feature/user-authentication, feature/shopping-cart-api). Sử dụng dấu gạch ngang - để ngăn cách các từ, viết thường, không dấu.

4. release/*
Mục đích: Chuẩn bị cho một phiên bản phát hành mới (new production release). Nhánh này cho phép tách biệt quá trình chuẩn bị release khỏi nhánh develop, nơi các tính năng mới cho phiên bản sau nữa có thể vẫn đang được tích hợp.

Công việc trên nhánh release/*:

Sửa các bug nhỏ cuối cùng (minor bug fixes).

Chuẩn bị metadata cho release (ví dụ: cập nhật số phiên bản, tài liệu hướng dẫn, changelog).

Thực hiện các bước kiểm thử cuối cùng (final QA, UAT).

Quy tắc:

Được tạo ra từ develop khi develop đã có đủ tính năng cho phiên bản tiếp theo và được coi là "feature complete".

Không thêm tính năng mới vào nhánh release/*. Chỉ tập trung vào việc ổn định hóa phiên bản.

Sau khi hoàn tất và sẵn sàng để phát hành:

Merge nhánh release/* vào main.

Tag commit trên main với số phiên bản tương ứng (ví dụ: v1.1.0).

Merge nhánh release/* trở lại vào develop để đảm bảo các bản vá lỗi hoặc thay đổi nhỏ trên nhánh release cũng có mặt trên develop (tránh regression).

Xóa nhánh release/* sau khi đã merge vào cả main và develop.

Quy tắc đặt tên: release/vX.Y.Z (ví dụ: release/v1.2.0).

5. hotfix/*
Mục đích: Sửa các lỗi nghiêm trọng (critical bugs) trên môi trường production một cách nhanh chóng mà không cần phải chờ đợi chu kỳ release thông thường.

Quy tắc:

Luôn được tạo ra (branched off) từ nhánh main (cụ thể là từ tag của phiên bản đang bị lỗi).

Chỉ chứa các commit sửa lỗi khẩn cấp đó.

Sau khi sửa xong và được kiểm thử:

Merge nhánh hotfix/* vào main.

Tag commit trên main với số phiên bản vá lỗi mới (ví dụ: v1.0.1 nếu lỗi xảy ra trên v1.0.0).

Merge nhánh hotfix/* trở lại vào develop để đảm bảo lỗi này cũng được sửa trong các phiên bản phát triển tiếp theo. Nếu đang có nhánh release/* hoạt động, hotfix cũng cần được merge vào nhánh release/* đó.

Xóa nhánh hotfix/* sau khi đã merge.

Quy tắc đặt tên: hotfix/ten-loi-ngan-gon hoặc hotfix/vX.Y.Z-issue-description (ví dụ: hotfix/login-critical-error, hotfix/v1.0.1-payment-gateway-fix).

Phần 5: Quy trình làm việc chuẩn (Phát triển tính năng với Git Flow)
Đây là "use case" điển hình khi bạn phát triển một tính năng mới:

Đồng bộ hóa develop với remote mới nhất:
Đảm bảo nhánh develop cục bộ của bạn được cập nhật với những thay đổi mới nhất từ server.

git checkout develop
git pull origin develop

Tạo nhánh tính năng mới:
Tạo một nhánh mới từ develop cho tính năng bạn sắp làm. Đặt tên theo quy ước feature/ten-tinh-nang.

git checkout -b feature/user-profile-page develop
# Lệnh trên tương đương với:
# git branch feature/user-profile-page develop
# git checkout feature/user-profile-page

Lúc này, bạn đang ở trên nhánh feature/user-profile-page.

Làm việc và Commit các thay đổi:
Thực hiện code cho tính năng mới. Sau mỗi thay đổi logic hoặc hoàn thành một phần nhỏ, hãy commit code.

Kiểm tra trạng thái các file:

git status

Thêm các file đã thay đổi vào Staging Area:

git add .  # Thêm tất cả các file thay đổi trong thư mục hiện tại và con của nó
# Hoặc thêm từng file cụ thể:
# git add path/to/your/file.js
# git add path/to/another/file.html

Commit các thay đổi đã được add:

git commit -m "Feat: Implement user profile display"
# Xem Phần 8 để biết quy tắc viết commit message

Lặp lại bước add và commit nhiều lần trong quá trình phát triển tính năng. Nên commit thường xuyên, mỗi commit nên nhỏ và tập trung vào một thay đổi logic.

Đẩy nhánh tính năng lên GitHub:
Khi bạn muốn chia sẻ nhánh của mình với người khác, hoặc khi bạn đã có một số commit và muốn sao lưu lên remote, hoặc khi chuẩn bị tạo Pull Request:

git push -u origin feature/user-profile-page

-u (hoặc --set-upstream) sẽ thiết lập nhánh feature/user-profile-page ở local theo dõi nhánh cùng tên trên origin. Lần sau bạn chỉ cần git push.

Tạo Pull Request (PR):
Khi tính năng đã hoàn thành (hoặc bạn muốn nhận phản hồi sớm), hãy tạo một Pull Request trên GitHub.
a.  Truy cập repository của dự án trên GitHub.
b.  GitHub thường sẽ tự động phát hiện nhánh mới được push và hiển thị một nút "Compare & pull request" cho nhánh feature/user-profile-page của bạn. Click vào đó.
c.  Nếu không thấy, bạn có thể vào tab "Pull requests" và click "New pull request".
d.  Quan trọng:
* Chọn base branch là develop.
* Chọn compare branch là nhánh feature/user-profile-page của bạn.
e.  Viết tiêu đề và mô tả chi tiết cho PR (xem Phần 8).
f.  Gán reviewer (nếu cần), thêm labels, milestones.
g.  Click "Create pull request".

Review và Merge:

Các thành viên khác trong team (hoặc Tech Lead) sẽ review code của bạn trong PR.

Họ có thể để lại comment, đặt câu hỏi, hoặc yêu cầu thay đổi.

Bạn cần thảo luận và thực hiện các thay đổi cần thiết (commit thêm vào nhánh feature của bạn và push lên, PR sẽ tự động cập nhật).

Khi PR đã được duyệt (approved) và các kiểm tra tự động (CI) đã pass (xem Phần 6), người có quyền sẽ merge PR đó vào nhánh develop.

Thường thì GitHub cung cấp nút "Merge pull request". Chọn phương thức merge phù hợp (thường là "Squash and merge" hoặc "Create a merge commit"). Team sẽ có quy định cụ thể về việc này.

Dọn dẹp (Xóa nhánh feature):
Sau khi PR đã được merge thành công vào develop, nhánh feature/user-profile-page không còn cần thiết nữa.

Xóa nhánh trên remote (GitHub): GitHub thường có nút "Delete branch" sau khi merge.

Xóa nhánh ở local:

git checkout develop      # Chuyển về nhánh develop
git pull origin develop   # Cập nhật develop với thay đổi vừa merge
git branch -d feature/user-profile-page # Xóa nhánh feature ở local

Nếu Git báo lỗi nhánh chưa được merge hoàn toàn (dù đã merge trên GitHub), bạn có thể dùng -D để ép xóa: git branch -D feature/user-profile-page.

Phần 6: Giới thiệu về Tích hợp và Triển khai Liên tục (CI/CD)
CI/CD là một tập hợp các thực hành tự động hóa quy trình xây dựng, kiểm thử và triển khai phần mềm. Với mô hình Git Flow của chúng ta, CI/CD hoạt động như sau:

CI (Continuous Integration - Tích hợp liên tục)
Kích hoạt:

Khi một Pull Request được tạo mới nhắm vào nhánh develop.

Khi có một commit mới được push lên một nhánh đang có Pull Request mở nhắm vào develop.

Hành động:

Hệ thống CI (ví dụ: GitHub Actions, Jenkins, GitLab CI) sẽ tự động lấy mã nguồn mới nhất từ PR.

Chạy các lệnh build (ví dụ: npm install, npm run build).

Chạy các bộ kiểm thử tự động (automated tests) như:

Unit Tests: Kiểm tra từng đơn vị code nhỏ (hàm, class) một cách độc lập.

Integration Tests: Kiểm tra sự tương tác giữa các thành phần khác nhau của hệ thống.

(Có thể có cả Linting, Code Style checks, Security scans).

Kết quả:

PR trên GitHub sẽ hiển thị trạng thái của các kiểm tra CI: "pass" (thành công) hoặc "fail" (thất bại).

Chỉ những PR có trạng thái CI "pass" mới được phép merge vào develop. Điều này đảm bảo rằng code mới không làm hỏng các tính năng hiện có hoặc vi phạm các tiêu chuẩn chất lượng.

CD (Continuous Delivery/Deployment - Chuyển giao/Triển khai liên tục)
Continuous Delivery (Chuyển giao liên tục):

Kích hoạt: Khi một commit mới được merge vào nhánh main (thường là từ việc merge một nhánh release/* hoặc hotfix/*).

Hành động:

Hệ thống tự động build phiên bản production của ứng dụng.

Đóng gói ứng dụng (ví dụ: tạo Docker image, file .zip).

Tự động triển khai phiên bản mới lên môi trường Staging (hoặc UAT).

Trên môi trường Staging, có thể chạy thêm các kiểm thử chấp nhận (acceptance tests) hoặc thực hiện kiểm thử thủ công cuối cùng.

Sau khi được xác nhận trên Staging, việc triển khai lên Production có thể là một bước thủ công (click một nút) hoặc cũng có thể tự động.

Continuous Deployment (Triển khai liên tục):

Tương tự như Continuous Delivery, nhưng bước triển khai lên Production cũng được tự động hóa hoàn toàn sau khi tất cả các kiểm thử ở các giai đoạn trước đã pass.

Mục đích:

Giảm thiểu sai sót do con người trong quá trình triển khai.

Tăng tốc độ phát hành sản phẩm và đưa giá trị đến người dùng nhanh hơn.

Đảm bảo mỗi thay đổi trên main đều có thể được phát hành một cách an toàn và nhanh chóng.

Phần 7: Các tình huống và lệnh hữu ích khác
Cập nhật nhánh feature với develop mới nhất
Trong quá trình bạn làm việc trên nhánh feature/my-cool-feature, nhánh develop có thể đã được cập nhật bởi các thành viên khác. Để đảm bảo nhánh feature của bạn có những thay đổi mới nhất từ develop (giúp giảm thiểu merge conflict sau này):

# 1. Đảm bảo bạn đang ở trên nhánh feature của mình
git checkout feature/my-cool-feature

# 2. Lấy về những thay đổi mới nhất từ remote (nhưng chưa merge)
git fetch origin

# 3. Rebase nhánh feature của bạn lên trên develop mới nhất
git rebase origin/develop
# Hoặc nếu bạn muốn merge thay vì rebase:
# git merge origin/develop

# Nếu có conflict, giải quyết conflict (xem phần dưới) rồi tiếp tục rebase:
# git add <file-da-sua-conflict>
# git rebase --continue
# Hoặc nếu muốn hủy rebase: git rebase --abort

# 4. Push lại nhánh feature (có thể cần --force-with-lease nếu đã rebase)
git push origin feature/my-cool-feature --force-with-lease
# Cẩn thận khi dùng --force hoặc --force-with-lease nếu có người khác cùng làm trên nhánh này.

Rebase vs Merge khi cập nhật nhánh feature:

Rebase: Viết lại lịch sử commit của nhánh feature, đặt các commit của bạn lên "đỉnh" của develop mới nhất. Giúp lịch sử commit trên develop (sau khi merge) thẳng và sạch hơn.

Merge: Tạo một merge commit mới để gộp develop vào nhánh feature của bạn. Giữ nguyên lịch sử, nhưng có thể làm lịch sử phức tạp hơn.
Team có thể có quy định cụ thể về việc này. Thường thì rebase được ưu tiên cho các nhánh feature cá nhân trước khi tạo PR.

Cách giải quyết Merge Conflict
Khi Git không thể tự động gộp các thay đổi từ hai nhánh (ví dụ, khi cả hai nhánh cùng sửa một dòng code theo những cách khác nhau), Merge Conflict sẽ xảy ra.

Git sẽ thông báo cho bạn biết file nào bị conflict. Ví dụ, sau lệnh git merge develop hoặc git rebase develop:

Auto-merging path/to/your/file.js
CONFLICT (content): Merge conflict in path/to/your/file.js
Automatic merge failed; fix conflicts and then commit the result.

Mở file bị conflict trong editor. Bạn sẽ thấy các dấu hiệu như:

<<<<<<< HEAD (hoặc tên nhánh của bạn)
// Code của bạn ở nhánh hiện tại
your changes
=======
// Code từ nhánh đang merge vào
changes from the other branch
>>>>>>> develop (hoặc tên nhánh kia)

Quyết định cách giải quyết:

Giữ lại code của bạn.

Giữ lại code từ nhánh kia.

Kết hợp cả hai (chỉnh sửa thủ công).

Viết lại hoàn toàn phần đó.
Xóa các dấu <<<<<<<, =======, >>>>>>> và phần code không mong muốn, chỉ để lại phần code cuối cùng bạn muốn.

Sau khi đã sửa tất cả các conflict trong file:

git add path/to/your/file.js # Đánh dấu conflict đã được giải quyết

Lặp lại cho tất cả các file bị conflict.

Hoàn tất quá trình merge/rebase:

Nếu bạn đang merge:

git commit # Git sẽ tự tạo một commit message, bạn có thể sửa nếu muốn

Nếu bạn đang rebase:

git rebase --continue

Nếu muốn hủy bỏ việc giải quyết conflict và quay lại trạng thái trước khi merge/rebase:

Khi merge: git merge --abort

Khi rebase: git rebase --abort

Hoàn tác commit (git revert)
Nếu bạn muốn hoàn tác một commit đã được push lên remote mà không làm thay đổi lịch sử (an toàn hơn git reset --hard cho các commit đã chia sẻ):

git revert <commit-SHA-can-hoan-tac>

Lệnh này sẽ tạo ra một commit mới đối nghịch lại với commit bạn muốn hoàn tác. Sau đó push commit mới này lên:

git push origin your-branch-name

Xem lịch sử git log
Lệnh git log có rất nhiều tùy chọn để xem lịch sử commit:

Xem lịch sử commit cơ bản:

git log

Xem lịch sử commit một cách gọn gàng hơn (mỗi commit một dòng):

git log --oneline

Xem lịch sử commit kèm theo biểu đồ nhánh:

git log --graph --oneline --decorate --all

Xem lịch sử commit của một file cụ thể:

git log path/to/your/file.js

Xem thay đổi (diff) của một commit cụ thể:

git show <commit-SHA>

Phần 8: Quy tắc Vàng và Best Practices
Quy tắc viết Commit Message chuyên nghiệp
Một commit message tốt giúp người khác (và chính bạn trong tương lai) hiểu rõ mục đích của commit đó. Chúng ta tuân theo quy ước Conventional Commits.
Cấu trúc chung:

<type>[optional scope]: <description>

[optional body]

[optional footer(s)]

Type (Loại):

feat: Một tính năng mới (tương ứng với MINOR trong semantic versioning).

fix: Sửa một bug (tương ứng với PATCH trong semantic versioning).

docs: Chỉ thay đổi tài liệu.

style: Thay đổi không ảnh hưởng đến ý nghĩa code (dấu chấm phẩy, thụt lề, etc).

refactor: Viết lại code mà không sửa bug hay thêm tính năng mới.

perf: Cải thiện hiệu năng.

test: Thêm hoặc sửa test.

build: Thay đổi ảnh hưởng đến hệ thống build hoặc dependencies bên ngoài (ví dụ: gulp, npm).

ci: Thay đổi file cấu hình CI hoặc script (ví dụ: GitHub Actions).

chore: Các thay đổi không liên quan đến source code hay test (ví dụ: cập nhật .gitignore).

revert: Hoàn tác một commit trước đó.

Scope (Phạm vi - tùy chọn): Chỉ rõ phần nào của codebase bị ảnh hưởng (ví dụ: feat(api): ..., fix(parser): ...).

Description (Mô tả):

Ngắn gọn, súc tích, viết ở thì hiện tại, dạng mệnh lệnh (ví dụ: "Add login page" thay vì "Added login page" hoặc "Adds login page").

Không viết hoa chữ cái đầu (trừ khi là tên riêng).

Không có dấu chấm ở cuối.

Body (Nội dung - tùy chọn):

Giải thích chi tiết hơn về commit nếu cần.

Nêu rõ LÝ DO thay đổi, không chỉ là CÁI GÌ thay đổi.

Cách dòng tiêu đề một dòng trống.

Footer (Chân trang - tùy chọn):

Chứa thông tin về Breaking Changes (thay đổi gây mất tương thích ngược): BREAKING CHANGE: ...

Tham chiếu đến Issues (ví dụ: Closes #123, Fixes #456).

Ví dụ commit message tốt:

feat: Add user authentication endpoint

Implement POST /api/login endpoint for user authentication.
Uses JWT for token generation.

Fixes #42

fix(ui): Correct button alignment on settings page

The save button was previously misaligned on smaller screens.
This commit adjusts the CSS flex properties to ensure proper alignment.


### Quy tắc tạo Pull Request (PR) chi tiết, rõ ràng
Một PR tốt giúp quá trình review code diễn ra nhanh chóng và hiệu quả.
* **Tiêu đề PR:**
    * Rõ ràng, súc tích, phản ánh nội dung chính của PR.
    * Có thể theo format tương tự commit message (ví dụ: `feat: User Profile Page`).
    * Nếu PR giải quyết một issue cụ thể, có thể thêm ID của issue vào tiêu đề (ví dụ: `feat: User Profile Page (closes #123)`).
* **Mô tả PR:**
    * **Mục đích của PR là gì?** (What)
    * **Tại sao cần thay đổi này?** (Why) - Liên kết đến issue, user story, hoặc giải thích bối cảnh.
    * **Thay đổi được thực hiện như thế nào?** (How) - Tóm tắt các thay đổi chính, các quyết định thiết kế quan trọng.
    * **Cách kiểm thử?** (How to test) - Các bước để reviewer có thể kiểm tra tính năng/sửa lỗi.
    * **Ảnh chụp màn hình/GIF (nếu có thay đổi UI):** Rất hữu ích để reviewer hình dung được thay đổi.
    * **Đánh dấu "Work In Progress" (WIP):** Nếu PR chưa sẵn sàng để merge nhưng bạn muốn nhận phản hồi sớm, hãy thêm `[WIP]` hoặc `Draft` vào tiêu đề PR.
    * **Liên kết đến các Issue liên quan:** Sử dụng từ khóa như `closes #<issue_number>`, `fixes #<issue_number>`, `relates to #<issue_number>`.
    * **Chia nhỏ PR:** Nếu một tính năng quá lớn, hãy cân nhắc chia thành nhiều PR nhỏ hơn, dễ review hơn. Mỗi PR nên tập trung vào một mục tiêu cụ thể.
    * **Tự review trước khi yêu cầu người khác review:** Kiểm tra lại code của mình, xóa debug code, đảm bảo code sạch sẽ.

---

Chúc bạn làm việc hiệu quả với Git và GitHub! Nếu có bất kỳ câu hỏi nào, đừng ngần ngại hỏi Tech Lead hoặc các thành viên khác trong team.
