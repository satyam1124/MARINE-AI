# MOB Security System - Design Document

## Part 1: Visual Design System

### Overview
A marine safety dashboard with a dark, high-contrast design optimized for ship bridge environments. The design prioritizes instant readability with large typography, clear status indicators, and a nautical color palette. The interface is designed to allow ship officers to understand critical situations within 2 seconds.

Key characteristics:
- **Dark mode first**: Deep navy background with high-contrast white text
- **High visibility**: Large fonts, clear icons, bold status colors
- **Marine aesthetic**: Nautical colors (navy, teal, ocean blue)
- **Mission-critical focus**: Alert states are impossible to miss
- **Responsive layout**: Works on various screen sizes

### Color Palette

**Primary Colors:**
- `--primary`: #1a3a5c (Deep Navy - main background)
- `--secondary`: #0d2137 (Darker Navy - cards, panels)
- `--accent`: #00d4aa (Ocean Teal - highlights, active states)
- `--text-primary`: #ffffff (White - primary text)
- `--text-secondary`: #8b9db3 (Muted Blue - secondary text)

**Status Colors:**
- `--status-safe`: #00d4aa (Teal - safe/normal)
- `--status-warning`: #f59e0b (Amber - warning)
- `--status-alert`: #ef4444 (Red - critical/MOB alert)
- `--status-info`: #3b82f6 (Blue - informational)

**Map Colors:**
- `--map-track`: #00d4aa (GPS track line)
- `--map-alert`: #ef4444 (Alert position)
- `--map-ship`: #ffffff (Ship marker)

### Typography System

**Font Families:**
- Headings: 'Segoe UI', system-ui, sans-serif
- Body: 'Segoe UI', system-ui, sans-serif
- Monospace (coordinates/data): 'Consolas', 'Monaco', monospace

**Type Scale (optimized for bridge visibility):**
- H1: 2.5rem (40px) - Page titles
- H2: 2rem (32px) - Section headers
- H3: 1.5rem (24px) - Card titles
- Body: 1.125rem (18px) - Standard text
- Small: 0.875rem (14px) - Labels, timestamps
- Data: 1.25rem (20px) - Telemetry values
- Alert: 3rem (48px) - Emergency alerts

**Font Weights:**
- Regular: 400
- Medium: 500
- Semibold: 600
- Bold: 700

### Spacing System

**Base unit: 0.25rem (4px)**

- xs: 0.25rem (4px)
- sm: 0.5rem (8px)
- md: 1rem (16px)
- lg: 1.5rem (24px)
- xl: 2rem (32px)
- 2xl: 3rem (48px)

**Section spacing:** 1.5rem - 2rem between major sections
**Card padding:** 1.25rem - 1.5rem
**Component gaps:** 0.75rem - 1rem

### Common Components

