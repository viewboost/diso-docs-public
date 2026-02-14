# Tài liệu Chỉ số Dashboard T-Fluencers

## Mục lục
- [1. Tổng quan](#1-tổng-quan)
- [2. Chỉ số Creator (Influencer)](#2-chỉ-số-creator-influencer)
- [3. Chỉ số Video](#3-chỉ-số-video)
- [4. Chỉ số Views (Lượt xem)](#4-chỉ-số-views-lượt-xem)
- [5. Chỉ số Thanh toán (Payment)](#5-chỉ-số-thanh-toán-payment)
- [6. Chỉ số Engagement (Tương tác)](#6-chỉ-số-engagement-tương-tác)
- [7. Chỉ số Platform (Nền tảng)](#7-chỉ-số-platform-nền-tảng)
- [8. Chỉ số Budget (Ngân sách)](#8-chỉ-số-budget-ngân-sách)
- [9. Chỉ số CPV (Cost Per View)](#9-chỉ-số-cpv-cost-per-view)
- [10. Chỉ số Approval (Duyệt nội dung)](#10-chỉ-số-approval-duyệt-nội-dung)
- [11. Chỉ số Transfer (Chuyển khoản)](#11-chỉ-số-transfer-chuyển-khoản)

---

## 1. Tổng quan

Dashboard hiển thị các chỉ số phân tích hiệu quả của chương trình T-Fluencers (Techcombank Influencer Marketing) trên nhiều nền tảng mạng xã hội (Facebook, YouTube, TikTok, Instagram).

### Scope (Phạm vi dữ liệu)
- **Global**: Dữ liệu toàn nền tảng, tất cả chiến dịch
- **Campaign**: Dữ liệu theo từng chiến dịch/thử thách cụ thể
- **Period**: Mặc định 30 ngày gần nhất, có thể tùy chỉnh

---

## 2. Chỉ số Creator (Influencer)

### 2.1. Tổng số Influencer (Total Influencers)
**Tên tiếng Việt**: Tổng số Influencer
**Component**: `GlobalCreatorKPIs`, `CreatorKPICards`
**Icon**: Users (👥)
**Màu sắc**: Blue (#3B82F6)

**Định nghĩa**: Tổng số influencer tham gia chương trình trong khoảng thời gian đã chọn.

**Cách tính**:
```
Tổng số influencer = Số lượng unique creators tham gia
```

**Ý nghĩa kinh doanh**:
- Đo lường quy mô mạng lưới influencer
- Theo dõi sự tăng trưởng cộng đồng creator
- KPI chính để đánh giá độ phủ của chương trình

**Trend (Xu hướng)**:
- ↑ (up): Tăng trưởng so với kỳ trước
- ↓ (down): Giảm so với kỳ trước
- → (neutral): Không đổi

---

### 2.2. Influencer mới (New Influencers)
**Tên tiếng Việt**: Influencer mới
**Component**: `GlobalCreatorKPIs`
**Icon**: UserPlus (👤+)
**Màu sắc**: Green (#22C55E)

**Định nghĩa**: Số lượng influencer mới tham gia lần đầu tiên trong kỳ.

**Cách tính**:
```
New Influencers = Số influencer có lần submit đầu tiên trong kỳ
```

**Ý nghĩa kinh doanh**:
- Đo lường khả năng thu hút influencer mới
- Đánh giá hiệu quả chiến lược acquisition
- Theo dõi tốc độ mở rộng mạng lưới

**Metrics liên quan**:
- First Time (Lần đầu): Influencer tham gia thử thách lần đầu

---

### 2.3. Tỷ lệ hoạt động (Active Rate)
**Tên tiếng Việt**: Tỷ lệ hoạt động
**Component**: `GlobalCreatorKPIs`
**Icon**: Activity (📊)
**Màu sắc**: Violet (#8B5CF6)
**Format**: Percent (%)

**Định nghĩa**: Tỷ lệ influencer đang hoạt động (có submit video) trên tổng số influencer.

**Cách tính**:
```
Active Rate = (Số influencer có submit / Tổng số influencer) × 100%
```

**Ý nghĩa kinh doanh**:
- Đo lường mức độ engagement của influencer với chương trình
- Đánh giá chất lượng mạng lưới (không chỉ số lượng)
- KPI quan trọng cho retention strategy

**Ngưỡng đánh giá**:
- ≥ 70%: Tốt (Green)
- 50-70%: Trung bình (Yellow)
- < 50%: Cần cải thiện (Red)

---

### 2.4. Tỷ lệ nghỉ (Churn Rate)
**Tên tiếng Việt**: Tỷ lệ nghỉ
**Component**: `GlobalCreatorKPIs`
**Icon**: TrendingDown (📉)
**Màu sắc**: Pink (#EC4899)
**Format**: Percent (%)

**Định nghĩa**: Tỷ lệ influencer ngừng tham gia (không submit trong kỳ hiện tại).

**Cách tính**:
```
Churn Rate = (Số influencer không submit / Tổng số influencer) × 100%
```

**Ý nghĩa kinh doanh**:
- Đo lường tỷ lệ mất influencer
- Cảnh báo sớm về vấn đề retention
- Giúp đánh giá sức khỏe của chương trình

**Lưu ý**:
- Churn Rate thấp là tốt (ngược với các chỉ số khác)
- Trend ↓ (giảm) là tích cực

---

## 3. Chỉ số Video

### 3.1. Tổng số Video (Total Videos)
**Tên tiếng Việt**: Tổng số Video
**Component**: `VideoKPI`, `CreatorKPICards`
**Icon**: Video (🎥), FileCheck (✅)
**Màu sắc**: Green (#22C55E)

**Định nghĩa**: Tổng số video được submit bởi influencer.

**Breakdown (Phân tích chi tiết)**:
- **Theo Platform**: Facebook, YouTube, TikTok
- **Theo Status**: Approved (Đã duyệt), Pending (Chờ duyệt), Rejected (Từ chối)

**Hiển thị**:
```
FB: 120 | YT: 85 | TT: 200
✓ Approved | ⏳ Pending | ✗ Rejected
```

**Ý nghĩa kinh doanh**:
- Đo lường sản lượng content
- Tracking campaign performance
- Dự báo payment obligation

---

### 3.2. Video theo Platform
**Component**: `VideoKPI.byPlatform`

**Cấu trúc dữ liệu**:
```typescript
byPlatform: {
  facebook: { total: 120, approved: 100, rejected: 5 }
  youtube: { total: 85, approved: 80, rejected: 2 }
  tiktok: { total: 200, approved: 190, rejected: 8 }
}
```

**Ý nghĩa**:
- So sánh hiệu quả giữa các nền tảng
- Tối ưu resource allocation
- Phát hiện platform có tỷ lệ reject cao

---

## 4. Chỉ số Views (Lượt xem)

### 4.1. Tổng lượt xem (Total Views)
**Tên tiếng Việt**: Tổng lượt xem
**Component**: `CreatorKPICards`, Platform Tables
**Icon**: Eye (👁️)
**Màu sắc**: Purple (#A855F7)

**Định nghĩa**: Tổng số lượt xem trên tất cả video của influencer.

**Cách thu thập**:
- Facebook: Video views
- YouTube: View count
- TikTok: Play count

**Ý nghĩa kinh doanh**:
- Đo lường reach (độ phủ) của campaign
- KPI chính cho brand awareness
- Cơ sở tính CPV (Cost Per View)

**Lưu ý**:
- Views được format theo locale (VD: 1,234,567 hoặc 1.2M)
- Có thể breakdown theo platform

---

## 5. Chỉ số Thanh toán (Payment)

### 5.1. Tổng phí quảng cáo (Total Ad Cost / Total Payment)
**Tên tiếng Việt**: Tổng phí quảng cáo
**Component**: `PaymentKPI`, `CreatorKPICards`
**Icon**: DollarSign ($), Wallet (💰)
**Màu sắc**: Orange (#F97316), Emerald (#10B981)
**Format**: Currency (VND)

**Định nghĩa**: Tổng số tiền chi trả cho influencer theo video đã approved.

**Cách tính**:
```
Total Payment = Σ (Video approved × Payment per video)
```

**Breakdown theo Platform**:
```
Facebook: 50,000,000 VND
YouTube: 30,000,000 VND
TikTok: 20,000,000 VND
```

**Ý nghĩa kinh doanh**:
- Tracking chi phí thực tế của campaign
- So sánh với budget allocation
- Basis để tính ROI (Return on Investment)

**Hiển thị Details**:
- Hover/Click để xem breakdown theo nền tảng
- Popover hiển thị chi tiết thanh toán

---

## 6. Chỉ số Engagement (Tương tác)

### 6.1. Interaction Breakdown (Phân tích tương tác)
**Component**: `InteractionBreakdown`

**Các loại tương tác**:

#### 6.1.1. Lượt xem (Views)
- **Icon**: Eye (👁️)
- **Màu**: Blue (#3B82F6)
- Không tính % (vì là base metric)

#### 6.1.2. Thích (Likes)
- **Icon**: Heart (❤️)
- **Màu**: Red (#EF4444)
- **Cách tính**: `(Likes / Views) × 100%`

#### 6.1.3. Bình luận (Comments)
- **Icon**: MessageCircle (💬)
- **Màu**: Amber (#F59E0B)
- **Cách tính**: `(Comments / Views) × 100%`

#### 6.1.4. Chia sẻ (Shares)
- **Icon**: Share2 (🔁)
- **Màu**: Green (#22C55E)
- **Cách tính**: `(Shares / Views) × 100%`

---

### 6.2. Tỷ lệ tương tác (Engagement Rate)
**Formula**:
```
Engagement Rate = ((Likes + Comments + Shares) / Views) × 100%
```

**Ý nghĩa kinh doanh**:
- Đo lường chất lượng content
- Đánh giá mức độ viral của video
- So sánh hiệu quả giữa các influencer/platform

**Benchmark**:
- Facebook: 1-3% (Tốt)
- YouTube: 3-5% (Tốt)
- TikTok: 5-10% (Tốt)

---

### 6.3. Average Engagement (Tương tác trung bình)
**Component**: Platform Columns
**Field**: `avgEngagement`
**Format**: Percent (%)

**Định nghĩa**: Tỷ lệ engagement trung bình trên tất cả video của platform.

---

## 7. Chỉ số Platform (Nền tảng)

### 7.1. Platform Statistics
**Component**: `PlatformStatsCard`, `PlatformTable`

**Các nền tảng hỗ trợ**:
- **Facebook**: Màu #1877F2 (Blue)
- **YouTube**: Màu #FF0000 (Red)
- **TikTok**: Màu #000000 / #FFFFFF (Black/White)
- **Instagram**: Màu #E4405F (Pink/Gradient)

**Chỉ số theo Platform**:
1. **Total Creators**: Số influencer trên platform
2. **Total Videos**: Tổng video trên platform
3. **Total Views**: Tổng lượt xem
4. **Total Payment**: Tổng thanh toán
5. **Avg Engagement**: Engagement trung bình
6. **Cost**: Chi phí (nếu có)
7. **CPV**: Cost per view (nếu có)

---

### 7.2. Platform Dot (Biểu tượng Platform)
**Component**: `PlatformDot`

Visual indicator để nhận diện nhanh platform:
- Small colored dot
- Ring border effect
- Platform-specific colors

---

## 8. Chỉ số Budget (Ngân sách)

### 8.1. Budget Widget
**Component**: `BudgetWidget`
**Card Title**: "Tổng quan Ngân sách"

**Các chỉ số**:

#### 8.1.1. Đã sử dụng (Used)
- Số tiền đã chi từ budget
- Format: VND currency

#### 8.1.2. Tổng (Total)
- Tổng ngân sách được phân bổ
- Format: VND currency

#### 8.1.3. Còn lại (Remaining)
- `Remaining = Total - Used`
- Số tiền budget còn available

#### 8.1.4. Tốc độ sử dụng (Burn Rate)
**Formula**:
```
Burn Rate = (Used / Total) × 100%
```

**Color Coding**:
- ≤ 70%: 🟢 Green (An toàn)
- 71-85%: 🟡 Yellow (Cảnh báo)
- > 85%: 🔴 Red (Nguy hiểm)

---

### 8.2. Budget Progress Bar
**Visual**: Horizontal progress bar với gradient color

**Hiển thị**:
- Percentage trên cùng (VD: "75%")
- Progress bar có màu động theo threshold
- 3 stat boxes: Used | Total | Remaining

**Ý nghĩa kinh doanh**:
- Kiểm soát chi phí real-time
- Cảnh báo khi sắp hết budget
- Planning cho phase tiếp theo

---

## 9. Chỉ số CPV (Cost Per View)

### 9.1. CPV Definition
**Tên đầy đủ**: Cost Per View
**Tên tiếng Việt**: Chi phí trên mỗi lượt xem
**Component**: Platform Columns
**Format**: VND (đồng)

**Formula**:
```
CPV = Total Payment / Total Views
```

**Ví dụ**:
```
Payment: 100,000,000 VND
Views: 5,000,000
CPV = 100,000,000 / 5,000,000 = 20đ/view
```

**Ý nghĩa kinh doanh**:
- Đo lường hiệu quả chi phí
- So sánh với các kênh marketing khác
- Benchmark giữa các platform
- Tối ưu budget allocation

**Benchmark CPV** (Tham khảo):
- Facebook: 10-30đ/view
- YouTube: 20-50đ/view
- TikTok: 5-20đ/view

**Lưu ý**:
- CPV thấp không phải lúc nào cũng tốt (cần xem quality)
- Cần kết hợp với Engagement Rate để đánh giá
- Hiển thị "---" nếu không có data

---

## 10. Chỉ số Approval (Duyệt nội dung)

### 10.1. Approval Chart
**Component**: `ApprovalChart`
**Chart Type**: Horizontal Stacked Bar

**Các trạng thái**:

#### 10.1.1. Đã duyệt (Approved)
- **Màu**: Green (#22C55E)
- **Label**: "Đã duyệt"
- Video đạt tiêu chuẩn, được thanh toán

#### 10.1.2. Chờ duyệt (Pending)
- **Màu**: Yellow (#EAB308)
- **Label**: "Chờ duyệt"
- Video đang chờ review

#### 10.1.3. Từ chối (Rejected)
- **Màu**: Red (#EF4444)
- **Label**: "Từ chối"
- Video không đạt yêu cầu

**Format hiển thị**:
```
[■■■■■■ 70% Approved][■■ 20% Pending][■ 10% Rejected]
```

---

### 10.2. Rejection Reasons (Lý do từ chối)
**Component**: `RejectionReasons`

**Các lý do phổ biến**:
1. Vi phạm guideline
2. Chất lượng video kém
3. Nội dung không phù hợp
4. Sai format/spec
5. Thiếu disclosure

**Chức năng**:
- Click vào reason → Filter content list
- Hiển thị số lượng từ chối theo reason
- Giúp identify vấn đề chính

**Ý nghĩa kinh doanh**:
- Cải thiện guideline communication
- Training influencer hiệu quả hơn
- Giảm rejection rate → Tăng efficiency

---

## 11. Chỉ số Transfer (Chuyển khoản)

### 11.1. Transfer Statistics
**Component**: `TransferTable`, `TransferColumns`

**Các chỉ số chính**:

#### 11.1.1. Yêu cầu (Request Total)
- Tổng số request chuyển khoản
- Format: Number với comma separator

#### 11.1.2. Thành công (Request Success Total)
- Số request được xử lý thành công
- **Màu**: Green (#22C55E)

#### 11.1.3. Tỷ lệ (Success Rate)
**Formula**:
```
Success Rate = (Success Total / Request Total) × 100%
```

**Color Coding**:
- ≥ 80%: 🟢 Green
- 50-79%: 🟡 Yellow
- < 50%: 🔴 Red

---

### 11.2. Transfer Cash Metrics

#### 11.2.1. Tổng tiền (Cash Request Total)
- Tổng số tiền trong batch transfer
- Format: VND currency

#### 11.2.2. Đã thanh toán (Cash Request Success Total)
- Số tiền đã chuyển thành công
- **Màu**: Green (#22C55E)
- **Font**: Bold

---

### 11.3. Transfer Status
**Các trạng thái trong workflow**:

| Status | Label | Màu | Ý nghĩa |
|--------|-------|-----|---------|
| `draft` | Nháp | Gray | Chưa hoàn thiện |
| `new` | Mới | Blue | Mới tạo |
| `pending` | Chờ xử lý | Amber | Đợi approve |
| `processing` | Đang xử lý | Yellow | Đang chuyển |
| `processed` | Đã xử lý | Purple | Hoàn tất xử lý |
| `transferring` | Đang chuyển | Orange | Đang transfer |
| `transferred` | Đã chuyển | Teal | Đã chuyển tiền |
| `finished` | Hoàn thành | Green | Hoàn tất |
| `rejected` | Từ chối | Red | Bị từ chối |

**Ý nghĩa kinh doanh**:
- Tracking payment workflow
- Đảm bảo influencer được thanh toán đúng hạn
- Audit trail cho finance team
- Identify bottleneck trong process

---

## 12. Trend Indicators (Chỉ số xu hướng)

### 12.1. Trend Badge
**Component**: `TrendBadge`

**Các loại trend**:

#### Up (↑)
- **Icon**: TrendingUp
- **Màu**: Green
- Tăng so với kỳ trước

#### Down (↓)
- **Icon**: TrendingDown
- **Màu**: Red
- Giảm so với kỳ trước

#### Neutral (→)
- **Icon**: Minus
- **Màu**: Gray
- Không đổi

**Format hiển thị**:
```
↑ +15.3%  (Tăng)
↓ -5.2%   (Giảm)
→ 0%      (Không đổi)
```

---

## 13. Rank (Xếp hạng)

### 13.1. Rank Cell
**Component**: `RankCell`

**Visual**:
- Top 3: Medal icons (🥇🥈🥉)
- Rank 4+: Number badge

**Ý nghĩa**:
- Gamification cho influencer
- Tạo động lực cạnh tranh
- Recognize top performers

---

## 14. Format & Display

### 14.1. Number Formats

#### formatNumber
```typescript
1234567 → "1,234,567"
```

#### formatCompact
```typescript
1234567 → "1.2M"
50000 → "50K"
```

#### formatCurrency
```typescript
1234567 → "1,234,567₫"
// hoặc
1234567 → "1.2M₫"
```

#### formatPercent
```typescript
0.1532 → "15.3%"
```

---

### 14.2. Color Scheme

#### KPI Colors (CSS Variables)
```css
--kpi-videos: Green (#22C55E)
--kpi-views: Purple (#A855F7)
--kpi-budget: Orange (#F97316)
--kpi-cpv: Pink (#EC4899)
--kpi-engagement: Violet (#8B5CF6)
--kpi-payment: Amber/Emerald
```

#### Platform Colors
```css
--facebook: #1877F2
--youtube: #FF0000
--tiktok: #000000 (light) / #FFFFFF (dark)
--instagram: #E4405F
```

---

## 15. Responsive Behavior

### Grid Layouts

#### Desktop (lg+)
```
4 columns: [KPI 1][KPI 2][KPI 3][KPI 4]
```

#### Tablet (md)
```
2 columns: [KPI 1][KPI 2]
           [KPI 3][KPI 4]
```

#### Mobile
```
1 column: [KPI 1]
          [KPI 2]
          [KPI 3]
          [KPI 4]
```

---

## 16. Loading & Error States

### Loading State (Skeleton)
- Hiển thị skeleton placeholders
- Giữ layout không bị shift
- Smooth loading experience

### Error State
- Icon: AlertCircle
- Text: "Không thể tải dữ liệu"
- Action: "Thử lại" button

### No Data State
- Icon: AlertCircle (muted)
- Text: "---" hoặc "Không có dữ liệu"
- Graceful degradation

---

## 17. Best Practices

### 17.1. Đọc hiểu chỉ số
1. **Context is key**: Luôn xem context (campaign, time range, platform)
2. **Compare trends**: So sánh với kỳ trước, không chỉ nhìn số tuyệt đối
3. **Cross-reference**: Kết hợp nhiều chỉ số để có insight đúng

### 17.2. Action Items
- **CPV cao**: Review content quality, optimize targeting
- **Engagement thấp**: Cải thiện guideline, training influencer
- **Churn rate cao**: Survey influencer, improve incentive
- **Rejection rate cao**: Clarify guideline, provide examples

---

## 18. Glossary (Thuật ngữ)

| Tiếng Việt | English | Viết tắt | Định nghĩa |
|------------|---------|----------|------------|
| Tổng lượt xem | Total Views | - | Tổng số lần video được xem |
| Tỷ lệ tương tác | Engagement Rate | ER | % tương tác trên lượt xem |
| Chi phí trên lượt xem | Cost Per View | CPV | Chi phí / lượt xem |
| Tỷ lệ hoạt động | Active Rate | - | % influencer có hoạt động |
| Tỷ lệ nghỉ | Churn Rate | - | % influencer ngừng tham gia |
| Tốc độ sử dụng | Burn Rate | - | % budget đã sử dụng |

---

## 19. API Data Structure

### 19.1. Global Analytics Response
```typescript
interface GlobalPlatformData {
  scope: 'global';
  lastUpdated: string;
  creators: GlobalCreatorMetrics;
  campaigns: GlobalCampaign[];
  budget: GlobalBudgetMetrics;
}
```

### 19.2. Creator Metrics
```typescript
interface GlobalCreatorMetrics {
  totalCreators: number;
  newCreators: number;
  activeRate: number;  // percentage
  churnRate: number;   // percentage
  trends: {
    totalCreators: TrendInfo;
    newCreators: TrendInfo;
    activeRate: TrendInfo;
    churnRate: TrendInfo;
  };
}
```

### 19.3. Budget Metrics
```typescript
interface GlobalBudgetMetrics {
  total: number;       // VND
  used: number;        // VND
  percentage: number;  // %
  averageCPV: number;  // VND
}
```

---

## 20. FAQs

### Q1: Tại sao Total Views và Engagement không khớp?
**A**: Engagement chỉ tính interaction (likes, comments, shares), không bao gồm passive views.

### Q2: CPV âm có nghĩa gì?
**A**: Không thể có CPV âm. Nếu hiển thị "---", nghĩa là chưa có data hoặc views = 0.

### Q3: Tại sao Churn Rate + Active Rate ≠ 100%?
**A**: Có thể có influencer registered nhưng chưa từng submit (inactive nhưng không phải churned).

### Q4: Trend so sánh với kỳ nào?
**A**: Mặc định so với cùng kỳ trước đó (30 ngày trước nếu filter là 30 ngày).

### Q5: Platform nào hiệu quả nhất?
**A**: Cần xem kết hợp CPV + Engagement Rate + Business Goals. Không có câu trả lời chung.

---

## 21. Change Log

| Phiên bản | Ngày | Thay đổi |
|-----------|------|----------|
| 1.0.0 | 2024-02-14 | Initial documentation |

---

## 22. Liên hệ & Hỗ trợ

- **Technical Issues**: Contact Dev Team
- **Business Questions**: Contact Marketing Team
- **Data Accuracy**: Contact Analytics Team

---

**Lưu ý**: Tài liệu này được tạo dựa trên phân tích source code. Vui lòng cập nhật khi có thay đổi trong business logic hoặc UI components.
