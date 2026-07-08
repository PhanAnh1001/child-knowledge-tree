# Child Knowledge Tree 🌳📚🤣

**Child Knowledge Tree** là dự án sử dụng **tiếng Việt** để lưu trữ kiến thức cơ bản, cốt lõi về các khái niệm theo dạng **truyện tranh hài hước lầy lội**.

Mỗi khái niệm được trình bày bằng các ảnh truyện tranh `.webp` khá nét. Ảnh cần chứa kiến thức chi tiết hơn: định nghĩa, ví dụ đời thường, cách áp dụng thực tế, vấn đề thực tế được giải quyết nếu có, so sánh với kiến thức tương tự và nguồn tham khảo.

## Mục tiêu

- Biến kiến thức cơ bản thành nội dung dễ đọc, dễ nhớ, dễ áp dụng.
- Tổ chức khái niệm theo dạng **mind map tree phân cấp**.
- Mỗi node trong cây là một khái niệm hoặc nhóm khái niệm.
- Mỗi khái niệm có `README.md` riêng, nội dung chính chỉ là các ảnh `.webp` cùng thư mục.
- Toàn bộ dữ liệu điều hướng, đường dẫn, quan hệ cha - con - cùng cấp được quản lý trong [`metadata.json`](./metadata.json) ở root.

## Khái niệm đã có

| Lĩnh vực | Nhánh | Khái niệm | Trạng thái |
|---|---|---|---|
| Tự nhiên | Thời tiết | Các loại lốc xoáy | `ready` |

## Cấu trúc thư mục

Không dùng thêm cấp thư mục `knowledge-tree/`. Cây kiến thức bắt đầu trực tiếp từ root repo.

```text
README.md
metadata.json
{linh-vuc}/
  README.md
  {linh-vuc-con}/
    README.md
    {khai-niem}/
      README.md
      cover.webp
      comic-01.webp
      comic-02.webp
      comic-03.webp
      summary-map.webp
```

Ví dụ đường dẫn khái niệm:

```text
{linh-vuc}/{linh-vuc-con-1}/.../{khai-niem-con-n}/README.md
```

Ví dụ thực tế:

```text
nature/weather/tornado-types/README.md
ai/llm/rag/README.md
programming/backend/api/README.md
```

## Quy ước tổ chức mind map tree

Mỗi node trong cây cần có:

- `id`: mã định danh duy nhất.
- `title`: tên hiển thị tiếng Việt.
- `slug`: tên thư mục ngắn gọn, ưu tiên `lower-kebab-case`.
- `path`: đường dẫn thư mục của node, **không có tiền tố `knowledge-tree/`**.
- `readme`: đường dẫn tới file `README.md` của node.
- `parent_id`: node cha, `null` nếu là root.
- `children`: danh sách node con.
- `siblings`: các node cùng cấp, có thể sinh từ metadata.
- `images`: danh sách ảnh `.webp` nằm cùng thư mục với README.
- `sources`: danh sách link nguồn tham khảo.
- `status`: trạng thái như `draft`, `ready`, `needs-images`, `needs-review`.

## Quy ước file README của từng khái niệm

README của khái niệm chỉ cần đóng vai trò như “khung treo tranh”. Nội dung kiến thức chi tiết nằm trong ảnh truyện tranh, không viết lại thành các section Markdown dài.

Mẫu tối giản:

```md
# Tên khái niệm

![Bìa truyện tranh](./cover.webp)
![Comic 01](./comic-01.webp)
![Comic 02](./comic-02.webp)
![Comic 03](./comic-03.webp)
![Sơ đồ tổng kết](./summary-map.webp)
```

Không cần viết các phần dài bằng Markdown như “5 ý cốt lõi”, “áp dụng vào đời sống”, “so sánh”, “nguồn tham khảo”. Các nội dung đó phải nằm trong ảnh hoặc trong `metadata.json` nếu cần phục vụ tra cứu.

## Quy ước nội dung bên trong ảnh truyện tranh

Mỗi bộ ảnh của một khái niệm nên có:

