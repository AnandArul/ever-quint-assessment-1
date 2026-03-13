## Max Profit & Water Tank Visualizer

This project is a small Vue 3 app that demonstrates solutions to two classic interview‑style problems:

- **Max profit with time constraint** (`MaxProfit.vue`): given a total amount of time \(N\), choose a combination of three building types to **maximize profit**.
  - **T**: takes 5 units of time, profit 1500
  - **P**: takes 4 units of time, profit 1000
  - **C**: takes 10 units of time, profit 2000
  - The user enters a single number (total time) and the app searches all valid combinations to show:
    - **Profit**: maximum achievable profit
    - **T, P, C**: how many of each building to construct

  Internally, `MaxProfit.vue`:
  - Uses a small `buildings` array with type, time, and profit for each building.
  - Recursively explores all combinations that fit within the remaining time.
  - Tracks the best profit seen so far and corresponding counts of `T`, `P`, and `C`.

- **Water tank (trapping rain water)** (`WaterTank.vue`): given an array of bar heights, compute how much water can be trapped between them and visualize the result.
  - The user enters a comma‑separated list such as `3,0,4,0,0,0,6,0,6,4,0`.
  - The app parses the numbers and:
    - Builds `startMax` and `endMax` arrays to track the tallest bar to the left and right of each index.
    - Computes how much water can sit on top of each bar.
    - Calculates the **total trapped water units**.
    - Renders a simple color grid:
      - **Yellow** cells for bar blocks.
      - **Blue** cells for trapped water blocks.
      - **White** cells for empty space.

The home view renders both components so you can try each problem interactively.

### Tech stack

- **Framework**: Vue 3 with `<script setup>`
- **Routing**: Vue Router (`src/router/index.js`)
- **Styling**: basic styles in `src/assets/main.css`
- **Tooling**: Vite (standard Vue 3 starter)

### Getting started

1. **Install dependencies**

```bash
npm install
```

2. **Run the dev server**

```bash
npm run dev
```

3. Open the printed local URL in your browser and:
   - Use the **Max Profit** section to try different total times (numbers only).
   - Use the **Water Tank** section to try different height arrays.

### How the algorithms work (high level)

- **Max profit**
  - A depth‑first recursive search:
    - `findSolution(remainingTime, counts, currentProfit)` tries to place each building while enough time remains.
    - On each recursive call it subtracts the building time, adds its profit, and updates the best solution if the profit is higher.

- **Water tank**
  - Classic trapping‑rain‑water approach:
    - Build `startMax[i]` = maximum height from the start to `i`.
    - Build `endMax[i]` = maximum height from the end to `i`.
    - Water at index `i` is `min(startMax[i], endMax[i]) - height[i]`, or 0 if negative.
    - The visualization stacks colored cells up to the maximum column height.

For more detail, read through `src/components/MaxProfit.vue` and `src/components/WaterTank.vue`.
