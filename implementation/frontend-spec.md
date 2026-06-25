# Frontend Specification

## Tech Stack

- **Web**: React 18 + TypeScript + Vite
- **Mobile**: React Native (Expo)
- **State**: Zustand
- **Charts**: D3.js + Recharts
- **UI**: Tailwind CSS + Radix UI

## Screens

### 1. Dashboard
- Hierarchical tree visualisation of $\Phi(k)$
- Real-time foam meter
- $R_{	ext{hier}}$ indicator
- Quick capture button

### 2. Capture
- Chat-like interface for thought input
- Emotion slider (-1 to 1)
- Auto-level detection (ML-based)
- Voice input support

### 3. Nullify
- Interactive "what-if" simulator
- Strategy selector (soft/hard/wave)
- Preview of expected $\Phi$ reduction
- Confirm/Cancel flow

### 4. Report
- Timeline of $\Phi(k)$ over days/weeks
- Cluster visualisation (t-SNE)
- Correlation with sleep, mood, activity
- Export to PDF

### 5. Settings
- Hierarchy level customisation
- Notification preferences
- Data export/delete (GDPR)

## Component Hierarchy

```
App
├── Layout
│   ├── Sidebar
│   └── Header
├── Routes
│   ├── Dashboard
│   │   ├── FoamTree
│   │   ├── FoamMeter
│   │   └── QuickCapture
│   ├── Capture
│   │   ├── ChatInterface
│   │   ├── EmotionSlider
│   │   └── LevelDetector
│   ├── Nullify
│   │   ├── Simulator
│   │   ├── StrategyPicker
│   │   └── PreviewChart
│   └── Report
│       ├── Timeline
│       ├── ClusterMap
│       └── ExportButton
```

## Design Tokens

- Primary: `#4F46E5` (Indigo)
- Secondary: `#10B981` (Emerald)
- Danger: `#EF4444` (Red)
- Background: `#F9FAFB` (Gray-50)
- Foam gradient: `#FEE2E2` → `#FEF3C7` → `#D1FAE5`
