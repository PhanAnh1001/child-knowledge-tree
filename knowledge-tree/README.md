# Cây kiến thức 🌳

Đây là node gốc của hệ thống **mind map tree** trong dự án **Child Knowledge Tree**.

Mỗi nhánh bên dưới sẽ là một lĩnh vực kiến thức, ví dụ:

```text
knowledge-tree/nature/
knowledge-tree/ai/
knowledge-tree/programming/
knowledge-tree/life-skills/
```

## Điều hướng

- Root dự án: [Child Knowledge Tree](../README.md)
- Metadata: [metadata.json](../metadata.json)
- Cha: không có, đây là node gốc của cây.
- Con: chưa có khái niệm con nào.

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
```

Sau đó cập nhật [`../metadata.json`](../metadata.json) để lưu:

- `id`
- `title`
- `slug`
- `path`
- `readme`
- `parent_id`
- `children`
- `images`
- `status`

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
