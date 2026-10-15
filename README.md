# Copyright Request Database

Repository lưu trữ cơ sở dữ liệu các công thức gán bản quyền (`copytag`) cho nhân vật (`chartag`) trên Danbooru.

## Quy ước định dạng trong `database.txt`:

### 1. Dòng ĐÃ DUYỆT (Không có dấu `?` ở đầu)
Format:
```text
chartag -> copytag
```
- Đã được con người kiểm tra và xác nhận.
- Bot chỉ dùng các dòng này để tự động gắn thẻ vào các bài đăng Danbooru.
- Ví dụ:
  ```text
  ookami_mio -> hololive
  shirakami_fubuki -> hololive
  rem_(re:zero) -> re:zero_kara_hajimeru_isekai_seikatsu
  ```

### 2. Dòng CHƯA DUYỆT (Có dấu `?` ở đầu)
Format:
```text
?chartag -> copytag1 copytag2 copytag3 ...
```
- Do bot tự động lấy top 10 thẻ bản quyền liên quan từ `https://danbooru.donmai.us/related_tag.json?query=chartag&category=copyright`.
- Ví dụ:
  ```text
  ?ookami_mio -> hololive hololive_gamers hololive_japan cover_corp
  ?tokino_sora -> hololive cover_corp
  ```

### 3. Quy trình người duyệt (Human-in-the-loop):
1. Tìm các dòng có dấu `?` ở đầu file.
2. Xóa dấu `?`.
3. Giữ lại 1 thẻ `copytag` chuẩn xác nhất cho nhân vật đó, xóa các tag gợi ý thừa còn lại.
4. Lưu file và commit lên Git.
