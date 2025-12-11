# 🎮 Emotional Labor Consultant - Customer Service Simulator

A web-based simulation game that puts you in the shoes of a customer service representative handling multiple demanding customers under time pressure.

## 🚀 How to Run

Simply open `index.html` in any modern web browser. No build tools or server required!

```bash
# Option 1: Double-click index.html in your file explorer

# Option 2: Open from command line
open index.html  # macOS
start index.html # Windows
xdg-open index.html # Linux
```

## 🎯 Game Mechanics

### Objective
Handle as many customer complaints as possible within **60 seconds** while managing your own personal needs.

### Key Features

1. **Time Limit**: 60 seconds to resolve as many customers as possible
2. **Patience System**: Each customer has a patience bar that depletes over time
   - If patience runs out (3 seconds of no response), customers send angry messages
   - Angry customers reduce your score
3. **Macro Response System**: No typing allowed! Use predefined macro buttons to respond
4. **Personal Tasks**: Simulate real workplace needs with blocking overlays:
   - 🚽 Toilet (5 seconds)
   - 💧 Water (3 seconds)
   - 🍱 Meal (5 seconds)
   - During these tasks, you cannot interact with customers!

### Customer Scenarios

The game includes 3 types of customer complaints:

- **Type A: Delivery Delay** (김철수)
  - Flow: Check Order → Check Location → Apology
- **Type B: Wrong Food** (이영희)
  - Flow: Check Order → Apology → Refund/Redelivery
- **Type C: Complaint** (박민수)
  - Flow: Apology → Check Order → Compensation

### Scoring
- ✅ **+100 points** per resolved customer
- 😠 **-50 points** per angry message triggered
- 🏆 **Final score** = (Resolved × 100) - (Angry × 50)

## 🎨 Customization Guide

### 1. Change Colors & Styling

All styles are in the `<style>` block. Key classes you can customize:

```css
/* Main layout colors */
.sidebar-left { background: #2c2c3e; } /* Left sidebar background */
.chat-main { background: #fafafa; } /* Center chat area */
.sidebar-right { background: #f9f9f9; } /* Right dashboard */

/* Chat bubble colors */
.chat-bubble.customer { background: #ffffff; } /* Customer messages */
.chat-bubble.agent { background: #4a9eff; } /* Your responses */
.chat-bubble.customer.angry { background: #ffe0e0; } /* Angry messages */

/* Button colors */
.btn-macro { border-color: #4a9eff; } /* Macro buttons */
.btn-action.btn-personal { background: #ff9800; } /* Personal task buttons */
.btn-action.btn-start { background: #4caf50; } /* Start button */

/* Timer colors */
.timer-display { color: #4a9eff; } /* Normal time */
.timer-display.warning { color: #ff9800; } /* < 30 seconds */
.timer-display.danger { color: #ff4444; } /* < 10 seconds */
```

### 2. Add/Modify Customer Scenarios

Find the `SCENARIOS` object in the JavaScript section:

```javascript
const SCENARIOS = {
    yourNewScenario: {
        type: 'yourNewScenario',
        customerName: '홍길동',  // Customer name
        initialMessage: '초기 메시지', // First message
        angryMessages: [  // Messages when patience runs out
            '화난 메시지 1',
            '화난 메시지 2'
        ],
        expectedFlow: ['action1', 'action2'],  // Required action sequence
        flowIndex: 0,
        responses: {
            action1: 'Response text for action 1',
            action2: 'Response text for action 2'
        },
        successMessage: '해결 완료 메시지',
        macros: [  // Available response buttons
            { id: 'action1', label: '버튼1', text: '응답 텍스트 1' },
            { id: 'action2', label: '버튼2', text: '응답 텍스트 2' }
        ]
    }
};
```

### 3. Adjust Game Difficulty

```javascript
// Change time limit (line ~350)
timeRemaining: 60,  // Change to 90 for easier, 45 for harder

// Change patience depletion rate (line ~580)
customer.patience -= 2;  // Higher = faster patience loss

// Change customer spawn rate (line ~649)
Math.random() * 7000 + 8000  // Range: 8-15 seconds
// Lower numbers = more frequent spawns

// Change personal task durations (line ~720)
startPersonalTask('화장실', 5, '🚽');  // Change 5 to any number of seconds
```

### 4. Modify UI Text

All Korean text can be easily changed throughout the file:

- **Sidebar header**: Line ~380 (`<div class="sidebar-title">고객 상담</div>`)
- **Chat header**: Line ~400 (`<div class="chat-header-title">고객을 선택하세요</div>`)
- **Button labels**: Lines ~430-450 (Personal task buttons)
- **Game over text**: Lines ~500-520

### 5. Add New Personal Tasks

```javascript
// Add button in HTML (around line 450)
<button class="btn-action btn-personal" id="btnSnack">
    🍿 간식 (2초)
</button>

// Add event listener (around line 760)
document.getElementById('btnSnack').addEventListener('click', () => {
    startPersonalTask('간식 먹기', 2, '🍿');
});
```

## 📁 File Structure

```
/workspace/
├── index.html    # Complete game (HTML + CSS + JS)
└── README.md     # This file
```

## 🛠️ Technical Details

- **Pure Vanilla JavaScript** - No frameworks or dependencies
- **CSS Grid Layout** - Responsive 3-column design
- **No Build Tools Required** - Just open and play
- **Commented Code** - Easy to understand and modify

## 🎮 Game Tips

1. **Prioritize customers** with low patience bars
2. **Use personal tasks strategically** during quiet moments
3. **Follow the correct response flow** for each customer type
4. **Quick responses** prevent patience depletion
5. **Don't let customers pile up** - they spawn continuously!

## 🐛 Troubleshooting

**Q: Game doesn't start?**
- Make sure JavaScript is enabled in your browser
- Try opening in Chrome, Firefox, or Safari

**Q: Buttons not working?**
- Check browser console (F12) for errors
- Refresh the page

**Q: Want to reset mid-game?**
- Just refresh the browser page

## 📝 License

Free to use and modify for personal or educational purposes!

## 🤝 Contributing

Feel free to fork and customize this game for your own needs. Some ideas:
- Add more customer scenarios
- Implement difficulty levels
- Add sound effects
- Create a high score system
- Add more personal tasks

---

Enjoy the game! 🎉
