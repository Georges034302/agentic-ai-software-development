
# Lab 1: Set Up the Agentic Dev Environment — Agentic Loop Demo

> **Pairs with:** [Module 1 — Set Up the Agentic Dev Environment](../modules/Module_1_Set_Up_the_Agentic_Dev_Environment.md). Read §1.1 (the agent loop), §1.4 (concept map), and §1.6 (environment setup) before starting.

## Objective

Experience the agentic loop hands-on by automating a real software development task. This is a **learning scaffold**—not agent development. You will:

- Implement a minimal **plan → act → observe → adapt** loop in Python (mirroring Module 1 §1.1)
- Use real tools (`subprocess`, file I/O) to act on code and observe results
- Map each Module 1 concept to a concrete line of code

> **Goal:** *Add unit tests for an existing Python module, run them, and adapt on failure.*

**This is a one-time demo to make agentic AI concrete. The rest of the course uses production agent tools.**

### Concept → Code Map (see Module 1 §1.4)

| Module 1 Concept | Where it lives in this lab |
|---|---|
| **Goal** | The string passed to `agentic_loop(...)` |
| **Plan** | `plan()` function |
| **Act** | `act()` function (writes test, runs tests) |
| **Observe** | `observe()` function (parses results) |
| **Adapt** | `adapt()` function, `max_retries` |
| **Tool use** | File I/O, `subprocess` |
| **Guardrail** | `max_retries=3` |

---

def add(a, b):
def subtract(a, b):

## Step 1: Prepare the Python App

Your "agent" will add a unit test for an existing backend Python function. Set up the code to be tested:

```bash
mkdir backend_app
cd backend_app
```

Create `backend_app/app.py`:

```python
def add(a, b):
    return a + b


    return a - b

if __name__ == "__main__":
    print("2 + 3 =", add(2, 3))
    print("5 - 2 =", subtract(5, 2))
```

Test it:

```bash
python app.py
# 2 + 3 = 5
# 5 - 2 = 3
```

Your agentic loop will generate and run a test file for `add()` and `subtract()`.
---

## Step 2: Implement the Agentic Loop (Driving Step 1)

Now write an agent that takes the Step 1 app as input and produces the test file automatically. The loop must:

1. Accept the goal: `"Add a unit test for add() and subtract() in backend_app/app.py"`
2. **Plan** the steps to add the test
3. **Act** — write `backend_app/test_app.py` to disk
4. **Observe** — run the tests and capture pass/fail
5. **Adapt** — retry or fix on failure

Save this as `backend_app/agent_loop.py` (next to `app.py` from Step 1):

```python
import os
import subprocess
import time

# The test file content the agent will write — targets the Step 1 app
TEST_FILE_CONTENT = '''import unittest
from app import add, subtract

class TestCalculator(unittest.TestCase):
    def test_add(self):
        self.assertEqual(add(2, 3), 5)
        self.assertEqual(add(-1, 1), 0)
        self.assertEqual(add(0, 0), 0)

    def test_subtract(self):
        self.assertEqual(subtract(5, 2), 3)
        self.assertEqual(subtract(0, 0), 0)
        self.assertEqual(subtract(-1, -1), 0)

if __name__ == "__main__":
    unittest.main()
'''

TEST_FILE_PATH = os.path.join(os.path.dirname(__file__), "test_app.py")

def plan(goal):
    return [
        "Write test_app.py with unit tests for add() and subtract()",
        "Run the test suite with unittest",
        "Check if all tests pass",
    ]

def act(step):
    print(f"Acting: {step}")
    if step.startswith("Write"):
        with open(TEST_FILE_PATH, "w") as f:
            f.write(TEST_FILE_CONTENT)
        return "test file written"
    if step.startswith("Run"):
        result = subprocess.run(
            ["python", "-m", "unittest", "test_app.py", "-v"],
            cwd=os.path.dirname(__file__),
            capture_output=True, text=True,
        )
        return result.stdout + result.stderr
    if step.startswith("Check"):
        return "checked"
    return "no-op"

def observe(action_result):
    if "OK" in action_result or "test file written" in action_result:
        return f"success: {action_result.splitlines()[-1]}"
    if "FAILED" in action_result or "Error" in action_result:
        return f"failure: {action_result}"
    return f"observed: {action_result}"

def adapt(observation, steps):
    print(f"Adapting due to: {observation}")
    # Simple adapt strategy: re-plan from scratch
    return steps

def agentic_loop(goal, max_retries=3):
    print(f"Goal: {goal}")
    steps = plan(goal)
    print(f"Plan: {steps}")
    attempts = 0
    while attempts < max_retries:
        success = True
        for step in steps:
            result = act(step)
            obs = observe(result)
            print(f"Observation: {obs}")
            if obs.startswith("failure"):
                success = False
                steps = adapt(obs, steps)
                break
        if success:
            print("Goal achieved!")
            return
        attempts += 1
        time.sleep(1)
    print("Max retries reached. Best effort complete.")

if __name__ == "__main__":
    agentic_loop("Add a unit test for add() and subtract() in backend_app/app.py")
```

**How Step 2 uses Step 1:**
- The agent's `act()` function imports from `app.py` (the Step 1 module) by writing a test file in the same folder.
- `subprocess.run([...])` executes the tests against the real Step 1 code — this is the **observe** phase grounded in actual program behavior.
- If you change `app.py` (e.g., break `add()`), re-running the loop will observe a failure and trigger **adapt**.

---

## Step 3: Run and Observe

From the repo root:

```bash
cd backend_app
python agent_loop.py
```

Expected (abridged) output:

```
Goal: Add a unit test for add() and subtract() in backend_app/app.py
Plan: ['Write test_app.py ...', 'Run the test suite ...', 'Check if all tests pass']
Acting: Write test_app.py ...
Observation: success: test file written
Acting: Run the test suite ...
Observation: success: OK
Acting: Check if all tests pass
Observation: success: checked
Goal achieved!
```

After the run, confirm `backend_app/test_app.py` now exists and matches the content shown in Step 1.

---

## Step 4: Reflection (tie back to Module 1)

Answer briefly, citing Module 1 sections where relevant:

1. **Loop (§1.1).** Walk through one full *plan → act → observe → adapt* cycle in your run. Which line of `agent_loop.py` corresponds to each phase?
2. **Spectrum (§1.1).** Where does this script sit on the autocomplete → chatbot → pair programmer → agent spectrum, and *why*?
3. **Anatomy (§1.1).** Which of the five engineering surfaces (goal, tools, memory, guardrails, loop) are present in your code? Which are stubbed?
4. **Why software dev (§1.2).** What verifiable signal does your agent rely on, and what would happen if you removed it?
5. **Next steps.** Name one concrete extension for each missing surface (memory, richer guardrails, more tools) — these are previews of Modules 3 and 4.

---

## Deliverables
- `backend_app/app.py` (Step 1)
- `backend_app/agent_loop.py` (Step 2) — your agentic loop with comments
- `backend_app/test_app.py` — written by the agent, not by you
- A sample run log from Step 3
- Short reflection answers from Step 4

---

**Proceed to [Lab 2](Lab_2_Drive_Agents_with_Prompts_and_Specs.md) when your loop runs to `Goal achieved!` and `test_app.py` exists.**

