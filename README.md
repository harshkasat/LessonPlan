# Lesson Plan Generator

This project is a lesson plan generator built using CrewAI, a framework for building collaborative agents.  It leverages Google's Gemini API for natural language processing and various other libraries for web scraping, data processing, and API interaction.  The application generates lesson plans based on specified subject and grade level.

## Purpose and Features

The core purpose is to automate the creation of lesson plans, saving educators time and effort.  Key features include:

* **Subject and Grade Level Input:**  Users specify the subject and grade level to generate a tailored lesson plan.
* **Collaborative Agent System:** Uses CrewAI to orchestrate multiple agents (Research Analyst, Teacher Analyst, Supervisor Analyst) to create a comprehensive plan.
* **Data Sources:** Leverages Wikipedia and DuckDuckGo for research.
* **Google Gemini Integration:** Utilizes the Gemini 2.0 flash model for natural language generation and understanding.
* **FastAPI Web Service:** Exposes the functionality via a RESTful API.

## Code Details

The project consists of several Python files:

* **`app.py` (FastAPI application):** This file defines the API endpoints.  The main function `lessonplan` receives subject and grade as input, creates a `LessonPlanCrew` instance, and returns the generated lesson plan.

```python
@app.post('/lessonplan/')
async def lessonplan(query:Query):
    try:
        subject = query.subject
        grade = query.grade
        lesson_plan_crew = LessonPlanCrew(subject=subject, grade=grade)
        response = await lesson_plan_crew.run()
        print("\n\n########################")
        print(f"## Here is the Lesson for {subject} and {grade} ")
        print("########################\n")
        print(response)
        return {"detail":f'{response}'}
    except Exception as e:
        raise HTTPException(status_code=400, detail=e)
```

* **`main.py`:** This file defines the `LessonPlanCrew` class, which orchestrates the different agents and tasks.

```python
class LessonPlanCrew:
    async def run(self):
        agents = LessonPlanAgents()
        tasks = LessonPlanTasks()
        # ... agent and task initialization ...
        crew = Crew(agents=[...], tasks=[...], verbose=True)
        result = crew.kickoff()
        return result
```

* **`Agents/lesson_plan_agent.py`:** This file defines the different agents using the CrewAI framework.  Each agent has a specific role, goal, backstory, and tools.  For example, the `research_analyst` uses `WikiSearch` to gather information.

```python
class LessonPlanAgents:
    def research_analyst(self):
        return Agent(role='Staff Research Analyst', goal="...", backstory="...", tools=[WikiSearch.search_wikipedia], llm=llm)
    # ... other agents ...
```

* **`Tasks/lesson_plan_tasks.py` (not fully shown):**  This file likely defines the tasks each agent performs.


* **`Tools/content_tools.py` and `Tools/search_tools.py` (not fully shown):** These files likely contain functions for interacting with Wikipedia and DuckDuckGo.


## Setup and Usage

1. **Install Dependencies:** Install the required Python packages listed in `requirements.txt`.  Note that there are two `requirements.txt` files;  ensure you use the one containing all necessary packages.  You'll need to create a virtual environment.

2. **Set Environment Variables:**  Set the `GOOGLE_API_KEY` environment variable with your Google Cloud API key.  This key is necessary for using the Google Gemini API.

3. **Run the Application:**  Run the `app.py` file using Uvicorn.  For example: `uvicorn app:app --reload`.

4. **Send API Request:** Send a POST request to `/lessonplan/` with a JSON payload containing the `subject` and `grade`.  For example:

```bash
curl -X POST -H "Content-Type: application/json" -d '{"subject": "Mathematics", "grade": "5"}' http://localhost:8000/lessonplan/
```

This will return a JSON response containing the generated lesson plan.


## Limitations

The provided code snippets only show parts of the project.  The full functionality and details of the `LessonPlanTasks` and tools modules are not available for a complete analysis.  The performance and scalability of the system are also unknown without further information and testing.  Error handling within the agents and tasks is crucial for robustness but isn't fully detailed in the provided code.