1. **`cover.webp`**: tên khái niệm, tình huống mở đầu, nhân vật vui nhộn.
2. **`comic-01.webp`, `comic-02.webp`, ...**: giải thích dễ hiểu, thuật ngữ tiếng Anh nếu có, ví dụ đời thường, cách áp dụng thực tế, vấn đề giải quyết, so sánh với kiến thức tương tự.
3. **`summary-map.webp`**: sơ đồ tóm tắt, bảng so sánh, checklist dùng khi nào/tránh khi nào.
4. **Nguồn tham khảo**: ưu tiên lưu link trong `metadata.json`; nếu cần hiển thị trong ảnh thì đặt nguồn ngắn gọn ở cuối `summary-map.webp`.

## Hướng dẫn tạo ảnh bằng DALL-E 3 hoặc DALL-E

Ảnh truyện tranh có thể được tạo bằng **DALL-E 3** hoặc **DALL-E**.

Quy trình khuyến nghị:

1. **Chốt nội dung trước**
   - Xác định ý cốt lõi, ví dụ đời thường, cách áp dụng thực tế, vấn đề được giải quyết và phần so sánh.
   - Chuẩn bị nguồn tham khảo để lưu vào `metadata.json`.

2. **Tạo ảnh bằng DALL-E 3 hoặc DALL-E**
   - Phong cách: truyện tranh tiếng Việt, hài hước lầy lội, giáo dục, dễ hiểu.
   - Bố cục: nhiều panel rõ ràng, chữ lớn, ít chữ mỗi ô, nhân vật biểu cảm mạnh.
   - Nội dung bắt buộc: định nghĩa, ví dụ, ứng dụng thực tế, lỗi dễ nhầm, so sánh.
   - Kết quả cần rõ nét, dễ đọc trên GitHub.

3. **Prompt mẫu ngắn**

```text
Tạo ảnh truyện tranh tiếng Việt về khái niệm: {TEN_KHAI_NIEM}.
Phong cách hài hước lầy lội, giáo dục, dễ hiểu.
Bố cục 4-6 panel, chữ lớn, ít chữ mỗi panel.
Nội dung gồm: định nghĩa ngắn, ví dụ đời thường, cách áp dụng thực tế, vấn đề được giải quyết, so sánh với khái niệm dễ nhầm.
Ảnh rõ nét, phù hợp lưu thành .webp.
```

4. **Hậu kỳ**
   - Nếu chữ tiếng Việt trong ảnh bị sai, cần sửa thủ công hoặc tạo lại ảnh.
   - Có thể tạo hình nền/nhân vật bằng DALL-E 3 hoặc DALL-E, rồi thêm chữ sau để đảm bảo đúng chính tả.
   - Xuất ảnh sang `.webp`, đặt cùng thư mục với `README.md` của khái niệm.

## Quy ước ảnh `.webp`

- Ảnh của khái niệm phải nằm **cùng thư mục** với `README.md` của khái niệm đó.
- Dùng định dạng `.webp` để nhẹ nhưng vẫn rõ nét.
- Tên ảnh nên có thứ tự:

```text
cover.webp
comic-01.webp
comic-02.webp
comic-03.webp
summary-map.webp
```

Cách nhúng ảnh trong README:

```md
![Minh hoạ khái niệm](./comic-01.webp)
```

## Quy ước metadata

File [`metadata.json`](./metadata.json) là nguồn dữ liệu trung tâm cho toàn bộ cây kiến thức.

Metadata dùng để:

- Sinh nav điều hướng nếu cần hiển thị ở app/site ngoài README.
- Biết node nào là cha, con, cùng cấp.
- Biết README nào thuộc khái niệm nào.
- Biết ảnh `.webp` nào thuộc khái niệm nào.
- Lưu link nguồn tham khảo của từng khái niệm.
- Phục vụ hiển thị mind map tree sau này.

## Trạng thái hiện tại

- Đã có root README.
- Đã có metadata root.
- Quy ước mới: bỏ cấp thư mục `knowledge-tree/`; đường dẫn khái niệm bắt đầu trực tiếp từ `{linh-vuc}/...`.
- Quy ước mới: README khái niệm chỉ cần nhúng ảnh truyện tranh `.webp`; nội dung chi tiết nằm trong ảnh.
- Ảnh truyện tranh có thể tạo bằng DALL-E 3 hoặc DALL-E, sau đó lưu `.webp` cùng thư mục với README khái niệm.

## Nguyên tắc nội dung

Viết sao cho người mới học hoặc dev đang bị deadline dí vẫn hiểu được:

> “À, cái này là vậy. Dùng trong đời thật kiểu này. Nhầm với cái kia là ăn hành liền.”