**Buttons:**
- Primary: Ocean teal background (#00d4aa), dark text, no border-radius
- Secondary: Transparent with teal border, teal text
- Alert: Red background (#ef4444), white text
- Padding: 0.75rem 1.5rem
- Font: 1rem, weight 600
- Hover: 10% brightness increase

**Cards:**
- Background: Darker navy (#0d2137)
- Border: 1px solid rgba(255,255,255,0.1)
- Border-radius: 8px
- Padding: 1.25rem
- Shadow: 0 4px 6px rgba(0,0,0,0.3)

**Tables:**
- Header: Darker background, uppercase text
- Rows: Alternating subtle backgrounds
- Hover: Highlight on row hover
- Padding: 0.75rem 1rem per cell

**Status Badges:**
- Safe: Teal background, dark text
- Warning: Amber background, dark text
- Alert: Red background, white text
- Padding: 0.25rem 0.75rem
- Border-radius: 4px

**Form Inputs:**
- Background: rgba(255,255,255,0.05)
- Border: 1px solid rgba(255,255,255,0.2)
- Border-radius: 4px
- Padding: 0.75rem 1rem
- Focus: Teal border highlight

### Layout Principles

**Container:**
- Max-width: 100% (full-width dashboard)
- Padding: 1rem - 1.5rem horizontal

**Grid System:**
- CSS Grid for main layout
- Flexbox for component alignment
- 12-column grid for dashboard widgets

**Responsive Breakpoints:**
- Desktop: 1200px+ (full dashboard)
- Tablet: 768px - 1199px (adjusted grid)
- Mobile: < 768px (stacked layout)

---

## Part 2: Global Animations & Interactions

### Page Load Animation Sequence
- Header fades in immediately (0ms)
- Dashboard cards stagger in from bottom (100ms delay each)
- Map initializes with fade-in (300ms)
- Duration: 400ms per element
- Easing: cubic-bezier(0.4, 0, 0.2, 1)

### Smooth Scroll Behavior
- scroll-behavior: smooth on html
- No custom scroll animations needed

### Scroll-Triggered Reveal Animations
- Elements fade in + translate Y (20px) when entering viewport
- Threshold: 0.1 (10% visible)
- Duration: 400ms
- Easing: ease-out

### Common Hover Patterns
- Buttons: brightness(1.1) transition
- Cards: subtle border highlight
- Table rows: background color shift
- Duration: 200ms
- Easing: ease

### Technical Specifications
- Use transform and opacity for animations (GPU accelerated)
- will-change on animated elements
- Reduced motion support: @media (prefers-reduced-motion: reduce)

---

## Part 3: Content Sections

### Section: Header/Navigation

**Layout & Style:**
- Fixed position at top
- Full width, height 64px
- Background: Deep navy with subtle bottom border
- Flex layout: logo left, nav center, user info right
- Z-index: 1000

**Interactions:**
- Logo hover: subtle glow effect
- Nav items: underline on hover
- User menu: dropdown on click

**Content:**
- Logo: Anchor icon + "MOB GUARD"
- Nav: Dashboard | Map | History | Settings
- User: Role badge + username

---

### Section: Status Banner

**Layout & Style:**
- Full width banner below header
- Height: 80px
- Background changes based on status:
  - SAFE: Teal gradient
  - WARNING: Amber gradient
  - ALERT: Red gradient with pulse animation
- Large status text centered

**Interactions:**
- Alert state: pulsing background animation
- Duration: 1.5s infinite pulse
- Easing: ease-in-out

**Content:**
- Status icon (check, warning, or alert)
- Status text: "SYSTEM NORMAL" / "WARNING" / "MAN OVERBOARD"
- Timestamp of last update

---

### Section: Telemetry Dashboard

**Layout & Style:**
- 4-column grid on desktop
- 2-column on tablet
- 1-column on mobile
- Gap: 1rem

**Card Types:**
1. **GPS Position Card**
   - Large coordinate display (monospace)
   - Satellite count badge
   - Fix status indicator

2. **Speed & Course Card**
   - Speed in knots (large)
   - Course in degrees with compass icon
   - Visual compass rose

3. **Signal Strength Card**
   - RSSI value with color coding
   - Signal bars visualization
   - Green: > -80dBm, Amber: -80 to -95dBm, Red: < -95dBm

4. **Beacon Info Card**
   - Device ID
   - Battery level (if available)
   - Last seen timestamp

**Interactions:**
- Cards: subtle lift on hover
- Values: flash animation on update
- Duration: 300ms flash

**Content:**
- Real-time telemetry data
- Auto-updating every 2 seconds

---

### Section: Map View

**Layout & Style:**
- Full-width container
- Height: 500px (desktop), 400px (mobile)
- Border-radius: 8px
- Border: 2px solid rgba(255,255,255,0.1)

**Map Configuration:**
- Base: OpenStreetMap
- Overlay: OpenSeaMap seamarks
- Controls: zoom, fullscreen, center-on-MOB

**Markers:**
- Ship: White boat icon with direction indicator
- MOB: Red pulsating circle with person icon
- Track: Teal polyline showing movement history

**Interactions:**
- Map pans to MOB on alert
- Markers clickable for info popup
- Center-on-MOB button

**Content:**
- Real-time position tracking
- Movement trail (last 50 points)
- Distance calculation from ship

---

### Section: Alert Panel

**Layout & Style:**
- Fixed position bottom-right
- Width: 400px
- Background: Dark navy with red border
- Border-radius: 8px
- Shadow: 0 10px 25px rgba(0,0,0,0.5)

**Alert Types:**
1. GPS Fix Lost
2. Low Signal Strength
3. Speed Anomaly
4. Manual Trigger

**Interactions:**
- Slide in from right on alert
- Pulsing red border
- Audio alarm (Web Audio API)
- Acknowledge button stops alarm

**Content:**
- Alert title
- Description
- Timestamp
- Acknowledge button

---

### Section: History Log

**Layout & Style:**
- Full-width table
- Scrollable container (max-height: 400px)
- Sticky header
- Alternating row colors

**Columns:**
- Timestamp
- Device ID
- Position (lat/lon)
- Speed
- RSSI
- Status
- Actions

**Interactions:**
- Row hover highlight
- Filter by date range
- Filter by alert type
- Export to CSV button

**Content:**
- Historical data from localStorage
- Pagination (50 items per page)

---

### Section: Login Modal

**Layout & Style:**
- Centered modal overlay
- Width: 400px
- Background: Dark navy
- Border-radius: 8px
- Backdrop blur

**Interactions:**
- Fade in on page load (if not logged in)
- Form validation
- Role-based redirect

**Content:**
- Username/password fields
- Role selection (Admin/Viewer)
- Login button
- Demo credentials hint

---

### Section: Footer

**Layout & Style:**
- Full width
- Background: Darker navy
- Padding: 1rem
- Text center

**Content:**
- System version
- Last sync time
- Marine safety disclaimer

---

## Part 4: Special Features

### Audio Alert System
- Web Audio API for alarm generation
- Oscillator-based siren sound
- Volume control
- Mute option

### Data Persistence
- localStorage for packet storage
- IndexedDB option for larger logs
- Auto-cleanup old data (30 days)

### API Simulation
- receiveLoRaPacket(packet) function
- Mock data generator for testing
- REST API ready structure

### Role-Based Access
- Admin: Full access
- Viewer: Read-only
- localStorage session
