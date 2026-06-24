# 💭 Reflection: Game Glitch Investigator

Answer each question in 3 to 5 sentences. Be specific and honest about what actually happened while you worked. This is about your process, not trying to sound perfect.

## 1. What was broken when you started?

- What did the game look like the first time you ran it?
The game UI looked static. Left column had all the main functionalities of the game and the right window had the input area and operation buttons.
- List at least two concrete bugs you noticed at the start  
  (for example: "the hints were backwards").
  1. The hints were opposite, e.g. when the right answer is 50 and you input 70, the hint would be "higher" but that doesn't make sense
  2. Clicking on "Restart game" button doesn't do anything, had to refresh the page to start a new game

**Bug Reproduction Log**

Document at least 3 bugs you found. Add rows as needed.

| Input | Expected Behavior | Actual Behavior | Console Output / Error |
|-------|-------------------|-----------------|------------------------|
| Click "Restart game" button | New Game | Nothing, old game still present | No output|
| Guess of 43 | Give me a Hint towards correct answer | Gives me a Hint away from correct answer | "Higher" instead of lower, vice versa |
| Click on "New Game" button | Start a new game | Start new game but my new input is not accepted | Instead of 7 tries, I get 8 tries |

---

## 2. How did you use AI as a teammate?

- Which AI tools did you use on this project (for example: ChatGPT, Gemini, Copilot)?
I used GitHub Copilot chat in VS Code as my main AI teammate during this lab. I used it to inspect app state issues, refactor logic from app.py into logic_utils.py, and suggest test updates after behavior changes. I kept prompts focused on one bug at a time so the edits stayed smaller and easier to review in the diff.
- Give one example of an AI suggestion that was correct (including what the AI suggested and how you verified the result).
One correct suggestion was to stop converting the secret number to a string before running check_guess, and to make hint messages match the outcome direction. I verified this by running pytest and confirming that a guess above the secret now returns "Too High" with a "Go LOWER!" hint while a lower guess returns "Too Low" with "Go HIGHER!". I also launched the Streamlit app to confirm the live hint behavior matched the expected game logic.
- Give one example of an AI suggestion that was incorrect or misleading (including what the AI suggested and how you verified the result).
An earlier AI-style pattern in the starter code was misleading because it mixed types during comparison and effectively inverted user guidance in some flows. Another misleading behavior was partial reset logic for New Game, which did not fully reset status/history/attempt consistency. I verified these were problems by reproducing them in the UI and then checking that full state reset plus logic refactor removed the issues.

---

## 3. Debugging and testing your fixes

- How did you decide whether a bug was really fixed?
I treated a bug as fixed only when both code-level and behavior-level checks passed. First I reviewed the diff to make sure logic moved into logic_utils.py cleanly and the app imports were correct. Then I ran tests and did a runtime app startup check to confirm there were no obvious regressions in execution.
- Describe at least one test you ran (manual or using pytest)  
  and what it showed you about your code.
I ran pytest and confirmed all tests passed, including checks that compare guesses to the secret with the correct outcomes and hint direction. The high/low tests now assert both the outcome value and hint text, which showed the hint bug was actually fixed rather than only cosmetically changed. I also started Streamlit and confirmed the app launched successfully after the refactor.
- Did AI help you design or understand any tests? How?
Yes, AI helped me reshape the tests after refactoring check_guess to return both outcome and message. It suggested asserting tuple contents directly so the tests validate actual game feedback, not just one field. That made the tests more aligned with the user-facing bug I was fixing.

---

## 4. What did you learn about Streamlit and state?

- How would you explain Streamlit "reruns" and session state to a friend who has never used Streamlit?
I would explain Streamlit reruns as the app starting over from the top every time you click a button, type into a widget, or change a setting. That means any normal variables get recreated unless you save them in `st.session_state`, which is Streamlit's way of remembering things between reruns. In this project, session state kept the secret number, score, attempts, and history alive even though the script kept rerunning.

---

## 5. Looking ahead: your developer habits

- What is one habit or strategy from this project that you want to reuse in future labs or projects?
  - This could be a testing habit, a prompting strategy, or a way you used Git.
I want to keep the habit of fixing one bug at a time and verifying it with both tests and the actual UI. That made the changes easier to understand and kept me from accidentally breaking unrelated parts of the game. I also want to keep moving the real game rules into a helper file so the app file stays easier to read.
- What is one thing you would do differently next time you work with AI on a coding task?
Next time, I would give AI even more specific context about the bug and the exact output I wanted before accepting any suggestion. I would also check the live behavior earlier instead of trusting a fix just because the code looked reasonable. That would help me catch state bugs or logic mismatches faster.
- In one or two sentences, describe how this project changed the way you think about AI generated code.
This project made me see AI-generated code as a starting point, not something I can trust without checking. It can help me move faster, but I still need to test it carefully because it can produce code that looks right while hiding bugs in state or logic.
