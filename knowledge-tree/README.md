# Cây kiến thức 🌳

Đây là node gốc của hệ thống **mind map tree** trong dự án **Child Knowledge Tree**.

## Điều hướng

- Root dự án: [Child Knowledge Tree](../README.md)
- Metadata: [metadata.json](../metadata.json)
- Cha: không có, đây là node gốc của cây.
- Con:
  - [Tự nhiên](./nature/README.md)

## Nhánh hiện có

| Node | Mô tả |
|---|---|
| [Tự nhiên](./nature/README.md) | Các hiện tượng tự nhiên, môi trường, thời tiết, địa lý, sinh học đời thường. |

## Cách thêm một khái niệm mới

Khi thêm khái niệm mới, tạo thư mục theo dạng:

```text
knowledge-tree/{linh-vuc}/{linh-vuc-con}/.../{khai-niem}/
```

Trong thư mục khái niệm cần có:

```text
README.md
cover.webp
comic-01.webp
comic-02.webp
summary-map.webp
```

Sau đó cập nhật [`../metadata.json`](../metadata.json) để lưu `id`, `title`, `slug`, `path`, `readme`, `parent_id`, `children`, `images`, `status`.

## Format nội dung khái niệm

Mỗi khái niệm nên viết như một mini truyện tranh hài hước lầy lội nhưng vẫn rõ kiến thức:

1. Điều hướng.
2. Mở màn truyện tranh.
3. 5 ý cốt lõi nhất.
4. 8 ý phổ biến còn lại.
5. Áp dụng vào đời sống.
6. Giải quyết vấn đề thực tế nào.
7. So sánh với kiến thức tương tự.
8. Nguồn tham khảo có citation.

> Học mà vui thì não bớt chạy trốn. Não bớt chạy trốn thì kiến thức mới có chỗ ngồi.
