# Child Knowledge Tree 🌳📚🤣

**Child Knowledge Tree** là dự án tiếng Việt lưu trữ kiến thức cơ bản, cốt lõi dưới dạng **truyện tranh hài hước lầy lội**.

Mỗi khái niệm là một thư mục riêng. `README.md` của khái niệm chỉ đóng vai trò **khung treo tranh**: nhúng ảnh `.webp` và đặt **citation nguồn tham khảo ngay dưới mỗi ảnh**. Nội dung chi tiết như định nghĩa, ví dụ đời thường, cách áp dụng, vấn đề giải quyết và so sánh nằm trong ảnh truyện tranh.

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
      comic-04.webp
      comic-05.webp
      comic-06.webp
      comic-07.webp
      comic-08.webp
      comic-09.webp
      comic-10.webp
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
- Cách delivery ảnh: CDN-first, local fallback.
- Trạng thái node: `draft`, `ready`, `needs-images`, `needs-review`.

Quy ước path trong metadata: **không có tiền tố `knowledge-tree/`**.

## README của từng khái niệm

README khái niệm chỉ nhúng ảnh và citation nguồn tham khảo dưới mỗi ảnh, không viết lại kiến thức dài bằng Markdown.

### Quy ước link ảnh: CDN-first, local fallback

Với bộ ảnh nhiều file `.webp`, README phải **ưu tiên load ảnh từ CDN trước** để giảm lỗi GitHub `too many requests`. Link ảnh local trong repo là **fallback** để người đọc mở bản gốc khi CDN lỗi hoặc cache chưa cập nhật.

Mẫu bắt buộc cho README khái niệm public:

```md
<a href="./comic-01.webp">
  <img src="https://cdn.jsdelivr.net/gh/PhanAnh1001/child-knowledge-tree@master/nature/weather/tornado-types/comic-01.webp" alt="Comic 01" loading="lazy">
</a>

Nguồn: [Tên nguồn](https://example.com)
```

Ý nghĩa:

- `img src="https://cdn.jsdelivr.net/gh/..."` là đường dẫn **CDN-first**, trình duyệt sẽ tải ảnh từ CDN trước.
- `a href="./comic-01.webp"` là **local fallback**: nếu CDN lỗi, người đọc bấm vào ảnh để mở file local trong repo.
- `loading="lazy"` giúp trình duyệt tải ảnh dần, không dồn 12 ảnh cùng lúc.
- Tránh dùng trực tiếp `raw.githubusercontent.com` hoặc `private-user-images.githubusercontent.com` trong README khái niệm vì dễ gặp giới hạn tải ảnh.

> Lưu ý: Trong GitHub README, fallback local là fallback dạng link bấm mở. Fallback tự động bằng JavaScript/onerror không nên dùng vì GitHub có thể chặn hoặc sanitize HTML/JS. Nếu sau này dựng website riêng bằng GitHub Pages/Next.js thì có thể thêm fallback tự động ở tầng web app.

### Cách tạo ảnh trên CDN cho khái niệm mới

Ảnh không upload trực tiếp lên CDN. Quy trình đúng là: **tạo ảnh local → commit lên GitHub → dùng URL jsDelivr CDN trỏ tới file trong repo**.

Ví dụ khái niệm mới có path:

```text
ai/llm/rag/README.md
ai/llm/rag/cover.webp
ai/llm/rag/comic-01.webp
```

Thì link CDN tương ứng là:

```text
https://cdn.jsdelivr.net/gh/PhanAnh1001/child-knowledge-tree@master/ai/llm/rag/cover.webp
https://cdn.jsdelivr.net/gh/PhanAnh1001/child-knowledge-tree@master/ai/llm/rag/comic-01.webp
```

Công thức tạo link CDN:

```text
https://cdn.jsdelivr.net/gh/{owner}/{repo}@{branch}/{path-to-image}
```

Với repo này:

```text
https://cdn.jsdelivr.net/gh/PhanAnh1001/child-knowledge-tree@master/{path-to-image}
```

Checklist cho khái niệm mới:

