# Tra cứu nhanh Chỉ số Dashboard

## 📊 Chỉ số Influencer

| Chỉ số | Icon | Màu | Công thức | Ý nghĩa |
|--------|------|-----|-----------|---------|
| **Tổng số Influencer** | 👥 | Blue | Count unique creators | Quy mô mạng lưới |
| **Influencer mới** | 👤+ | Green | First-time submitters | Tốc độ tăng trưởng |
| **Tỷ lệ hoạt động** | 📊 | Violet | (Active / Total) × 100% | Mức độ engagement |
| **Tỷ lệ nghỉ** | 📉 | Pink | (Inactive / Total) × 100% | Retention quality |

## 🎥 Chỉ số Video & Views

| Chỉ số | Icon | Màu | Công thức | Ý nghĩa |
|--------|------|-----|-----------|---------|
| **Tổng số Video** | 🎥 | Green | Sum all videos | Sản lượng content |
| **Tổng lượt xem** | 👁️ | Purple | Sum all views | Độ phủ campaign |

## 💰 Chỉ số Tài chính

| Chỉ số | Icon | Màu | Công thức | Ý nghĩa |
|--------|------|-----|-----------|---------|
| **Tổng phí quảng cáo** | 💰 | Orange | Sum payments | Chi phí thực tế |
| **Budget đã dùng** | 💵 | Green | Used amount | Tiến độ chi tiêu |
| **Budget còn lại** | 💵 | Blue | Total - Used | Ngân sách available |
| **Burn Rate** | 🔥 | Dynamic | (Used/Total) × 100% | Tốc độ tiêu budget |
| **CPV** | 💸 | Pink | Payment / Views | Hiệu quả chi phí |

## ❤️ Chỉ số Tương tác

| Chỉ số | Icon | Màu | Công thức |
|--------|------|-----|-----------|
| **Lượt xem** | 👁️ | Blue | Base metric |
| **Thích** | ❤️ | Red | (Likes/Views) × 100% |
| **Bình luận** | 💬 | Amber | (Comments/Views) × 100% |
| **Chia sẻ** | 🔁 | Green | (Shares/Views) × 100% |
| **Engagement Rate** | 📈 | - | ((L+C+S)/Views) × 100% |

## 🌐 Chỉ số Platform

| Platform | Màu | CSS Variable |
|----------|-----|--------------|
| Facebook | Blue #1877F2 | `--facebook` |
| YouTube | Red #FF0000 | `--youtube` |
| TikTok | Black/White | `--tiktok` |
| Instagram | Pink #E4405F | `--instagram` |

## ✅ Chỉ số Duyệt nội dung

| Trạng thái | Màu | Label |
|------------|-----|-------|
| Approved | 🟢 Green | Đã duyệt |
| Pending | 🟡 Yellow | Chờ duyệt |
| Rejected | 🔴 Red | Từ chối |

## 💸 Chỉ số Chuyển khoản

| Chỉ số | Màu | Công thức |
|--------|-----|-----------|
| **Yêu cầu** | - | Count requests |
| **Thành công** | Green | Success count |
| **Tỷ lệ thành công** | Dynamic | (Success/Total) × 100% |
| **Tổng tiền** | - | Sum amount |
| **Đã thanh toán** | Green | Success amount |

## 🎯 Ngưỡng đánh giá

### Active Rate
- ✅ ≥ 70%: Tốt
- ⚠️ 50-70%: Trung bình
- ❌ < 50%: Cần cải thiện

### Burn Rate
- ✅ ≤ 70%: An toàn
- ⚠️ 71-85%: Cảnh báo
- ❌ > 85%: Nguy hiểm

### Transfer Success Rate
- ✅ ≥ 80%: Tốt
- ⚠️ 50-79%: Trung bình
- ❌ < 50%: Cần xử lý

### Engagement Rate (Benchmark)
- Facebook: 1-3%
- YouTube: 3-5%
- TikTok: 5-10%

## 📈 Trend Indicators

| Icon | Màu | Ý nghĩa |
|------|-----|---------|
| ↑ | Green | Tăng so với kỳ trước |
| ↓ | Red | Giảm so với kỳ trước |
| → | Gray | Không đổi |

## 🎨 KPI Color Codes

```css
--kpi-videos: Green (#22C55E)
--kpi-views: Purple (#A855F7)
--kpi-budget: Orange (#F97316)
--kpi-cpv: Pink (#EC4899)
--kpi-engagement: Violet (#8B5CF6)
--kpi-payment: Emerald (#10B981)
```

## 📱 Grid Responsive

- **Desktop (lg+)**: 4 columns
- **Tablet (md)**: 2 columns
- **Mobile**: 1 column

## 🔢 Format Functions

| Function | Input | Output |
|----------|-------|--------|
| formatNumber | 1234567 | "1,234,567" |
| formatCompact | 1234567 | "1.2M" |
| formatCurrency | 1234567 | "1,234,567₫" |
| formatPercent | 15.32 | "15.3%" |

## 🚨 Action Items theo Chỉ số

| Chỉ số cao/thấp | Action |
|-----------------|--------|
| CPV cao | Review content quality, optimize |
| Engagement thấp | Improve guideline, training |
| Churn rate cao | Survey influencer, improve incentive |
| Rejection rate cao | Clarify guideline, examples |
| Burn rate > 85% | Review budget, pause campaign |
| Success rate < 80% | Check payment process |

## 📊 Workflow Status Chuyển khoản

```
draft → new → pending → processing → processed →
transferring → transferred → finished
                ↓
             rejected
```

---

**Tip**: Luôn xem context (campaign, time range) khi phân tích chỉ số!
