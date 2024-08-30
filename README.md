# Lesson Plan Generator

## Overview
This project is a FastAPI-based web application that leverages a Large Language Model (LLM) to automatically generate customized lesson plans for students. The application takes input parameters such as the subject, grade level, and specific topics, and uses the LLM to create detailed lesson plans tailored to the student's needs.

## Features
- **Custom Lesson Plans:** Generate lesson plans based on specific subjects, grade levels, and topics.
- **FastAPI Backend:** A high-performance, modern web framework that handles requests and responses.
- **LLM Integration:** Uses a powerful Large Language Model to create detailed and relevant lesson plans.

## Tech Stack
- **FastAPI:** High-performance web framework for building APIs.
- **LLM (Large Language Model):** AI model for generating lesson plans.
- **Python:** Core programming language for the application.

## Setup and Installation

### Prerequisites
- Python 3.9+
- Virtual environment tool (e.g., `venv` or `virtualenv`)

### Installation Steps

1. **Clone the repository:**
   ```bash
   git clone https://github.com/harshkasat/LessonPlan
   cd LessonPlan

2. **Create and activate a virtual environment:**
   ```bash
   python3 -m venv env
   source env/bin/activate  # On Windows, use `env\Scripts\activate`
3. **Install the required dependencies:**
    ```bash
    pip install -r requirements.txt
4. **Set up environment variables:**
- Create a .env file in the root directory and add any necessary environment variables for your LLM model and FastAPI configuration.
- ```bash
  GOOGLE_API_KEY = "YOUR API KEY"
5. **Run the FastAPI server:**
   ```bash
   uvicorn app:app --reload
