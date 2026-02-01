# 💭 Reflection: Game Glitch Investigator

Answer each question in 3 to 5 sentences. Be specific and honest about what actually happened while you worked. This is about your process, not trying to sound perfect.

## 1. What was broken when you started?

- What did the game look like the first time you ran it?
  - The first time I ran it, it was working fine. Problems began when I tried refreshing the game.
- **List at least two concrete bugs you noticed at the start**  
  - 2 concrete bugs I noticed at the start include:
    - The hints were inaccurate. As I guessed numbers, the hints were misguiding me.
    - New Game button does not reset the game, it only resets the developer debug chart.

---

## 2. How did you use AI as a teammate?

- Which AI tools did you use on this project (for example: ChatGPT, Gemini, Copilot)?
- Give one example of an AI suggestion you accepted and why.
- Give one example of an AI suggestion you changed or rejected and why.

---

## 3. Debugging and testing your fixes

- How did you decide whether a bug was really fixed?
  - I verified the bug was fixed by reproducing the original failure and then repeating the same steps after the change. I checked that the hint messages matched the numeric comparison (higher guess -> "Go LOWER", lower guess -> "Go HIGHER"). I also validated that the comparison still worked when the secret was stored as a string on even attempts. Finally, I watched the UI messages and outcomes to ensure they aligned with the expected game state.
- Describe at least one test you ran (manual or using pytest) and what it showed you about your code.
  - I ran pytest on `test_game_logic.py` and specifically checked the case where the secret is a string to avoid lexicographic mistakes. The test confirmed that `check_guess(60, "50")` returns `"Too High"` with the correct "Go LOWER" hint. I also manually entered guesses above and below the secret to confirm the hint direction in the UI. This showed the bug was fixed both at the logic level and in the app.
- Did AI help you design or understand any tests? How?
  - Yes, AI suggested adding a targeted test for the string secret case, which is the edge case that used to break the hint logic. It also helped update the tests to assert both the outcome and the hint message so the behavior is explicit; this made the test suite better at catching regressions in the future.

---

## 4. What did you learn about Streamlit and state?

- In your own words, explain why the secret number kept changing in the original app.
  - The original app regenerated the secret on each rerun due to the fact that it did not reliably store the value in session state.
- How would you explain Streamlit "reruns" and session state to a friend who has never used Streamlit?
  - Streamlit reruns is like a phone that updates every time you click settings while session state is your phone's memory that remembers your previous choices so they don't reset each time.
- What change did you make that finally gave the game a stable secret number?
  - The secret number was stored in `st.session_state` and was ONLY generated when the key didn't already exist.

---

## 5. Looking ahead: your developer habits

- What is one habit or strategy from this project that you want to reuse in future labs or projects?
  - The habit of testing and also writing clearer prompts. In my opinion, **clear prompt = accurate output**.
- What is one thing you would do differently next time you work with AI on a coding task?
  - Take more time to understand the code base in its totality + write more tests.
- In one or two sentences, describe how this project changed the way you think about AI generated code.
  - Showed me the speed in which code can be generated but also showed me the need to test as well.
