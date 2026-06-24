# 🎮 Game Glitch Investigator: The Impossible Guesser

## 🚨 The Situation

You asked an AI to build a simple "Number Guessing Game" using Streamlit.
It wrote the code, ran away, and now the game is unplayable. 

- You can't win.
- The hints lie to you.
- The secret number seems to have commitment issues.

## 🛠️ Setup

1. Create a virtual environment: `python3 -m venv .venv`
2. Activate it: `source .venv/bin/activate`
3. Install dependencies: `python -m pip install -r requirements.txt`
4. Run the broken app: `python -m streamlit run app.py`

If you prefer not to activate the environment, you can also run:

`./.venv/bin/python -m streamlit run app.py`

## 🕵️‍♂️ Your Mission

1. **Play the game.** Open the "Developer Debug Info" tab in the app to see the secret number. Try to win.
2. **Find the State Bug.** Why does the secret number change every time you click "Submit"? Ask ChatGPT: *"How do I keep a variable from resetting in Streamlit when I click a button?"*
3. **Fix the Logic.** The hints ("Higher/Lower") are wrong. Fix them.
4. **Refactor & Test.** - Move the logic into `logic_utils.py`.
   - Run `pytest` in your terminal.
   - Keep fixing until all tests pass!

## 📝 Document Your Experience

- [x] Describe the game's purpose: Streamlit number guessing game where players find a secret number within a limited number of attempts, receiving hints and earning a score based on attempt efficiency.
- [x] Detail which bugs you found: 
  1. Inverted hint logic due to type-casting in comparison (guess above secret said "Go HIGHER" instead of "Go LOWER").
  2. New Game reset incomplete—did not clear attempts, status, history, or score.
- [x] Explain what fixes you applied:
  1. Refactored game logic into logic_utils.py.
  2. Fixed check_guess to compare guess and secret as integers; corrected hint directions.
  3. Fixed New Game button to fully reset all session state.
  4. Updated tests to verify both outcome and message content.

## 📸 Demo Walkthrough

Describe your fixed game in numbered steps so a reader can follow along without watching a video:

1. Guess 40 → Too Low, Go HIGHER (7 attempts left)
2. Guess 70 → Too High, Go LOWER (6 attempts left)
3. Guess 60 → Too High, Go LOWER (5 attempts left)
4. Guess 55 → Too High, Go LOWER (4 attempts left)
5. Guess 52 → Too High, Go LOWER (3 attempts left)
6. Guess 50 → Win, Correct! Score: 70 points.
7. Click New Game → Session state resets; secret changes, attempts = 0, history cleared, ready to play again.

**Screenshot** *(optional)*: <!-- Insert a screenshot of your fixed, winning game here -->

## 🧪 Test Results

```
# Paste your pytest output here, e.g.:
# pytest tests/
# ========================= X passed in 0.XXs =========================
```
luisramon@Mac ai110-module1show-gameglitchinvestigator-starter % ./.venv/bin/python -m pytest -v
===================== test session starts ======================
platform darwin -- Python 3.12.0, pytest-9.1.1, pluggy-1.6.0 --/Users/luisramon/ai110-module1show-gameglitchinvestigator-starter/.venv/bin/python
cachedir: .pytest_cache
rootdir: /Users/luisramon/ai110-module1show-gameglitchinvestigator-starter
plugins: anyio-4.14.0
collected 3 items                                              

tests/test_game_logic.py::test_winning_guess PASSED      [ 33%]
tests/test_game_logic.py::test_guess_too_high PASSED     [ 66%]
tests/test_game_logic.py::test_guess_too_low PASSED      [100%]

====================== 3 passed in 0.01s =======================

## 🚀 Stretch Features

- [ ] [If you choose to complete Challenge 4, describe the Enhanced UI changes here — a screenshot is optional]
