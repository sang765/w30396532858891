# Hướng dẫn đóng góp

> 🇬🇧 [English](README.md) · [README tiếng Việt](README.vi.md)

Tài liệu này viết cho người **chưa từng dùng Git**. Làm theo từng bước là chạy được,
không cần hiểu hết lý thuyết.

---

## 0. Git là gì? (đọc 30 giây)

- **Repo** = một bản chụp toàn bộ thư mục map, kèm lịch sử các bản chụp trước đó.
- **Commit** = chụp một lần. Bạn tự đặt tên cho bản chụp.
- **Push** = đưa bản chụp mới nhất lên GitHub để mọi người thấy.
- **Clone** = tải toàn bộ repo (gồm cả lịch sử) về máy.

Bạn không cần nhớ lý thuyết — chỉ cần nhớ đúng 5 lệnh ở mục 3.

---

## 1. Chuẩn bị (chỉ làm 1 lần)

1. Cài **Git**: <https://git-scm.com/downloads>
2. Tạo tài khoản **GitHub**: <https://github.com/signup>
3. Cài **GitHub Desktop** (khuyến nghị cho người mới): <https://desktop.github.com>
   - Giao diện bấm chuột, không cần gõ lệnh.
   - Có thể thay bằng **Git Bash** (đi kèm khi cài Git trên Windows) nếu bạn thích gõ lệnh.

---

## 2. Tải map về máy (chỉ làm 1 lần)

**Bằng GitHub Desktop**

1. Mở GitHub Desktop → `File` → `Clone repository…`
2. Chọn tab `URL`, dán `https://github.com/sang765/w30396532858891.git`
3. Chọn nơi lưu, bấm `Clone`.

**Bằng lệnh**

```bash
git clone https://github.com/sang765/w30396532858891.git
cd w30396532858891
```

Sau bước này bạn có một thư mục trên máy — đó là nơi bạn sẽ copy map vào.

> [!WARNING]
> Trong thư mục vừa clone có một thư mục ẩn tên là `.git`. **Đừng xóa, đừng đổi tên,
> đừng copy đè lên nó.** Nếu mất `.git` thì repo thành một thư mục thường, không push lên đâu được nữa.

---

## 3. Quy trình cập nhật map (mỗi lần cập nhật)

### Bước 1 — Lưu map trong game

Vào map, chỉnh sửa/chơi xong, **thoát hẳn khỏi map** (đừng chỉ alt-tab ra).
Game chỉ ghi file ra đĩa khi bạn thoát, nên nếu copy sớm thì sẽ lấy nhầm bản cũ.

### Bước 2 — Copy file map vào thư mục clone

Tìm thư mục map trên máy — tên của nó trùng với tên repo
(`w30396532858891`). Nếu chưa biết đường dẫn, hỏi trong nhóm: Android / iOS / PC
mỗi nền tảng một chỗ khác nhau.

Copy **nội dung** thư mục map đè vào thư mục bạn vừa clone, tức là copy đè lên
`m0/`, `sandbox/`, `ss/`, `visualcode/`, `wdesc.fb`… của bản clone.

- ✅ **Được phép:** đè các thư mục `m0/`, `ss/`, `visualcode/`… và file `*.fb`
- ❌ **Không được:** xóa hết thư mục clone rồi mới copy vào
- ❌ **Không được:** đè mất `.git/`, `README.md`, `README.vi.md`, `CONTRIBUTING.md`, `.gitignore`

Cách an toàn nhất: chọn tất cả trong thư mục map → copy → paste vào thư mục clone →
bấm **Ghi đè** khi Windows/Hệ điều hành hỏi. Đừng dùng chế độ "xóa rồi copy".

### Bước 3 — Kiểm tra trước khi commit

```bash
git status
```

Đọc kết quả:

- `Changes not staged for commit:` — danh sách file đã thay đổi. Xem qua, nếu có
  file lạ (file `.log`, thư mục tạm…) thì **đừng add**, báo lại cho người quản lý.
- `Untracked files:` — file mới xuất hiện. Nếu đó là file bạn thật sự thêm thì OK.
- Không có file rác nào → tiếp tục.

### Bước 4 — Chụp lại (commit)

```bash
git add -A
git commit -m "cập nhật: mô tả ngắn những gì bạn vừa đổi"
```

Ví dụ tên commit tốt:

- `cập nhật: thêm khu Zoo và 2 lệnh mới /antivoid, /tree`
- `sửa: sửa trigger teleport về hub`
- `dọn: xóa file tạm do game tạo ra`

