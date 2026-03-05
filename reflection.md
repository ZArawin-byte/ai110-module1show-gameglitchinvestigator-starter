# 💭 Reflection: Game Glitch Investigator

Answer each question in 3 to 5 sentences. Be specific and honest about what actually happened while you worked. This is about your process, not trying to sound perfect.

## 1. What was broken when you started?

- What did the game look like the first time you ran it?
- List at least two concrete bugs you noticed at the start  
  (for example: "the secret number kept changing" or "the hints were backwards").

---The hints were backwards when I guessed a number that was too high, like 90 when the secret was 83, but the game told me to go higher instead of lower. The secret number was also impossible to guess on even attempts because the game was secretly converting it to a string, so comparing my integer guess to a string always failed. The third bug was the new game button not fully resetting the game, it kept the old status so if you lost you couldn't actually play again.

## 2. How did you use AI as a teammate?

- Which AI tools did you use on this project (for example: ChatGPT, Gemini, Copilot)?
- Give one example of an AI suggestion that was correct (including what the AI suggested and how you verified the result).
- Give one example of an AI suggestion that was incorrect or misleading (including what the AI suggested and how you verified the result).

---I used Claude to help me fix the bugs. One thing Claude got right was identifying that the check_guess function had reversed hint messages and suggesting to flip "Go higher" and "Go lower", I verified it by playing the game and the hints made sense after. But Claude also misled me at first with the hint messages in logic_utils.py, it still had the wrong direction in there even after fixing app.py, so I had to go back and fix logic_utils.py separately to match.

## 3. Debugging and testing your fixes

- How did you decide whether a bug was really fixed?
- Describe at least one test you ran (manual or using pytest)  
  and what it showed you about your code.
- Did AI help you design or understand any tests? How?

---I played the game manually after each fix to see if it was actually working. I also ran pytest in the terminal and all 3 tests passed, which showed me that check_guess was returning the right outcomes for winning, guessing too high, and guessing too low. Claude helped me understand what the tests were checking but I ran them myself to confirm.

## 4. What did you learn about Streamlit and state?

- In your own words, explain why the secret number kept changing in the original app.
- How would you explain Streamlit "reruns" and session state to a friend who has never used Streamlit?
- What change did you make that finally gave the game a stable secret number?

---The secret number kept changing because every time you clicked a button, Streamlit reruns the whole file from top to bottom, so it kept generating a new random number every click. Streamlit reruns are like refreshing a page, everything resets unless you save it in session_state which is like a memory that sticks around between those reruns. The fix was making sure the secret was only set once using "if secret not in st.session_state" so it wouldn't regenerate every time.

## 5. Looking ahead: your developer habits

- What is one habit or strategy from this project that you want to reuse in future labs or projects?
  - This could be a testing habit, a prompting strategy, or a way you used Git.
- What is one thing you would do differently next time you work with AI on a coding task?
- In one or two sentences, describe how this project changed the way you think about AI generated code.

---One habit I want to keep is running pytest after every fix so I know right away if something broke. Next time I would double check every file the AI touches because it fixed the bug in one place but left the same mistake in another file. This project made me realize AI generated code can look correct but still have hidden bugs, you really have to actually play or test it yourself to know if it works.
