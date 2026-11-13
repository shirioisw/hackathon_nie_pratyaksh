# 🥟 Canteen Clicker

**An idle clicker game set in a busy college canteen.** Sell samosas and chai, earn coins, and spend them on upgrades like extra staff, a bigger counter and a festival menu board. You only have room for three active upgrades, so every purchase is a choice.

Built for **VibeSprint, Problem Card 12 (Fun & Creative)**.

**Live demo:** https://shirioisw.github.io/hackathon_nie_pratyaksh/

---

## Table of contents

1. [The idea](#the-idea)
2. [How to run it](#how-to-run-it)
3. [How to play](#how-to-play)
4. [Game mechanics in detail](#game-mechanics-in-detail)
5. [Upgrades](#upgrades)
6. [The 3-slot limit and swap fee](#the-3-slot-limit-and-swap-fee)
7. [Judge verification path](#judge-verification-path)
8. [Feedback, validation and result states](#feedback-validation-and-result-states)
9. [Sound and animation](#sound-and-animation)
10. [Accessibility](#accessibility)
11. [Build rules checklist](#build-rules-checklist)
12. [Tech and project structure](#tech-and-project-structure)
13. [Testing it yourself](#testing-it-yourself)
14. [Ideas for the future](#ideas-for-the-future)

---

## The idea

Idle clickers are satisfying because every click makes a number go up, and every upgrade makes the next click worth more. Canteen Clicker puts that loop in a setting every student knows: the rush at the canteen counter.

You start with an empty counter and two items to sell. Early on you earn coins by clicking. As you buy staff and equipment, customers start getting served on their own, and you move from serving everyone by hand to running the canteen.

The twist in the design is the **three-slot limit**. You can't stack every upgrade, so you decide which combination makes the most money, and swapping out an upgrade costs an extra fee.

## How to run it

**Option 1: play online.** Open the live demo link above.

**Option 2: run it locally.** Download or clone this repository and double-click `index.html`. It opens in your browser.

There is nothing to install. The game is a single file with no API, no login, no database, no environment variables and no secret keys. All data is fictional and all calculations happen in your browser.

## How to play

1. **Serve customers.** Click **Sell samosa** or **Sell chai** on the serving counter. Each click is one sale and earns coins.
2. **Watch your numbers.** The top of the screen shows your **coins**, your **total sales** and your **coins per second**.
3. **Buy upgrades.** The upgrade panel lists six upgrades with their cost and effect. When you can afford one, click **Buy**.
4. **Fill your slots.** Bought upgrades go into one of three upgrade slots. The slot bar shows how many are in use.
5. **Make room.** Once all three slots are full, a new upgrade needs a swap: pick a slot to replace and pay the upgrade's price plus a swap fee.
6. **Reset anytime.** The **Reset game** link under the counter starts a fresh game.

## Game mechanics in detail

**Base prices**

| Item | Base price |
|------|-----------|
| Samosa | 5 coins |
| Chai | 3 coins |

**How the price of a sale is calculated.** Upgrades are applied in this order:

1. Start with the item's base price.
2. Add flat bonuses (for example, +2 from Bigger counter).
3. Apply item multipliers (Spicy chutney for samosas, Steel kettle for chai).
4. Apply the all-items multiplier (Festival menu board).
5. Round to one decimal place.

For example, with Bigger counter and Spicy chutney active, a samosa sells for (5 + 2) x 1.5 = 10.5 coins, and chai sells for 3 + 2 = 5 coins.

**Automatic serving.** Staff upgrades serve customers without any clicking, once per second. Each automatically served customer earns the average of the current samosa and chai prices and counts toward total sales. The **coins per second** figure at the top is the automatic serving rate multiplied by that average price.

**Milestones.** Every 25 total sales, a banner and a celebration sound mark the milestone.

## Upgrades

| Upgrade | Cost | Effect |
|---------|------|--------|
| Extra staff | 40 | Serves 1 customer every second |
| Bigger counter | 60 | +2 coins on every sale |
| Spicy chutney | 80 | Samosas sell for 50% more |
| Steel kettle | 80 | Chai sells for 50% more |
| Cashier | 150 | Serves 3 more customers per second |
| Festival menu board | 200 | All coins x1.5 |

Each upgrade shows its cost and its effect directly on its card, so you never have to guess what a purchase will do. Upgrades that are currently active are marked "active".

## The 3-slot limit and swap fee

- You can have **at most 3 active upgrades**.
- While a slot is free, buying an upgrade costs its normal price and puts it in the first empty slot.
- When all 3 slots are full, every unbought upgrade changes to **Swap in**, with its price plus a **25-coin swap fee** shown on the button.
- Clicking it asks you to choose which slot to replace. Each filled slot shows a **Replace this** button.
- You pay the upgrade price plus the fee, the old upgrade is removed, and the new one takes its place. A message confirms exactly what was swapped and what you paid.
- If you don't have enough coins for the swap, nothing changes and the game tells you how many coins you are short.

## Judge verification path

| Step | What to do | What you will see |
|------|-----------|-------------------|
| 1. Sell an item and show the coin balance increase | Click Sell samosa or Sell chai | The coin balance goes up, a "+coins" pop-up floats from the button, a coin sound plays, and a success message appears |
| 2. Purchase upgrades until three slots are occupied | Earn coins and buy upgrades one by one | Each upgrade fills a slot, the slot bar fills, and confetti and a banner appear when all 3 are full |
| 3. Verify a fourth active upgrade is blocked or requires a swap fee | Try to buy any other upgrade | The button changes to "Swap in" with the extra fee, you must pick a slot to replace, and the total cost is charged |

**Fast way to test:** click Sell samosa 8 times to reach 40 coins, buy Extra staff, then keep selling and buying until all three slots are full.

## Feedback, validation and result states

Every action gives a visible result in the message box under the counter:

- **Success (green):** a sale, a purchase, a swap, or a milestone. The message says what happened and how many coins changed.
- **Error (red, with a shake and a buzz):** trying to buy something you can't afford, or confirming a swap without enough coins. The message says how many coins you are short.
- **Blocked state:** with 3 slots full, a new upgrade can't simply be added. The game explains the swap rule and shows the total cost.

Buttons for upgrades you can't afford yet stay clickable on purpose, so the player gets an explanation instead of a silent, greyed-out button.

## Sound and animation

All sound is generated in the browser, so there are no audio files to load.

**Sounds**
- A soft click on every button
- A coin sound for each sale
- A rising chime for a purchase
- A whoosh for a swap
- A low buzz for errors
- A short fanfare for big moments

A **Sound on / Sound off** button in the top right mutes everything. Browsers only allow sound after the first click on the page, so the very first click may be silent.

**Animations**
- Floating "+coins" pop-ups from the button you click
- A bump on the coin counter after each sale
- A button squish when pressed
- A pop-in effect when an upgrade fills a slot
- A shake on the message box for errors
- Confetti and a banner when all 3 slots are filled and at every 25 sales

## Accessibility

- Keyboard friendly: every control is a real button with a visible focus outline.
- Status updates (coins, messages) are announced to screen readers through live regions.
- The game respects the **reduce motion** setting on your device: animations, pop-ups and confetti are switched off.
- Meaning is never carried by color alone. Costs, effects and states are always written out in text.
- The layout is responsive and stacks into one column on phones.

## Build rules checklist

| Rule | How this project meets it |
|------|---------------------------|
| Browser-first prototype | Runs fully in the browser with local calculations and sample data |
| No external API, paid service, login, database or secret key | None are used |
| No `.env` dependency | The app loads and works straight away |
| Core interaction with validation and a visible result | Selling, buying and swapping all validate and show success or error states |
| Fictional data only | Samosas, chai and coins are made up |
| Submission includes the app, documentation and proof | Live link and source code in this repo, this README, and a screen recording with screenshots |

## Tech and project structure

- **Language:** plain HTML, CSS and JavaScript, with no frameworks or build step
- **Hosting:** GitHub Pages, served from the `main` branch
- **Audio:** the Web Audio API
- **Animation:** CSS keyframes and the Web Animations API

```
hackathon_nie_pratyaksh/
├── index.html   # the whole game: markup, styles and logic
└── README.md    # this document
```

The game keeps a small state object (coins, sales and three upgrade slots). Every action updates that state and then redraws the screen from it, which keeps the numbers, slots and buttons consistent.

## Testing it yourself

1. Open the live demo.
2. Click Sell samosa and confirm the coins increase and a message appears.
3. Try to buy an upgrade with too few coins and confirm you get an error with the shortfall.
4. Earn enough coins and buy three upgrades. Confirm the slot bar reaches 3 of 3 and the confetti appears.
5. Click a fourth upgrade. Confirm it asks you to pick a slot and charges the price plus the 25-coin fee.
6. Press **Reset game** and confirm everything returns to zero.

## Ideas for the future

- Saving progress between visits
- More menu items, such as vada pav, cold coffee and sandwiches
- Upgrades that can be levelled up instead of bought once
- Random rush hours and customer moods
- A shared leaderboard of the busiest canteens

---

Built with Claude at VibeSprint.
