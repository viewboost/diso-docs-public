# Tài liệu Chỉ số Dashboard T-Fluencers

## Mục lục
- [1. Tổng quan](#1-tổng-quan)
- **Phần A — Chỉ số Toàn cục (Global)**
  - [2. Chỉ số Influencer](#2-chỉ-số-influencer)
- **Phần B — Chỉ số theo Thử thách (Tab Overview)**
  - [3. Chỉ số Video](#3-chỉ-số-video)
  - [4. Lượt xem (Views)](#4-lượt-xem-views)
  - [5. Tổng phí quảng cáo (Total Ad Spend)](#5-tổng-phí-quảng-cáo-total-ad-spend)
  - [6. Tương tác (Engagement)](#6-tương-tác-engagement)
  - [7. Nền tảng (Platform)](#7-nền-tảng-platform)
  - [8. Ngân sách (Budget)](#8-ngân-sách-budget)
  - [9. CPV (Cost Per View)](#9-cpv-cost-per-view)
  - [10. Duyệt nội dung (Approval)](#10-duyệt-nội-dung-approval)
- **Phần C — Chỉ số Chuyển khoản (Tab Admin)**
    - [11. Chuyển khoản (Transfer)](#11-chuyển-khoản-transfer)
- **Phần D — Xuất dữ liệu (Export)**
  - [12. Chức năng Xuất dữ liệu](#12-chức-năng-xuất-dữ-liệu)

---

## 1. Tổng quan

Dashboard hiển thị các chỉ số phân tích hiệu quả của chương trình T-Fluencers.

### Phạm vi dữ liệu (Scope)
- **Toàn cục (Global)**: Dữ liệu toàn hệ thống, tất cả chiến dịch
- **Thử thách (Campaign)**: Dữ liệu theo từng chiến dịch/thử thách cụ thể
- **Thời gian (Period)**: Mặc định 30 ngày gần nhất, có thể tùy chỉnh

---

## Phần A — Chỉ số Toàn cục (Global)

> **Bộ lọc**: Không có — dữ liệu cố định, luôn lấy **toàn bộ hệ thống, tất cả thử thách, 30 ngày gần nhất (không kể hôm nay)**. Không thể thay đổi bằng bộ lọc Campaign hay Time Period trên giao diện.

---

## 2. Chỉ số Influencer

> **Phạm vi**: 4 KPI cards này là **Toàn cục - Tất cả thử thách (Global - Platform-wide)**, tức dữ liệu toàn hệ thống, không lọc theo campaign. Dữ liệu lấy **30 ngày gần nhất, không kể hôm nay**. Mặc định so sánh với 30 ngày liền trước đó.

### 2.1. Tổng số Influencer (Total Influencers)

**Định nghĩa**: Tổng số influencer đã đăng ký trong hệ thống tính đến thời điểm hiện tại (không lọc theo kỳ).

**Cách tính**:
```
Tổng số Influencer = COUNT(tất cả users trong collection UserRaw)
```
> Không lọc theo ngày — đây là tổng tích lũy toàn bộ từ trước đến nay.

**Trend so sánh**:
```
Kỳ trước = COUNT(users WHERE createdAt <= 30 ngày trước)
Trend = (Total hiện tại - Kỳ trước) / Kỳ trước × 100%
```

**Ý nghĩa kinh doanh**:
- Đo lường quy mô mạng lưới influencer tích lũy
- KPI chính để đánh giá độ phủ của chương trình

---

### 2.2. Influencer mới (New Influencers)

**Định nghĩa**: Số influencer **mới đăng ký tài khoản** vào hệ thống trong 30 ngày gần nhất.

**Cách tính**:
```
Influencer mới = COUNT(users WHERE createdAt >= [30 ngày trước] AND createdAt <= [hôm nay])
```

> **Lưu ý quan trọng**: "Influencer mới" ở đây là **mới đăng ký tài khoản**, không phải mới lần đầu tham gia campaign. Một influencer có thể đăng ký nhưng chưa submit video nào.

**Ý nghĩa kinh doanh**:
- Đo lường tốc độ tuyển mới (acquisition)
- Đánh giá hiệu quả các kênh onboarding

---

### 2.3. Tỷ lệ hoạt động (Activity Rate)

**Định nghĩa**: Tỷ lệ influencer có ít nhất 1 lần submit content trong 30 ngày gần nhất, trên tổng số influencer đã đăng ký.

**Cách tính**:
```
Influencer hoạt động = COUNT(DISTINCT user IN contents WHERE date >= 30 ngày trước AND date <= hôm nay)
Tỷ lệ hoạt động     = ROUND(Influencer hoạt động / Tổng số Influencer × 100%, 1 chữ số thập phân)

Ví dụ: 5 creators hoạt động / 48 tổng = 10.4%
```

> **Nguồn dữ liệu**: Collection `contents` (không phải `content_flow`), field `user` (không phải `createdBy`). Query: `Distinct("user", {date: {$gte: start, $lte: end}})`

**Ý nghĩa kinh doanh**:
- Đo lường mức độ engagement thực tế của mạng lưới
- Tỷ lệ hoạt động thấp (10.4%) cho thấy phần lớn influencer đăng ký nhưng chưa hoạt động
- KPI quan trọng để đánh giá "chất lượng" mạng lưới (không chỉ số lượng)

---

### 2.4. Tỷ lệ nghỉ (Churn Rate)

**Định nghĩa**: Tỷ lệ influencer **không** có hoạt động submit content trong 30 ngày gần nhất.

**Cách tính**:
```
Tỷ lệ nghỉ = ROUND(100% - Tỷ lệ hoạt động, 1 chữ số thập phân)

Ví dụ: 100% - 10.4% = 89.6%
```

> **Quan trọng**: Tỷ lệ nghỉ được tính trực tiếp từ Tỷ lệ hoạt động, không query riêng. Luôn đảm bảo: `Tỷ lệ hoạt động + Tỷ lệ nghỉ = 100%`.

**Ý nghĩa kinh doanh**:
- Tỷ lệ nghỉ cao (89.6%) = phần lớn influencer không hoạt động trong kỳ
- Cảnh báo sớm về vấn đề retention
- Tỷ lệ nghỉ **thấp** là tốt (ngược với các chỉ số tăng trưởng khác)
- Trend ↓ (giảm Tỷ lệ nghỉ) là tín hiệu tích cực

---

### 2.5. Phân nhóm Creator (Creator Segments) ⚠️ Chưa hiển thị trên UI

**Phạm vi**: Theo từng campaign cụ thể (không phải Global)

**Định nghĩa & Cách phân loại**:

| Nhóm | Điều kiện | Ví dụ |
|------|-----------|-------|
| **Tham gia** (Participating) | Đã submit ≥ 1 video trong campaign | 324 creators |
| **Chưa submit** (Not Submitted) | Đăng ký campaign nhưng chưa submit | 180 creators |
| **Lần đầu** (First Time) | Lần đầu tham gia bất kỳ campaign nào | 85 creators |
| **Quay lại** (Returning) | Đã tham gia ≥ 1 campaign trước đó | 59 creators |

```
Logic phân loại:
IF contentCount > 0 (trong campaign này):
    IF không có record ở campaign nào trước → "Lần đầu"
    ELSE → "Quay lại"
ELSE:
    → "Chưa submit"
```

> **Lưu ý**: "Lần đầu" và "Quay lại" là subset của "Tham gia" — tổng "Lần đầu + Quay lại = Tham gia".

---

## Phần B — Chỉ số theo Thử thách (Tab Overview)

> **Bộ lọc**: Phụ thuộc hoàn toàn vào bộ lọc phía trên giao diện:
> - **Thử thách (Campaign)**: Chọn một hoặc tất cả thử thách. Mặc định: All Campaigns
> - **Khoảng thời gian (Time Period)**: Chọn 7 ngày / 30 ngày / tùy chỉnh. Mặc định: 30 ngày gần nhất
> - **From – To**: Ngày bắt đầu và kết thúc cụ thể
>
> Sau khi thay đổi bộ lọc, nhấn **Apply** để cập nhật dữ liệu.

---

## 3. Chỉ số Video

### 3.1. Tổng số Video (Total Videos)

**Định nghĩa**: Tổng số video hợp lệ (không tính bị từ chối) được submit bởi influencer.

**Cách tính**:
```
Tổng số Video = SUM(event_analytic_daily.statistic.totalContent)
              - SUM(event_analytic_daily.statistic.totalContentRejected)
              = Đã duyệt + Chờ duyệt  (không tính Từ chối)
```

**Phân tích chi tiết (Breakdown)**:
- **Theo nền tảng**: Facebook, Facebook Reel, YouTube, YouTube Short, TikTok, Instagram, Instagram Reel
- **Theo trạng thái**: Đã duyệt (Approved), Chờ duyệt (Pending), Từ chối (Rejected)

**Ý nghĩa kinh doanh**:
- Đo lường sản lượng content
- Tracking campaign performance
- Dự báo chi phí thanh toán (chỉ video đã duyệt mới được thanh toán)

---

### 3.2. Video theo nền tảng

**Nguồn dữ liệu**: Có 2 cách tính tùy theo loại dữ liệu hiển thị:

**Số lượng video (Total/Approved/Pending/Rejected) per platform** — từ `event_analytic_daily`:
```
Video[platform]    = SUM(event_analytic_daily.statistic.[platform].totalContent)
Approved[platform] = SUM(event_analytic_daily.statistic.[platform].totalContentApproved)
Pending[platform]  = SUM(event_analytic_daily.statistic.[platform].totalContentPending)
Rejected[platform] = SUM(event_analytic_daily.statistic.[platform].totalContentRejected)
```

Các nền tảng được tổng hợp: `facebook`, `facebookReel`, `youtube`, `youtubeShort`, `tiktok`, `instagram`, `instagramReel`

**Card "Video theo nền tảng" (videosByPlatform breakdown)** — từ `event_analytic_daily`:
```
Video[platform]    = SUM(event_analytic_daily.statistic.[platform].totalContent)
Approved[platform] = SUM(event_analytic_daily.statistic.[platform].totalContentApproved)
Rejected[platform] = SUM(event_analytic_daily.statistic.[platform].totalContentRejected)
```

> Tái sử dụng `GetPlatformBreakdown()` — có đầy đủ date filter. Đã migrate từ `content_flow` (v2.7.0).

**Ví dụ thực tế**:
```
YouTube:  Tổng 139 | ✓ Đã duyệt 130 | ✗ Từ chối 9
Facebook: Tổng 115 | ✓ Đã duyệt 100 | ✗ Từ chối 15
TikTok:   Tổng 108 | ✓ Đã duyệt 95  | ✗ Từ chối 13
```

**Ý nghĩa**:
- So sánh hiệu quả giữa các nền tảng
- Phát hiện nền tảng có tỷ lệ từ chối cao

---

## 4. Lượt xem (Views)

**Định nghĩa**: Tổng số lượt xem được ghi nhận trên tất cả video của influencer trong kỳ lọc.

### 4.1. KPI card Tổng lượt xem (Overview tab)

**Cách tính**:
```
Tổng lượt xem = SUM(event_analytic_daily.statistic.view.total)
              - SUM(event_analytic_daily.statistic.view.rejected)
              (loại trừ rejected views)
```

> **Lưu ý**: Backend API `/analytics/dashboard` hiện chưa trả field `viewRejected` riêng — FE dùng gross `view.total` tạm thời. Khi BE thêm field này, FE sẽ cập nhật sang net.

**Bộ lọc áp dụng**: Campaign + From/To date range (xem Phần B)

---

### 4.2. Lượt xem theo nền tảng (Platform table)

Lượt xem theo platform được lấy từ collection **khác** — `content_analytic_daily` (không phải `event_analytic_daily`):

```
Lượt xem[platform] = SUM(content_analytic_daily.view.value)
                     WHERE source = [platform] AND date IN [range]
```

> Platform là field `source` trong `content_analytic_daily`, group by `$source`.

---

### 4.3. Biểu đồ Timeline (Lượt xem theo ngày)

**Cách tính**:
```
Lượt xem[ngày] = SUM(user_event_analytic_daily.statistic.view.total)
               - SUM(user_event_analytic_daily.statistic.view.rejected)
                 WHERE date = [ngày đó]
```

**Bộ lọc**: Campaign + date range. Timeline hỗ trợ 3 khoảng: 7 ngày, 30 ngày, 90 ngày.

---

### 4.4. Lượt xem trong tab Influencer (Creator KPIs)

Khi xem theo từng influencer (tab Influencer), lượt xem được tổng hợp từ `user_event_analytic_daily`:

```
Tổng lượt xem = SUM(user_event_analytic_daily.statistic.view.total)
                WHERE event IN [campaigns] AND user IN [influencers] AND date IN [range]
```

---

**Ý nghĩa kinh doanh**:
- Đo lường độ phủ (reach) của campaign
- KPI chính cho brand awareness
- **Cơ sở để tính CPV** — càng nhiều lượt xem với cùng chi phí → CPV càng thấp → càng hiệu quả

---

## 5. Tổng phí quảng cáo (Total Ad Spend)

**Định nghĩa**: Tổng số tiền thưởng đã phát sinh cho influencer trong kỳ lọc, bao gồm tất cả trạng thái thanh toán.

### 5.1. KPI card Tổng phí (Overview tab)

Dữ liệu cash được tổng hợp từ `event_analytic_daily`:

```
Tổng phí quảng cáo (hiển thị) = SUM(cash.total) - SUM(cash.rejected)
                               = Pending + Completed + Transferred  (loại trừ Rejected)
                               = cashValid
```

> **Lưu ý quan trọng**: KPI card hiển thị **cashValid** (loại trừ rejected), không phải `cash.total`.
> Backend field `cash.completed` trong API response thực chất được gán = `cash.total - cash.rejected` (= cashValid) — đặt tên misleading, giá trị là cashValid.

**Các giá trị backend trả về**:
```
cash.total     = SUM(cash.total)     = Pending + Completed + Transferred + Rejected
cash.rejected  = SUM(cash.rejected)
cash.pending   = SUM(cash.pending)
cash.completed = cash.total - cash.rejected  ← tên misleading, thực chất = cashValid
cash.transferred = SUM(cash.transfer)
```

**Bộ lọc áp dụng**: Campaign + From/To date range

---

### 5.2. Ngân sách campaign (Budget & CashValid)

Budget và CashValid **không** lấy từ `event_analytic_daily` — được truy vấn riêng từ collection `events`:

```
Budget    = SUM(event.budget)
            WHERE _id IN [campaignIds]

CashValid = SUM(event.statistic.totalCashPending
              + event.statistic.totalCashCompleted
              + event.statistic.totalCashWaiting)
            WHERE _id IN [campaignIds]
```

> Budget là ngân sách được cấp phát cho campaign (không phụ thuộc date range).
> CashValid là tổng tiền thưởng hợp lệ đang trong chu trình xử lý (pending + completed + waiting).

---

**Ý nghĩa kinh doanh**:
- Tracking chi phí thực tế của campaign
- So sánh `CashValid` với `Budget` để biết mức độ giải ngân
- `cashValid` (= `cash.total - cash.rejected`) là cơ sở tính CPV (xem mục 9.1)

---

## 6. Tương tác (Engagement)

### 6.1. Phân tích tương tác (Interaction Breakdown)

KPI card tương tác lấy từ `event_analytic_daily`, gồm 3 chỉ số:

```
Lượt xem  (Views)    = SUM(event_analytic_daily.statistic.view.total)
Thích     (Likes)    = SUM(event_analytic_daily.statistic.like.total)
Bình luận (Comments) = SUM(event_analytic_daily.statistic.comment.total)
```

> **Chia sẻ (Shares) đã bị loại bỏ** — không được thu thập từ các nền tảng, field luôn = 0. Widget không hiển thị Shares.

---

### 6.2. Tỷ lệ tương tác (Engagement Rate)

**Cách tính trong KPI card** (Overview tab):
```
Engagement Rate = (Thích + Bình luận) / Lượt xem × 100%
```

> Không có Shares — công thức chỉ dùng Likes + Comments.

**Cách tính trong biểu đồ Timeline** — chia cho số video (không phải views):
```
Engagement[ngày] = (Likes + Comments) / totalVideosNet × 100%
                   WHERE totalVideosNet > 0

totalVideosNet = totalContent - totalContentRejected
```

> Timeline dùng `user_event_analytic_daily`, group by date. Engagement = 0 nếu không có video trong ngày đó.

**Ý nghĩa kinh doanh**:
- Đo lường chất lượng content (lượt xem nhiều nhưng tỷ lệ tương tác thấp = content chưa đủ hấp dẫn)
- Đánh giá mức độ viral của video
- So sánh hiệu quả giữa các influencer/nền tảng

---

### 6.3. Tương tác trung bình theo nền tảng (Avg Engagement per Platform)

Lấy từ `content_analytic_daily` (không phải `event_analytic_daily`), group by `source` (platform):

```
Likes[platform]    = SUM(content_analytic_daily.like.value)    WHERE source = [platform]
Comments[platform] = SUM(content_analytic_daily.comment.value) WHERE source = [platform]
Views[platform]    = SUM(content_analytic_daily.view.value)    WHERE source = [platform]

Avg Engagement[platform] = (Likes + Comments) / Views × 100%
```

---

## 7. Nền tảng (Platform)

UI hiển thị 2 components trong mục này.

### 7.1. Biểu đồ Phân bố Nền tảng (Donut chart)

**Định nghĩa**: Tỷ lệ % số video hợp lệ (không tính rejected) theo từng nền tảng.

**Cách tính**:
```
VideoNet[platform]  = SUM(totalContent) - SUM(totalContentRejected)
totalNetVideos      = SUM(VideoNet[all platforms])
Phần trăm[platform] = VideoNet[platform] / totalNetVideos × 100%
```

> Sub-platform được gộp lại trước khi tính: `facebook + facebookReel → Facebook`, `youtube + youtubeShort → YouTube`, `instagram + instagramReel → Instagram`
> Percentage được tính lại client-side từ net values (không dùng % gross từ BE).

**Nguồn**: `event_analytic_daily` — API `GET /analytics/platforms?withMetrics=true`

**Bộ lọc**: Campaign + From/To date range

**Hiển thị**: Legend và tooltip hiển thị cả % lẫn số video tuyệt đối — ví dụ: `"YouTube (72% · 1,234)"`

---

### 7.2. Biểu đồ Lượt xem theo Nền tảng (Bar chart ngang)

**Định nghĩa**: Tổng lượt xem theo từng nền tảng, sắp xếp giảm dần.

**Cách tính**:
```
Lượt xem[platform] = SUM(content_analytic_daily.view.value)
                     WHERE source = [platform] AND date IN [range]
```

> Lấy từ `content_analytic_daily` (khác nguồn với donut chart), group by field `source`.
> Sub-platform cũng được gộp theo cùng logic trên.

**Bộ lọc**: Campaign + From/To date range

---

## 8. Ngân sách (Budget)

Widget "Tổng quan Ngân sách" hiển thị 4 chỉ số: progress bar, Used (%), Total, Remaining.

**Nguồn dữ liệu**: API `/analytics/dashboard` → `cash.cashValid` và `cash.budget` (xem mục 5.2)

### 8.1. Đã sử dụng (Used)

```
Used = event.statistic.totalCashPending
     + event.statistic.totalCashCompleted
     + event.statistic.totalCashWaiting
```

> Là `cashValid` — tổng tiền thưởng đang trong chu trình xử lý (chưa tính rejected, không phụ thuộc date range).

### 8.2. Tổng ngân sách (Total)

```
Total = event.budget
```

> Ngân sách cố định được cấp phát cho campaign, không thay đổi theo date range.

### 8.3. Còn lại (Remaining)

```
Remaining = Total - Used
```

### 8.4. Phần trăm đã dùng (Used %)

```
Used % = ROUND(Used / Total × 100)%
```

**Màu sắc theo ngưỡng**:
- ≤ 70%: Xanh (An toàn)
- 71–85%: Vàng (Cảnh báo)
- > 85%: Đỏ (Nguy hiểm)

> **Lưu ý**: Trước đây widget hiển thị thêm block "Burn Rate" riêng — đã loại bỏ vì là alias của Used % (không thêm thông tin mới).

**Ý nghĩa kinh doanh**:
- Theo dõi mức độ giải ngân so với ngân sách phân bổ
- Cảnh báo khi sắp hết ngân sách

---

## 9. CPV (Cost Per View)

**Tên đầy đủ**: Chi phí trên mỗi lượt xem (Cost Per View). Đơn vị: đồng/lượt xem (VND/view).

CPV xuất hiện ở 2 nơi trên UI với **công thức tử số khác nhau**.

### 9.1. KPI card CPV (Overview tab)

Tính trong service layer sau khi aggregate từ `event_analytic_daily` (`dashboard_analytics.go`):

```
totalCashValid = SUM(cash.total) - SUM(cash.rejected)
              = pending + completed + transferred  (loại trừ rejected)

totalViewValid = SUM(view.total) - SUM(view.rejected)

CPV = totalCashValid / totalViewValid

Nếu totalViewValid = 0 → CPV = 0
```

> **Tử số** là `cash.total - cash.rejected` (= cashValid), **không phải** `cash.completed`.
> **Mẫu số** là `view.total - view.rejected`, **không phải** `view.total`.
> Cả tử và mẫu đều loại trừ phần bị từ chối (rejected).

**Bộ lọc**: Campaign + From/To date range

---

### 9.2. CPV per campaign (Global tab — Campaign Portfolio Table)

Tính trên backend sau khi aggregate (`global_dashboard.go`):

```
cashValid[campaign] = totalCashCompleted + totalCashPending + totalCashWaiting
totalViewsNet       = SUM(view.total) - SUM(view.rejected)

CPV = ROUND(cashValid / totalViewsNet × 100) / 100

Nếu totalViewsNet = 0 → CPV = 0
```

> Tử số là `cashValid` (loại trừ rejected) — **nhất quán với KPI card** từ v2.8.0.

**Bộ lọc**: theo từng campaign riêng lẻ, không có date range

### 9.3. Danh sách Chiến dịch (Campaign Portfolio Table) — Logic chi tiết

**Nguồn**: Collection `events` — toàn bộ campaigns (không filter theo status), sort `status ASC, name ASC` → active-first.

| Cột | Công thức |
|-----|-----------|
| Videos | `SUM(totalContent) - SUM(totalContentRejected)` (net) |
| Views | `SUM(view.total) - SUM(view.rejected)` (net) |
| budgetUsed | `totalCashCompleted + totalCashPending + totalCashWaiting` (cashValid) |
| CPV | `cashValid / viewsNet` |

> Tất cả campaigns hiển thị, kể cả inactive/expired.

---

**Ý nghĩa kinh doanh**:
- Đo lường hiệu quả chi phí: **CPV càng thấp = càng hiệu quả**
- Kết hợp với Tỷ lệ tương tác để đánh giá chất lượng (CPV thấp + Tương tác cao = tối ưu)

**Lưu ý**:
- Hiển thị "---" nếu Lượt xem = 0 hoặc chưa có data
- CPV per platform **không hiển thị** trên UI hiện tại

---

## 10. Duyệt nội dung (Approval)

> **Phạm vi**: Tab Overview — lọc theo Campaign + date range.

### 10.1. Tỷ lệ duyệt (Approval Rate)

**Cách tính**:
```
Tỷ lệ duyệt = ROUND(Video đã duyệt / Tổng video, 2)
            = math.Round(approved / total * 100) / 100

Ví dụ: 362 đã duyệt / 403 tổng = 89.83%
```

> **Nguồn dữ liệu**: Collection `contents` (không phải `content_flow`), group theo field `status`.
> Pipeline: `GetOverallApprovalWithCondPipeline` → `ContentDAO`

**Các trạng thái** (giá trị trong field `status`):

| Trạng thái | Giá trị DB | Ý nghĩa |
|-----------|------------|---------|
| Đã duyệt (Approved) | `approved` | Video đạt tiêu chuẩn |
| Chờ duyệt (Pending) | `waiting_approved` | Video đang chờ review (trong Overall pipeline) |
| Từ chối (Rejected) | `rejected` | Video không đạt yêu cầu |

> **Lưu ý**: Trong pipeline Overall, `pending` được tính là `status = "waiting_approved"`.
> Trong pipeline ByPlatform, `pending` được tính là `status = "pending"`.

**Hiển thị**:
```
[■■■■■■■■■ 89.8% Đã duyệt][■ 5% Chờ duyệt][■ 5.2% Từ chối]
Đã duyệt: 89.8% (362)
Chờ duyệt: 5% (20)
Từ chối: 5.2% (21)
```

> Mỗi badge hiển thị cả % lẫn số video tuyệt đối. Tooltip cũng hiển thị `"Approved: 89.8% (362)"`.

### 10.2. Tỷ lệ duyệt theo nền tảng

Group theo field `platform` (không phải `source`):
```
ApprovalRate per platform = approved / total * 100 (nếu total > 0, else 0)
```

> Pipeline: `GetPlatformApprovalWithCondPipeline`, sort theo `total DESC`

---

### 10.3. Lý do từ chối (Rejection Reasons)

**Nguồn dữ liệu**: Collection `contents`, field `reason` (không phải `rejectReason`) — filter `status = "rejected"` AND `reason != ""`, group by `reason`, count, sort DESC, lấy top 10.

> Pipeline: `GetTopRejectionReasonsWithCondPipeline`

**Ý nghĩa kinh doanh**:
- Cải thiện guideline communication để giảm tỷ lệ từ chối
- Training influencer hiệu quả hơn dựa trên lý do thực tế
- Giảm tỷ lệ từ chối → Tăng hiệu quả (ít revision, ít delay)

---

## Phần C — Chỉ số Chuyển khoản (Tab Admin)

> **Bộ lọc**: Dành cho finance/admin team. Hiển thị theo đợt chuyển khoản (batch), không lọc theo campaign hay time period như Phần B.

---

## 11. Chuyển khoản (Transfer)

> **Nguồn dữ liệu**: Collection `transfers` (không phải `cash_flow`), mỗi document = 1 batch chuyển khoản. Các chỉ số được lấy trực tiếp từ field `statistic` đã pre-computed trên mỗi document.

### 11.1. Thống kê chuyển khoản (Transfer Statistics)

#### Tổng đợt (Total Transfers)
- Số batch chuyển khoản trong khoảng thời gian
- `TotalTransfers = COUNT(documents trong collection transfers)`

#### Tổng yêu cầu (Total Requests)
- Tổng số lượt yêu cầu trong tất cả batch
- `TotalRequests = SUM(transfers[].statistic.requestTotal)`

#### Yêu cầu thành công (Successful Requests)
- Tổng số yêu cầu hoàn tất thành công
- `TotalRequestSuccess = SUM(transfers[].statistic.requestSuccessTotal)`

#### Tỷ lệ thành công (Success Rate)
```
Tỷ lệ thành công = (TotalRequestSuccess / TotalRequests) × 100%
```

---

### 11.2. Chỉ số tiền chuyển khoản

| Chỉ số | Field nguồn | Ý nghĩa |
|--------|-------------|---------|
| Tổng tiền yêu cầu | `SUM(statistic.cashRequestTotal)` | Tổng tiền trong tất cả batch |
| Tiền thành công | `SUM(statistic.cashRequestSuccessTotal)` | Tiền đã chuyển thành công |
| Tiền đang chờ | `SUM(statistic.cashRequestPendingTotal)` | Tiền đang chờ xử lý |
| Tiền bị từ chối | `SUM(statistic.cashRejectedTotal)` | Tiền bị từ chối |

---

### 11.3. Trạng thái chuyển khoản (Transfer Status)

| Trạng thái | Nhãn | Màu | Ý nghĩa |
|--------|-------|-----|---------|
| `draft` | Nháp | Xám | Chưa hoàn thiện, đang soạn |
| `new` | Mới | Xanh dương | Batch mới được tạo |
| `pending` | Chờ xử lý | Vàng đất | Đợi approve từ admin |
| `processing` | Đang xử lý | Vàng | Đang xử lý lệnh chuyển |
| `processed` | Đã xử lý | Tím | Hoàn tất xử lý phía hệ thống |
| `transferring` | Đang chuyển | Cam | Đang thực hiện chuyển khoản ngân hàng |
| `transferred` | Đã chuyển | Xanh lơ | Đã chuyển tiền thành công |
| `finished` | Hoàn thành | Xanh lá | Toàn bộ quy trình hoàn tất |
| `rejected` | Từ chối | Đỏ | Bị từ chối, không chuyển |

**Ý nghĩa kinh doanh**:
- Tracking payment workflow end-to-end
- Đảm bảo influencer được thanh toán đúng hạn
- Audit trail cho finance team
- Phát hiện bottleneck trong quy trình (VD: nhiều batch bị kẹt ở `pending`)

---

---

## Phần D — Xuất dữ liệu (Export)

---

## 12. Chức năng Xuất dữ liệu

Cho phép xuất dữ liệu dashboard theo bộ lọc hiện tại ra file Excel (XLSX) hoặc CSV.

### 12.1. Cách sử dụng

1. Chọn bộ lọc (chiến dịch, khoảng thời gian, creator) trên giao diện
2. Nhấn nút **Xuất dữ liệu**
3. Chọn định dạng file: **XLSX** (một file nhiều sheet) hoặc **CSV** (file ZIP chứa nhiều CSV)
4. Chọn loại dữ liệu cần xuất (có thể chọn nhiều)
5. Nhấn **Xuất** → hệ thống tạo file bất đồng bộ → tự động chuyển sang trang **Dữ liệu** trong Admin để tải về

> **Lưu ý**: File được tạo ở background (bất đồng bộ). Sau khi nhấn Xuất, trang tự động chuyển sang Admin/Data sau 1.5 giây để xem tiến trình.

---

### 12.2. Loại dữ liệu xuất

| Loại | Sheet/File | Nguồn dữ liệu | Bộ lọc áp dụng |
|------|-----------|---------------|----------------|
| **Chiến dịch** (`campaigns`) | Sheet "campaigns" | Collection `event_analytic_daily` (cùng pipeline với UI) | Event IDs, Date range (`date`) |
| **Creator** (`creators`) | Sheet "creators" | Collection `user_events` | Event IDs, Partner, Creator IDs (`user $in`), Date range (`createdAt`) |
| **Thanh toán** (`payments`) | Sheet "payments" | Collection `transfers` | Partner, Event IDs (`event $in`), Date range (`createdAt`) |
| **Nội dung** (`contents`) | Sheet "contents" | Collection `contents` | Event IDs, Partner, Creator IDs (`createdBy $in`), Date range (`createdAt`) |

---

### 12.3. Định dạng file

#### XLSX (Excel)
- **1 file `.xlsx`** chứa nhiều sheet, mỗi sheet = 1 loại dữ liệu đã chọn
- Có thêm sheet **"Export Info"** chứa metadata (tên xuất, ngày xuất, bộ lọc đã dùng)
- Tên file: `{tên_xuất}_{DD_MM_YYYY_HH_MM_SS}.xlsx`

#### CSV
- **1 file `.zip`** chứa nhiều file CSV, mỗi file = 1 loại dữ liệu đã chọn
- Tên các file bên trong: `campaigns.csv`, `creators.csv`, `payments.csv`, `contents.csv`
- Tên file zip: `{tên_xuất}_{DD_MM_YYYY_HH_MM_SS}.zip`

---

### 12.4. Các cột dữ liệu

#### Sheet Chiến dịch (Campaigns)

> **Nguồn**: Dùng cùng pipeline với UI (`GetFilteredCampaignsFromDailyPipeline` — bắt đầu từ `event_analytic_daily`, group by event, lookup `events`). Metrics được tính theo **date range đã chọn**, không phải all-time.

| Cột | Mô tả | Công thức |
|-----|-------|-----------|
| STT | Số thứ tự | — |
| Tên chiến dịch | Tên campaign | `event.name` |
| Trạng thái | Trạng thái campaign | `event.status` |
| Số video | Video hợp lệ (không tính bị từ chối) | `totalContent - totalContentRejected` |
| Lượt xem | Tổng lượt xem (bao gồm rejected views) | `SUM(statistic.view.total)` |
| Ngân sách | Ngân sách được phân bổ | `event.budget` |
| Ngân sách đã dùng | Chi phí hợp lệ (loại rejected) | `SUM(cash.total) - SUM(cash.rejected)` |
| CPV | Chi phí/lượt xem hợp lệ | `cashNotRejected / viewsNotRejected`, làm tròn 2 chữ số |

#### Sheet Creator

| Cột | Mô tả |
|-----|-------|
| STT | Số thứ tự |
| Tên Creator | `user.name` (join từ users collection) |
| User ID | `userEvent.user` (ObjectID) |
| Nền tảng | "Multiple" |
| Số video | `userEvent.statistic.totalContentApproved` |
| Lượt xem | Tổng TikTok + YouTube + Facebook views |
| Lượt thích | Tổng TikTok + YouTube + Facebook likes |
| Engagement (%) | (Thích / Lượt xem) × 100 |
| Thanh toán | `userEvent.statistic.cashTotal.completed` |
| Hoàn tiền | `userEvent.statistic.cashBonus.completed` |

#### Sheet Thanh toán (Payments)

| Cột | Mô tả |
|-----|-------|
| STT | Số thứ tự |
| Tên Creator | `transfer.name` |
| Video được duyệt | `transfer.statistic.requestSuccessTotal` |
| Tổng lượt xem | (tạm thời = 0, cần aggregate) |
| Số tiền thanh toán | `transfer.statistic.cashRequestSuccessTotal` |
| Hoàn tiền | (tạm thời = 0) |
| Trạng thái | `transfer.status` |
| Ngày chuyển | `transfer.createdAt` |

#### Sheet Nội dung (Contents)

| Cột | Mô tả |
|-----|-------|
| STT | Số thứ tự |
| Content ID | `content._id` |
| Creator | `content.author` |
| Nền tảng | `content.source` |
| Lượt xem | `content.statistic.view.total` |
| Lượt thích | `content.statistic.like.total` |
| Bình luận | `content.statistic.comment.total` |
| Trạng thái | `content.status` |
| Ngày tạo | `content.createdAt` |

---

### 12.5. Bộ lọc áp dụng khi xuất

Bộ lọc được lấy từ trạng thái bộ lọc **hiện tại** trên giao diện dashboard tại thời điểm nhấn Xuất:

| Bộ lọc | Field gửi lên | Cách xử lý backend |
|--------|--------------|-------------------|
| Chiến dịch | `events: string[]` (mảng Event ObjectID) | `$in` query trên field tương ứng |
| Creator | `users: string[]` (mảng User ObjectID) | `$in` query trên `user` / `createdBy` |
| Từ ngày | `fromAt: string` (ISO 8601 full, ví dụ `"2026-01-25T00:00:00.000Z"`) | `createdAt >= fromAt` |
| Đến ngày | `toAt: string` (ISO 8601 full, ví dụ `"2026-02-25T23:59:59.999Z"`) | `createdAt <= toAt` |

> **Lưu ý**: Nếu không chọn chiến dịch cụ thể (All Campaigns), `events` = `[]` → **không filter** → lấy toàn bộ.
> Nếu không chọn creator, `users` = `[]` → lấy tất cả creator.

---

### 12.6. Giới hạn

- Tối đa **50.000 dòng** mỗi loại dữ liệu (`MaxExportRows = 50000`)
- File được tạo ở background, trạng thái: `waiting` → `running` → `completed` / `failed`
- Tối đa **2 file** đang xử lý đồng thời (queue-based)
- File lưu trên MinIO, link tải có hiệu lực **15 phút** (presigned URL)

---

### 12.7. Loại export (Type) trong Admin

Trong trang Admin > Dữ liệu, cột **Loại** hiển thị nhãn tương ứng:

| Type (DB) | Nhãn hiển thị |
|-----------|--------------|
| `dashboard_multi` | Dashboard - Tổng hợp |
| `dashboard_campaigns` | Dashboard - Chiến dịch |
| `dashboard_creators` | Dashboard - Creator |
| `dashboard_payments` | Dashboard - Thanh toán |
| `creator_analytics` | Thống kê creator |
| `transfer_user_cash` | Chuyển tiền người dùng |
| `content` | Nội dung |
| `reconciliation_item` | Đối soát |
| `transfer_withdraw` | Rút tiền |

---

## 13. Xu hướng (Trend Indicators)

### 12.1. Cách tính Trend

**So sánh**: Kỳ hiện tại vs. cùng kỳ liền trước

```
change = ((current - previous) / previous) × 100

Nếu previous = 0 và current > 0 → change = 100, direction = "up"
Nếu previous = 0 và current = 0  → change = 0,   direction = "flat"

Trend% = TRUNC(|change| × 100) / 100  (làm tròn 2 chữ số, bỏ dấu âm)
```

> Mặc định: filter 30 ngày → so sánh với 30 ngày liền trước đó.

> Hàm `calculateTrend(previous, current)` trong `dashboard_analytics.go`

### 12.2. Các loại xu hướng

| Loại | Điều kiện (change) | Direction | Màu |
|------|--------------------|-----------|-----|
| Tăng ↑ | change > +0.5% | `"up"` | Xanh lá |
| Không đổi → | -0.5% ≤ change ≤ +0.5% | `"flat"` | Xám |
| Giảm ↓ | change < -0.5% | `"down"` | Đỏ |

> **Lưu ý**: Ngưỡng ±0.5% — thay đổi nhỏ hơn 0.5% được coi là "flat" (không đổi), không phải "up"/"down".

**Hiển thị**:
```
↑ +15.3%  (Tăng)
↓ -5.2%   (Giảm)
→ 0%      (Không đổi)
```

---

## 13. Xếp hạng (Rank)

**Cơ sở xếp hạng**: Mặc định theo Tổng lượt xem, có thể đổi sang Video, Thích, Chia sẻ, Thanh toán.

**Hiển thị**:
- Top 3: 🥇🥈🥉
- Hạng 4+: Number badge

---

## 14. Định dạng hiển thị (Format & Display)

### 14.1. Định dạng số

| Hàm | Ví dụ |
|-----|-------|
| Số thường | `1,234,567` |
| Số rút gọn | `1.2M` / `50K` |
| Tiền tệ | `1,234,567₫` / `1.2M₫` |
| Phần trăm | `15.3%` |

### 14.2. Màu sắc

#### KPI Colors
```
Video:        Xanh lá (#22C55E)
Lượt xem:     Tím (#A855F7)
Ngân sách:    Cam (#F97316)
CPV:          Hồng (#EC4899)
Tương tác:    Tím đậm (#8B5CF6)
Thanh toán:   Hổ phách / Ngọc lục bảo
```

#### Platform Colors
```
Facebook:  #1877F2
YouTube:   #FF0000
TikTok:    #000000 (sáng) / #FFFFFF (tối)
Instagram: #E4405F
```

---

## 15. Giao diện responsive

| Màn hình | Layout |
|----------|--------|
| Desktop (lg+) | 4 cột: [KPI 1][KPI 2][KPI 3][KPI 4] |
| Tablet (md) | 2 cột: [KPI 1][KPI 2] / [KPI 3][KPI 4] |
| Mobile | 1 cột: mỗi KPI một hàng |

---

## 16. Trạng thái tải và lỗi

- **Đang tải**: Skeleton placeholder giữ layout ổn định
- **Lỗi**: Icon cảnh báo + "Không thể tải dữ liệu" + nút "Thử lại"
- **Không có dữ liệu**: Hiển thị "---" hoặc "Không có dữ liệu"

---

## 17. Hướng dẫn đọc chỉ số

### 17.1. Nguyên tắc
1. **Context is key**: Luôn xem context (campaign, time range, nền tảng)
2. **So sánh xu hướng**: So sánh với kỳ trước, không chỉ nhìn số tuyệt đối
3. **Kết hợp chỉ số**: Nhiều chỉ số cùng nhau mới cho insight đúng

### 17.2. Action Items theo từng chỉ số
- **CPV cao**: Review content quality, tối ưu targeting, chuyển ngân sách sang nền tảng có CPV thấp hơn
- **Tỷ lệ tương tác thấp**: Cải thiện guideline, training influencer, thử format video mới
- **Tỷ lệ hoạt động thấp**: Khảo sát influencer, cải thiện incentive, giảm rào cản tham gia
- **Tỷ lệ từ chối cao**: Làm rõ guideline, cung cấp ví dụ, hỗ trợ 1-on-1 creator
- **Tốc độ sử dụng > 85%**: Cân nhắc tạm dừng ngân sách, xem lại phân bổ

---

## 18. Thuật ngữ (Glossary)

| Tiếng Việt | English | Viết tắt | Định nghĩa |
|------------|---------|----------|------------|
| Lượt xem | Views | - | Tổng số lần video được phát |
| Tỷ lệ tương tác | Engagement Rate | ER | (Thích + Bình luận) / Lượt xem × 100% (Shares = 0, không có trong schema) |
| Chi phí trên mỗi lượt xem | Cost Per View | CPV | (cash.total - cash.rejected) / (view.total - view.rejected) — KPI card loại trừ rejected ở cả tử và mẫu |
| Tỷ lệ hoạt động | Activity Rate | - | COUNT(DISTINCT user IN contents trong kỳ) / Tổng creators × 100% |
| Tỷ lệ nghỉ | Churn Rate | - | 100% - Tỷ lệ hoạt động |
| Tốc độ sử dụng ngân sách | Burn Rate | - | % ngân sách đã dùng (= Percentage, alias của cashValid/budget × 100%). Không phải VND/ngày. |
| Tỷ lệ duyệt | Approval Rate | - | Video đã duyệt / Tổng video submit × 100% |
| Influencer mới | New Influencers | - | Users có createdAt trong kỳ hiện tại |
| Tổng phí quảng cáo | Total Ad Spend | - | Tổng tiền thưởng đã chi cho influencer |

---

## 19. Cấu trúc API

### 19.1. Dashboard KPI Response
```typescript
GET /api/admin/analytics/dashboard?eventId=...&startDate=...&endDate=...

{
  "kpis": {
    "videos":     { "total": 362, "approved": 325, "pending": 20, "rejected": 17, "trend": { "value": 12.5, "direction": "up" } },
    "views":      { "total": 469835, "trend": { "value": 45.2, "direction": "up" } },
    "budget":     { "allocated": 100000000, "spent": 65000000, "remaining": 35000000, "percentage": 65, "burnRate": 65 },
    "cpv":        { "value": 138, "trend": { "value": -8.3, "direction": "down" } },
    "engagement": { "rate": 7.9, "trend": { "value": 5.1, "direction": "up" } },
    "payment":    { "total": 65000000, "byPlatform": { "facebook": 22000000, "youtube": 28000000, "tiktok": 15000000 } }
  },
  "interactions": { "views": 469835, "likes": 31131, "comments": 3765, "shares": 0 }
}
```

### 19.2. Platform Analytics Response
```typescript
GET /api/admin/analytics/platforms?eventId=...

{
  "platforms": [
    { "name": "youtube",  "views": 198500, "cost": 28000000, "cpv": 141, "videos": { "total": 139, "approved": 130, "rejected": 9 } },
    { "name": "facebook", "views": 156200, "cost": 22000000, "cpv": 141, "videos": { "total": 115, "approved": 100, "rejected": 15 } },
    { "name": "tiktok",   "views": 115135, "cost": 15000000, "cpv": 130, "videos": { "total": 108, "approved": 95,  "rejected": 13 } }
  ],
  "totals": { "videos": 362, "views": 469835, "cost": 65000000, "avgCpv": 138 }
}
```

### 19.3. Creator Segments Response
```typescript
GET /api/admin/analytics/creators/segments?eventId=...

{
  "total": 1328,
  "segments": {
    "participating": { "count": 324, "percentage": 24.4 },
    "inactive":      { "count": 180, "percentage": 13.6 },
    "new":           { "count": 85,  "percentage": 6.4  },
    "returning":     { "count": 59,  "percentage": 4.4  }
  },
  "participationRate": 24.4
}
```

---

## 20. Câu hỏi thường gặp (FAQs)

### Q1: Tại sao Lượt xem và Tương tác không khớp?
**A**: Tương tác chỉ tính interaction (thích, bình luận, chia sẻ), không bao gồm passive views.

### Q2: CPV âm có nghĩa gì?
**A**: Không thể có CPV âm. Nếu hiển thị "---", nghĩa là chưa có data hoặc Lượt xem = 0.

### Q3: Tại sao "Lần đầu + Quay lại" ≠ "Tham gia"?
**A**: Không xảy ra — "Lần đầu" và "Quay lại" là subset của "Tham gia", tổng luôn bằng "Tham gia". Nếu có sai lệch là do lỗi data.

### Q4: Trend so sánh với kỳ nào?
**A**: Mặc định so với cùng kỳ liền trước. Ví dụ: filter 30 ngày → so sánh với 30 ngày liền trước đó.

### Q5: Tổng phí quảng cáo khác gì Ngân sách đã dùng?
**A**: Về giá trị thường bằng nhau. Tuy nhiên Ngân sách được phân bổ là con số lớn hơn — đây là ngân sách được phê duyệt ban đầu, chưa chắc đã chi hết.

### Q6: Nền tảng nào hiệu quả nhất?
**A**: Cần xem kết hợp CPV + Tỷ lệ tương tác + Mục tiêu kinh doanh. TikTok thường có CPV thấp nhất nhưng đối tượng khác với YouTube/Facebook. Không có câu trả lời chung.

---

## 21. Lịch sử thay đổi (Change Log)

| Phiên bản | Ngày | Thay đổi |
|-----------|------|----------|
| 1.0.0 | 2024-02-14 | Initial documentation |
| 2.0.0 | 2026-02-24 | Cập nhật toàn bộ công thức tính chính xác từ PRD v2.1, bổ sung nguồn dữ liệu MongoDB, ví dụ thực tế, phân loại creator segments, FAQ mở rộng |
| 2.1.0 | 2026-02-24 | Rà soát lại 4 KPI global từ source code backend: sửa định nghĩa Influencer mới (đăng ký tài khoản), Tỷ lệ hoạt động (distinct users submit content), Tỷ lệ nghỉ (= 100% - Tỷ lệ hoạt động) |
| 2.2.0 | 2026-02-24 | Chuẩn hóa toàn bộ tên chỉ số theo format "Tiếng Việt (English)" theo i18n |
| 2.3.0 | 2026-02-24 | Rà soát và sửa section 10-12: Collection Approval là `contents` (không phải `content_flow`), field lý do từ chối là `reason` (không phải `rejectReason`), Transfer lấy từ collection `transfers` (không phải `cash_flow`), Trend ngưỡng flat ±0.5%, Glossary sửa Burn Rate và Engagement Rate |
| 2.4.0 | 2026-02-24 | Sửa section 2.3 Activity Rate: nguồn dữ liệu là collection `contents` field `user` (không phải `content_flow` field `createdBy`) — xác nhận từ source code `global_dashboard.go` |
| 2.5.0 | 2026-02-24 | Sửa section 9.1 CPV KPI card: tử số là `cash.total - cash.rejected` (cashValid), mẫu số là `view.total - view.rejected` — cả hai loại trừ rejected, xác nhận từ `dashboard_analytics.go` |
| 2.6.0 | 2026-02-24 | Sửa section 5.1 Total Ad Spend: KPI card hiển thị cashValid (loại trừ rejected), không phải cash.total. Note rõ `cash.completed` trong API response là misleading name — thực chất = cashValid |
| 2.7.0 | 2026-02-24 | Phase 01: Migrate videosByPlatform từ content_flow → event_analytic_daily (có date filter). Phase 03: Loại Shares khỏi Engagement formula và widget. Section 3.1 Total Videos dùng net (loại rejected). Section 3.2 Card videosByPlatform dùng event_analytic_daily |
| 2.8.0 | 2026-02-24 | Phase 04: Campaign Portfolio Table — Videos/Views/budgetUsed/CPV đều dùng net values. Thêm section 9.3. Phase 05: Timeline Views/Videos loại rejected. Phase 06: Interaction widget ẩn Shares. Phase 07: Budget widget xóa Burn Rate block (alias của Used%). Phase 08: Approval chart hiển thị counts bên cạnh %. Phase 09: Platform donut chart dùng net video counts, tính lại % client-side. Phase 11: Creator KPI cards + bảng Danh sách Influencer loại rejected |
| 2.9.0 | 2026-02-25 | Thêm Phần D — Xuất dữ liệu (section 12): mô tả chức năng export, các loại dữ liệu (campaigns/creators/payments/contents), định dạng file (XLSX/CSV+ZIP), bộ lọc áp dụng, giới hạn, bảng cột dữ liệu, và mapping type → nhãn hiển thị trong Admin |
| 2.10.0 | 2026-02-25 | Cập nhật section 12.2 & 12.4: Export campaigns nay dùng cùng pipeline với UI (`GetFilteredCampaignsFromDailyPipeline` từ `event_analytic_daily`, filter theo `date` range). Bảng cột campaigns: bỏ cột Engagement, Ngày tạo, Số creators; thêm Ngân sách đã dùng với công thức đúng. Videos = net (loại rejected). CPV tính đúng (cashNotRejected / viewsNotRejected) |

---

## 22. Liên hệ & Hỗ trợ

- **Technical Issues**: Contact Dev Team
- **Business Questions**: Contact Marketing Team
- **Data Accuracy**: Contact Analytics Team

---

**Lưu ý**: Tài liệu này được cập nhật dựa trên PRD TCB Creator Analytics Dashboard v2.1 (2026-01-30) và phân tích source code. Vui lòng cập nhật khi có thay đổi trong business logic.
