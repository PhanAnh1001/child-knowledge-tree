# Child Knowledge Tree 🌳📚🤣

**Child Knowledge Tree** là dự án tiếng Việt lưu trữ kiến thức cơ bản, cốt lõi dưới dạng **truyện tranh hài hước lầy lội**.

Mỗi khái niệm là một thư mục riêng, trong đó `README.md` chỉ đóng vai trò **khung treo tranh**: nhúng các ảnh `.webp`. Nội dung chi tiết như định nghĩa, ví dụ đời thường, cách áp dụng, vấn đề giải quyết, so sánh và nguồn tham khảo sẽ nằm trong ảnh hoặc `metadata.json`.

## Khái niệm đã có

| Lĩnh vực | Nhánh | Khái niệm | Trạng thái |
|---|---|---|---|
| Tự nhiên | Thời tiết | [Các loại lốc xoáy](./nature/weather/tornado-types/README.md) | `ready` |

## Cấu trúc thư mục

Không dùng thêm cấp `knowledge-tree/`. Cây kiến thức bắt đầu trực tiếp từ root repo.

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

Ví dụ:

```text
nature/weather/tornado-types/README.md
ai/llm/rag/README.md
programming/backend/api/README.md
```

## Metadata là nguồn dữ liệu trung tâm

File [`metadata.json`](./metadata.json) dùng để lưu:

- `id`, `title`, `slug`, `path`, `readme`.
- Quan hệ cây: `parent_id`, `children`, `siblings` nếu cần.
- Danh sách ảnh `.webp` của từng khái niệm.
- Danh sách nguồn tham khảo `sources`.
- Trạng thái node: `draft`, `ready`, `needs-images`, `needs-review`.

Quy ước path trong metadata: **không có tiền tố `knowledge-tree/`**.

## README của từng khái niệm

README khái niệm chỉ cần nhúng ảnh, không viết lại kiến thức dài bằng Markdown.

Mẫu tối giản:

```md
# Tên khái niệm

![Bìa truyện tranh](./cover.webp)

![Comic 01](./comic-01.webp)

![Comic 02](./comic-02.webp)

![Comic 03](./comic-03.webp)

![Sơ đồ tổng kết](./summary-map.webp)
```

## Chuẩn ảnh truyện tranh

Mỗi bộ ảnh của một khái niệm nên có:

| File | Vai trò |
|---|---|
| `cover.webp` | Bìa khái niệm, tình huống mở đầu, nhân vật vui nhộn. |
| `comic-01.webp`, `comic-02.webp`, `comic-03.webp` | Giải thích kiến thức, ví dụ đời thường, áp dụng thực tế, lỗi dễ nhầm, so sánh. |
| `summary-map.webp` | Sơ đồ tổng kết, bảng so sánh, checklist dùng khi nào/tránh khi nào, nguồn ngắn gọn nếu cần. |

Yêu cầu nội dung trong ảnh:

- Tiếng Việt dễ hiểu, có thuật ngữ tiếng Anh nếu cần.
- Phong cách truyện tranh hài hước lầy lội, nhiều nhân vật biểu cảm mạnh.
- Có ví dụ đời thường, hướng dẫn áp dụng thực tế, vấn đề được giải quyết và so sánh với khái niệm dễ nhầm.
- Nguồn tham khảo đầy đủ lưu trong `metadata.json`; ảnh có thể ghi nguồn ngắn gọn ở `summary-map.webp`.

## Tạo và tối ưu ảnh

Ảnh có thể tạo bằng **DALL-E 3** hoặc **DALL-E**.

Thông số khuyến nghị:

| Thuộc tính | Quy ước |
|---|---|
| Kích thước ảnh dọc | **1055×1491 px** hoặc tỷ lệ gần **1000:1414** |
| Định dạng | `.webp` |
| Chất lượng WebP | **88–92** |
| Nén WebP | Ưu tiên `method=6` nếu dùng Pillow/Python |
| Dung lượng mục tiêu | Khoảng **450–700 KB/ảnh** cho ảnh nhiều panel, nhiều chữ, màu rõ |

Không nên giảm chiều rộng quá thấp nếu ảnh có nhiều chữ, vì chữ trong panel sẽ dễ mờ hoặc vỡ. Ưu tiên đọc được chữ trước, nhẹ file sau.

Prompt mẫu:

```text
Tạo ảnh truyện tranh tiếng Việt về khái niệm: {TEN_KHAI_NIEM}.
Phong cách hài hước lầy lội, giáo dục, dễ hiểu.
Bố cục 4-6 panel, chữ lớn, ít chữ mỗi panel, nhiều nhân vật biểu cảm mạnh.
Nội dung gồm: định nghĩa ngắn, ví dụ đời thường, cách áp dụng thực tế, vấn đề được giải quyết, so sánh với khái niệm dễ nhầm.
Ảnh dọc kích thước khoảng 1055×1491 px hoặc tỷ lệ 1000:1414, rõ nét, phù hợp lưu thành .webp.
```

Ví dụ tối ưu bằng Python/Pillow:

```python
from PIL import Image
from pathlib import Path

src = Path("comic-01.png")
dst = Path("comic-01.webp")

im = Image.open(src).convert("RGB")
im.save(dst, "WEBP", quality=90, method=6)
```

Dung lượng tham khảo từ bộ ảnh `nature/weather/tornado-types`:

| File | Kích thước | Dung lượng WebP tham khảo |
|---|---:|---:|
| `cover.webp` | 1055×1491 px | ~463 KB |
| `comic-01.webp` | 1055×1491 px | ~593 KB |
| `comic-02.webp` | 1055×1491 px | ~573 KB |
| `comic-03.webp` | 1055×1491 px | ~681 KB |
| `summary-map.webp` | 1055×1491 px | ~541 KB |

## Quy trình thêm khái niệm mới

1. Chọn path ngắn gọn theo dạng `{linh-vuc}/{linh-vuc-con}/.../{khai-niem}/`.
2. Chốt nội dung: định nghĩa, ví dụ, áp dụng thực tế, so sánh, nguồn tham khảo.
3. Tạo ảnh bằng DALL-E 3 hoặc DALL-E theo chuẩn trên.
4. Nếu chữ tiếng Việt trong ảnh sai, sửa thủ công hoặc tạo lại ảnh.
5. Xuất ảnh sang `.webp`, đặt cùng thư mục với `README.md`.
6. Tạo README khái niệm chỉ nhúng ảnh.
7. Cập nhật `metadata.json` với node, path, ảnh, nguồn và trạng thái.

## Trạng thái hiện tại

- Đã bỏ cấp thư mục `knowledge-tree/`.
- README khái niệm chỉ nhúng ảnh truyện tranh `.webp`.
- Ảnh dọc khuyến nghị **1055×1491 px**, WebP chất lượng **88–92**.

## Nguyên tắc nội dung

Viết sao cho người mới học hoặc dev đang bị deadline dí vẫn hiểu được:

> “À, cái này là vậy. Dùng trong đời thật kiểu này. Nhầm với cái kia là ăn hành liền.”