1. Tạo đủ 12 ảnh `.webp`: `cover.webp`, `comic-01.webp` → `comic-10.webp`, `summary-map.webp`.
2. Đặt ảnh cùng thư mục với `README.md` của khái niệm.
3. Commit ảnh lên GitHub trước để CDN có file nguồn.
4. Trong README khái niệm, dùng `img src` là link jsDelivr CDN.
5. Bọc mỗi ảnh bằng `a href="./file.webp"` để có local fallback.
6. Đặt dòng `Nguồn:` ngay dưới mỗi ảnh.
7. Cập nhật `metadata.json`: danh sách ảnh local, `cdn_base_url`, trạng thái và nguồn tham khảo.
8. Nếu vừa thay ảnh mà CDN chưa cập nhật, đổi tên file theo version như `comic-01-v2.webp` hoặc purge cache jsDelivr.

Mẫu tối giản nếu chỉ xem nội bộ repo, không cần CDN:

```md
# Tên khái niệm

![Bìa truyện tranh](./cover.webp)

Nguồn: [Tên nguồn 1](https://example.com), [Tên nguồn 2](https://example.com)

![Comic 01](./comic-01.webp)

Nguồn: [Tên nguồn](https://example.com)
```

## Chuẩn ảnh truyện tranh

Mỗi bộ ảnh của một khái niệm nên có **12 ảnh**:

| Nhóm ảnh | File | Vai trò |
|---|---|---|
| Mở đầu | `cover.webp` | Bìa khái niệm, tình huống mở đầu, nhân vật vui nhộn. |
| Nội dung chính | `comic-01.webp` → `comic-10.webp` | Giải thích kiến thức chi tiết, ví dụ đời thường, áp dụng thực tế, lỗi dễ nhầm, so sánh với kiến thức tương tự. |
| Tổng kết | `summary-map.webp` | Sơ đồ tổng kết, bảng so sánh, checklist dùng khi nào/tránh khi nào, nguồn ngắn gọn nếu cần. |

Yêu cầu nội dung trong ảnh:

- Tiếng Việt dễ hiểu, có thuật ngữ tiếng Anh nếu cần.
- Phong cách truyện tranh hài hước lầy lội, nhiều nhân vật biểu cảm mạnh.
- Có ví dụ đời thường, hướng dẫn áp dụng thực tế, vấn đề được giải quyết và so sánh với khái niệm dễ nhầm.
- Mỗi ảnh nên tập trung vào một cụm ý nhỏ để chữ to, dễ đọc.
- Nguồn tham khảo đầy đủ lưu trong `metadata.json`; trong README vẫn phải có dòng **Nguồn:** ngay dưới từng ảnh.

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
3. Chia nội dung thành 12 ảnh: `cover.webp`, `comic-01.webp` đến `comic-10.webp`, `summary-map.webp`.
4. Tạo ảnh bằng DALL-E 3 hoặc DALL-E theo chuẩn trên.
5. Nếu chữ tiếng Việt trong ảnh sai, sửa thủ công hoặc tạo lại ảnh.
6. Xuất ảnh sang `.webp`, đặt cùng thư mục với `README.md`.
7. Commit ảnh `.webp` lên GitHub để jsDelivr có nguồn tạo CDN.
8. Tạo README khái niệm theo mẫu CDN-first: `img src` là link CDN, `a href` là link local fallback.
9. Đặt citation nguồn tham khảo ngay dưới mỗi ảnh.
10. Cập nhật `metadata.json` với node, path, ảnh, nguồn, trạng thái và cấu hình `image_delivery`.

## Trạng thái hiện tại

- Đã bỏ cấp thư mục `knowledge-tree/`.
- README khái niệm chỉ nhúng ảnh truyện tranh `.webp` và citation nguồn dưới từng ảnh.
- Mỗi khái niệm nên có **12 ảnh**: 1 ảnh mở đầu, 10 ảnh comic nội dung, 1 ảnh tổng kết.
- Ảnh dọc khuyến nghị **1055×1491 px**, WebP chất lượng **88–92**.
- Với các bộ ảnh dễ gặp lỗi GitHub `too many requests`, dùng mô hình **CDN-first, local fallback**.

## Nguyên tắc nội dung

Viết sao cho người mới học hoặc dev đang bị deadline dí vẫn hiểu được:

> “À, cái này là vậy. Dùng trong đời thật kiểu này. Nhầm với cái kia là ăn hành liền.”