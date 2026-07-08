# Child Knowledge Tree 🌳📚🤣

**Child Knowledge Tree** là dự án sử dụng **tiếng Việt** để lưu trữ kiến thức cơ bản, cốt lõi về các khái niệm theo dạng **truyện tranh hài hước lầy lội**.

Thay vì đọc lý thuyết khô như bánh mì để quên 3 ngày, mỗi khái niệm sẽ được trình bày như một mini comic: có nhân vật, tình huống đời thường, ví dụ thực tế, so sánh dễ hiểu và ảnh minh hoạ `.webp` nằm cùng thư mục với file nội dung.

## Mục tiêu

- Biến kiến thức cơ bản thành nội dung dễ đọc, dễ nhớ, dễ áp dụng.
- Tổ chức khái niệm theo dạng **mind map tree phân cấp**.
- Mỗi node trong cây là một khái niệm hoặc nhóm khái niệm.
- Mỗi khái niệm có `README.md` riêng, kèm ảnh `.webp` cùng thư mục.
- Toàn bộ dữ liệu điều hướng, đường dẫn, quan hệ cha - con - cùng cấp được quản lý trong [`metadata.json`](./metadata.json) ở root.

## Cấu trúc thư mục

```text
README.md
metadata.json
knowledge-tree/
  README.md
  {linh-vuc}/
    README.md
    {linh-vuc-con}/
      README.md
      {khai-niem}/
        README.md
        image-01.webp
        image-02.webp
```

Ví dụ đường dẫn khái niệm:

```text
knowledge-tree/{lĩnh vực}/{lĩnh vực con 1}/.../{khái niệm con n}/README.md
```

Ví dụ thực tế sau này:

```text
knowledge-tree/nature/weather/tornado/README.md
knowledge-tree/ai/llm/rag/README.md
knowledge-tree/programming/backend/api/README.md
```

## Quy ước tổ chức mind map tree

Mỗi node trong cây cần có:

- `id`: mã định danh duy nhất.
- `title`: tên hiển thị tiếng Việt.
- `slug`: tên thư mục ngắn gọn, ưu tiên `lower-kebab-case`.
- `path`: đường dẫn thư mục của node.
- `readme`: đường dẫn tới file `README.md` của node.
- `parent_id`: node cha, `null` nếu là root.
- `children`: danh sách node con.
- `siblings`: các node cùng cấp, có thể sinh từ metadata.
- `images`: danh sách ảnh `.webp` nằm cùng thư mục với README.
- `status`: trạng thái như `draft`, `ready`, `needs-images`, `needs-review`.

## Quy ước file README của từng khái niệm

Mỗi file nội dung khái niệm nên có cấu trúc:

1. **Nav điều hướng**
   - Link về node cha.
   - Link tới các node con.
   - Link tới các node cùng nhánh / cùng cấp.

2. **Mở màn truyện tranh**
   - Giới thiệu bằng tình huống hài hước, dễ hiểu.
   - Có thể dùng nhân vật cố định như: Bé Não Cá Vàng, Thầy Cú Đêm, Robot Gà Mờ, Boss Deadline.

3. **5 ý cốt lõi nhất**
   - Mỗi ý ngắn, rõ, có ví dụ đời thường.
   - Ưu tiên trả lời: “Nó là gì?”, “Dùng khi nào?”, “Giải quyết vấn đề gì?”.

4. **8 ý phổ biến còn lại**
   - Các câu hỏi hoặc tình huống thường gặp.
   - Tập trung vào hiểu đúng, tránh nhầm lẫn, áp dụng thực tế.

5. **Áp dụng vào đời sống**
   - Trường hợp thực tế.
   - Cách dùng kiến thức để ra quyết định hoặc xử lý vấn đề.

6. **So sánh với kiến thức tương tự**
   - So sánh bằng bảng hoặc ví dụ hài.
   - Nêu điểm giống, khác, khi nào chọn cái nào.

7. **Nguồn tham khảo**
   - Có link citation tới nguồn đáng tin cậy.
   - Ưu tiên tài liệu chính thống, sách, tổ chức giáo dục, tài liệu kỹ thuật, trang khoa học hoặc tài liệu gốc.

## Quy ước ảnh minh hoạ `.webp`

- Ảnh của khái niệm phải nằm **cùng thư mục** với `README.md` của khái niệm đó.
- Dùng định dạng `.webp` để nhẹ nhưng vẫn rõ nét.
- Tên ảnh nên có thứ tự:

```text
cover.webp
comic-01.webp
comic-02.webp
summary-map.webp
```

Cách nhúng ảnh trong README:

```md
![Minh hoạ khái niệm](./comic-01.webp)
```

## Quy ước metadata

File [`metadata.json`](./metadata.json) là nguồn dữ liệu trung tâm cho toàn bộ cây kiến thức.

Metadata dùng để:

- Sinh nav điều hướng.
- Biết node nào là cha, con, cùng cấp.
- Biết README nào thuộc khái niệm nào.
- Biết ảnh `.webp` nào thuộc khái niệm nào.
- Phục vụ hiển thị mind map tree sau này.

## Mẫu nav trong README khái niệm

```md
## Điều hướng

- Cha: [Thời tiết](../README.md)
- Cùng cấp:
  - [Mưa](../rain/README.md)
  - [Bão](../storm/README.md)
- Con:
  - [Lốc xoáy lửa](./fire-whirl/README.md)
  - [Vòi rồng](./waterspout/README.md)
```

## Trạng thái hiện tại

- Đã có root README.
- Đã có metadata root.
- Đã có thư mục khởi đầu `knowledge-tree/`.
- Các khái niệm chi tiết sẽ được thêm dần theo đúng metadata.

## Nguyên tắc viết nội dung

Viết sao cho một bạn nhỏ, một người mới học, hoặc một dev đang bị deadline dí vẫn hiểu được:

> “À, cái này là vậy. Dùng trong đời thật kiểu này. Nhầm với cái kia là ăn hành liền.”
