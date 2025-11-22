# teacher-assistant-crewai
A small crew-of-agents teacher assistant — converts raw lesson notes into a structured lesson plan, generates quizzes, and provides teaching advice. Built as a lightweight Python project demonstrating agent-task separation and simple mock "services" for education workflows.
teacher-assistant-crewai/
├── pyproject.toml (optional) or requirements.txt
├── src/
│ ├── main.py # CLI entrypoint for the teacher assistant
│ ├── crewai.py # Task & Agent helper classes (simple framework)
│ ├── dummy_services.py # Agents and fake generator functions
│ ├── tasks.py # Task definitions & service implementations
│ └── agents.py # Agent definitions used by crewai (if separated)
├── examples/
│ └── sample_notes.txt # Example lesson notes to try
└── .gitignore
Project description

This project demonstrates a small multi-agent (crew) architecture for educational content preparation. Given raw notes (from a text file, stdin, or CLI argument), the system will:

Generate a structured lesson plan

Generate a short quiz (multiple choice / short answer)

Provide teaching advice and tips

All generation is powered by simple deterministic / heuristic functions in tasks.py and exposed through dummy_services.py which declare Agent objects.

Installation

Create a virtual environment and install dependencies (if any). This project uses only Python standard library by default, so no extra packages are strictly required.
python -m venv .venv
source .venv/bin/activate # or .venv\Scripts\activate on Windows
pip install -r requirements.txt # optional if you add deps
Add a pyproject.toml if you want packaging metadata.

Usage

There are two main ways to run the assistant: as a CLI tool (recommended) and programmatically.

CLI
# 1) Using notes via CLI argument
python src/main.py --notes "Photosynthesis is the process by which plants convert light..."


# 2) Using a text file
python src/main.py --file examples/sample_notes.txt


# 3) Piped input
cat examples/sample_notes.txt | python src/main.py


# 4) Interactive fallback (if no args provided)
python src/main.py
# then paste notes when prompted
Programmatic (import)
from src.tasks import generate_lesson_plan, generate_quiz, generate_advice
notes = "A short lesson about photosynthesis and light-dependent reactions."
plan = generate_lesson_plan(notes)
quiz = generate_quiz(notes)
advice = generate_advice(notes)
print(plan, quiz, advice)
Example input

examples/sample_notes.txt (example content):
Expected output (terminal)

When running the CLI with the example notes above, you should see a structured printed output similar to:
===== Generated Lesson Plan =====
• Introduction: Photosynthesis is the process by which plants convert light energy into chemical energy
• Main Content: It includes light-dependent reactions and the Calvin cycle; This lesson will cover the main steps and highlight common misconceptions; The experiment will show oxygen evolution
• Practice: The experiment will show oxygen evolution
• Summary and Homework


===== Quiz =====
• What is the main topic of the lesson?
A. A related concept to consider
B. It includes light-dependent reactions and the Calvin cycle
C. Photosynthesis is the process by which plants convert light energy into chemical energy
Answer: C
• Name one key detail mentioned in the notes.
A. The experiment will show oxygen evolution
B. Photosynthesis is the process by which plants convert light energy into chemical energy
C. It includes light-dependent reactions and the Calvin cycle
Answer: A
• Define the term 'photosynthesis'.
A. Definition based on context: see notes — photosynthesis relates to the lesson content
B. It includes light-dependent reactions and the Calvin cycle
C. A related concept to consider
Answer: A


===== Teaching Advice =====
• Check for prior knowledge before introducing new topics
• Include a short formative assessment to check understanding

