# PBT 05 - Đáp án

## Thông tin cá nhân

- Họ tên: Trịnh Bùi Duy Nguyên
- Email: nguyentwd.hubt@gmail.com
- MSSV: 2251061853
- Lớp: 66KTPM2

---

## Phần A - Kiểm tra đọc hiểu

### Câu A1
1. Thẻ viewport chuẩn:

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

`width=device-width` buộc trình duyệt sử dụng chiều rộng thực của thiết bị. `initial-scale=1.0` đặt mức zoom ban đầu là 100%.

2. Nếu thiếu thẻ này, iPhone thường giả định trang có chiều rộng ~980px rồi thu nhỏ toàn bộ layout để vừa màn hình, dẫn tới chữ nhỏ, nút khó bấm và người dùng phải phóng to.

3. Mobile-First: viết CSS mặc định cho màn hình nhỏ, sau đó mở rộng bằng `@media (min-width: ...)`. Desktop-First: viết cho màn hình lớn trước rồi thu nhỏ bằng `@media (max-width: ...)`.

```css
.grid { grid-template-columns: 1fr; }
@media (min-width: 768px) {
  .grid { grid-template-columns: repeat(2, 1fr); }
}

/* Desktop-First */
.grid { grid-template-columns: repeat(2, 1fr); }
@media (max-width: 767px) {
  .grid { grid-template-columns: 1fr; }
}
```

Mobile-First được khuyến nghị vì giúp tối ưu cho mobile (tải ít CSS hơn) và thúc đẩy thiết kế theo nội dung.

### Câu A2
| Breakpoint | Kích thước | Thiết bị đại diện | Gợi ý số cột |
|---|---:|---|---:|
| Mobile | &lt; 576px | iPhone SE, điện thoại nhỏ | 1 |
| Mobile L | &ge; 576px | điện thoại lớn, ngang | 2 |
| Tablet | &ge; 768px | iPad, tablet | 2 |
| Desktop | &ge; 992px | laptop nhỏ | 3 |
| Desktop L | &ge; 1200px | desktop, laptop lớn | 4 |
| Desktop XL | &ge; 1400px | màn hình lớn | 4-5 |

### Câu A3
| Chiều rộng màn hình | `.container` width |
|---|---:|
| 375px (iPhone SE) | 100% |
| 600px | 540px |
| 800px | 720px |
| 1000px | 960px |
| 1400px | 1140px |

### Câu A4
1. Variables: ví dụ `$primary-color: #2563eb;` dùng để tái sử dụng giá trị nhiều lần.

2. Nesting: viết CSS lồng theo cấu trúc HTML giúp code ngắn gọn và rõ ràng.

```scss
.card {
  padding: 16px;
  .card-title { font-weight: 700; }
  &:hover { transform: translateY(-4px); }
}
```

3. Mixins: định nghĩa khối CSS tái sử dụng.

```scss
@mixin flex-center {
  display: flex;
  justify-content: center;
  align-items: center;
}
```

4. `@extend`: cho selector này kế thừa selector khác.

```scss
.btn { padding: 12px 20px; border-radius: 9999px; }
.btn-primary { @extend .btn; background: #2563eb; color: white; }
```

Trình duyệt không đọc trực tiếp `.scss` vì chỉ hiểu CSS; cần biên dịch SCSS sang CSS bằng Sass compiler (ví dụ `sass`, Live Sass Compiler, Vite, webpack).

---

## Phần B - Thực hành code

### Bài B1 - Responsive Product Page

- Mobile: 1 cột, sidebar ẩn, menu hamburger.
- Tablet: 2 cột, menu ngang, sidebar hiển thị.
- Desktop: 4 cột, có ads bar, max-width 1200px.

HTML/CSS tham khảo nằm trong `responsive.html` và `responsive.css`.

### Bài B2 - CSS Transitions & Animations

- Card hover: `transform: translateY(-8px)` và shadow đậm hơn.
- Button hover: đổi màu và scale nhẹ.
- Image zoom: container `overflow: hidden`, ảnh scale 1.1 khi hover.
- Spinner: dùng `@keyframes spin`.
- Fade-in: dùng `@keyframes fadeIn`.

File tham khảo: `animations.html` và `animations.css`.

### Bài B3 - SCSS Refactor

Ví dụ biến:

```scss
$primary-color: #2563eb;
$secondary-color: #7c3aed;
$font-primary: 'Inter', sans-serif;
$breakpoint-tablet: 768px;
$breakpoint-desktop: 1024px;
$spacing-sm: 8px;
$spacing-md: 16px;
$spacing-lg: 32px;
```

Lệnh biên dịch tham khảo:

```bash
npx sass scss/style.scss css/style.css --watch
```

---

## Phần C - Phân tích

### Câu C1
- Mobile 375px: header rút gọn, hamburger xuất hiện, grid thường 1-2 cột, banner phụ ẩn bớt.
- Tablet 768px: menu rộng hơn, grid 2-3 cột, một số block quảng cáo bắt đầu hiển thị.
- Desktop 1440px: menu ngang đầy đủ, sidebar/lọc hiển thị rõ, grid 4 cột trở lên.

Media query thường gặp:

```css
@media (min-width: 768px) { ... }
@media (min-width: 1024px) { ... }
```

### Câu C2
Mobile: hero ở trên, form ở dưới, grid ảnh 1 cột (hoặc 2 cột nhỏ), map ở cuối.
Tablet: grid ảnh 2 cột, form đặt tách, map dưới form.
Desktop: bố cục 2-3 cột, nội dung chính ở giữa, map hoặc sidebar bên phải.

CSS skeleton (Mobile-First):

```css
.restaurant-page {
  display: grid;
  gap: 24px;
  grid-template-columns: 1fr;
}

.food-grid {
  display: grid;
  gap: 16px;
  grid-template-columns: 1fr;
}

@media (min-width: 768px) {
  .food-grid { grid-template-columns: repeat(2, 1fr); }
}

@media (min-width: 1024px) {
  .restaurant-page { grid-template-columns: 2fr 1fr; }
  .food-grid { grid-template-columns: repeat(3, 1fr); }
}
```

---