### Bước 5 — Đẩy lên GitHub (push)

```bash
git push origin main
```

**Bằng GitHub Desktop** (thay cho bước 3–5):

1. Mở GitHub Desktop → tab `Changes` → xem danh sách file, viết `Summary`.
2. Bấm `Commit to main`.
3. Bấm `Push origin` (góc dưới trái).

Xong. Vào trang repo trên GitHub để kiểm tra file của bạn đã có mặt.

---

## 4. Nếu bạn không có quyền push thẳng vào repo

Nếu `git push` báo `Permission denied` / `403`, nghĩa là bạn chưa được thêm làm
collaborator. Dùng **Fork**:

```bash
# 1. Fork repo trên GitHub: bấm nút Fork, chọn tài khoản của bạn

# 2. Clone BẢN FORK của bạn (lưu ý: URL của BẠN, không phải của người khác)
git clone https://github.com/<ten-ban>/w30396532858891.git
cd w30396532858891

# 3. Nối về repo gốc để lấy bản mới nhất
git remote add upstream https://github.com/sang765/w30396532858891.git
git fetch upstream
git rebase upstream/main

# 4. Copy map vào, rồi add / commit / push như bình thường
git add -A
git commit -m "cập nhật: ..."
git push origin main

# 5. Vào GitHub → repo của bạn → bấm "Compare & pull request"
```

Nếu trùng tên với `main` thì cần thêm một nhánh trước khi commit:

```bash
git checkout -b sua-<ten-branch>
# ... copy map, add, commit, push
git push -u origin sua-<ten-branch>
```

---

## 5. Xử lý sự cố thường gặp

### `git push` báo `non-fast-forward` / `rejected`

Có người đã push trước bạn. Cứ kéo bản mới nhất rồi push lại:

```bash
git pull --rebase origin main
git push origin main
```

### Báo `CONFLICT` sau khi pull

Git không tự quyết được file nào thắng. Mở file bị báo lỗi, tìm hai dòng đánh dấu:

```
<<<<<<< HEAD
bản của người khác
=======
bản của bạn
>>>>>>> xxx
```

Giữ lại phần đúng, **xóa hẳn** ba dòng `<<<<<<<`, `=======`, `>>>>>>>`, rồi:

```bash
git add -A
git commit -m "ghép: giải quyết conflict <tên file>"
git push origin main
```

### Lỡ commit sai tên / lỡ add nhầm file

Chỉ được sửa khi **chưa push**:

```bash
git commit --amend -m "tên commit đúng"
```

### Lỡ xóa nhầm file

```bash
git restore <ten-file>
```

Muốn trả về đúng bản của GitHub (ghi đè mọi thay đổi chưa commit — cẩn thận):

```bash
git restore .
```

### Không biết còn thay đổi gì

```bash
git diff              # so sánh nội dung từng file
git log --oneline -10 # 10 commit gần nhất
git status            # trạng thái hiện tại
```

### `fatal: this operation must be run in a work tree`

Thường do biến môi trường `GIT_DIR` / `GIT_WORK_TREE` còn sót từ phiên trước:

```bash
env | grep GIT_
unset GIT_DIR GIT_WORK_TREE
```

### Lỡ push file mật khẩu / thông tin nhạy cảm

**Đừng tự xóa lịch sử** (sẽ gãy repo của mọi người). Báo ngay cho người quản lý để xử lý.

---

## 6. Bảng lệnh ghi nhớ nhanh

| Lệnh | Làm gì |
| --- | --- |
| `git status` | Xem có gì thay đổi, có gì chưa được add |
| `git diff` | Xem bên trong file thay đổi gì |
| `git add -A` | Chọn tất cả thay đổi để chụp |
| `git commit -m "..."` | Chụp lại và đặt tên |
| `git push origin main` | Đưa bản chụp lên GitHub |
| `git pull --rebase origin main` | Lấy bản mới nhất của mọi người về |
| `git log --oneline -10` | Xem 10 lần chụp gần nhất |
| `git restore <file>` | Hoàn tác thay đổi của một file |

---

## 7. Checklist trước khi push

- [ ] `git status` không liệt kê file rác (`.log`, `*tmp*`, `*.uinError`, file lạ trong `visualcode/`)
- [ ] `README.md`, `README.vi.md`, `CONTRIBUTING.md`, `.gitignore` còn nguyên
- [ ] Tên commit mô tả đúng điều bạn đã đổi
- [ ] Đã `git pull --rebase origin main` nếu push bị từ chối
