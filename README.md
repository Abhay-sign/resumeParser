# AI-Powered Resume Parser & Job Matcher

An AI-powered resume screening tool built with Python, Groq's LLM API, and Pydantic. It extracts structured information from resumes, analyzes job descriptions, evaluates candidate-job compatibility, and ranks candidates based on their match scores.

## Features

- **Resume Parsing:** Extracts candidate details, skills, education, work experience, projects, and certifications.
- **Multiple File Formats:** Supports PDF and DOCX resumes.
- **Job Description Analysis:** Extracts job roles, required skills, preferred skills, education requirements, responsibilities, and minimum experience.
- **AI-Powered Matching:** Compares candidate profiles against job requirements using an LLM.
- **Structured Output:** Uses Pydantic models to validate extracted information.
- **Candidate Ranking:** Sorts candidates by match score and displays the top and lowest-scoring candidates.
- **Flexible Resume Interpretation:** Recognizes information across different resume section headings rather than relying only on exact labels.

## Tech Stack

- **Language:** Python
- **LLM API:** Groq
- **Model:** `qwen/qwen3.8-27b` (as configured in the source code)
- **Data Validation:** Pydantic
- **PDF Processing:** pypdf
- **Word Document Processing:** python-docx
- **Environment Variables:** python-dotenv

## How It Works

1. **Load the job description:** The application provides a job description for the target position.
2. **Extract job requirements:** The LLM converts the description into structured JSON containing skills, responsibilities, education requirements, and other relevant details.
3. **Read resumes:** The application reads PDF and DOCX files from the `resumes/` directory.
4. **Parse candidate profiles:** The LLM extracts candidate information into a structured resume model.
5. **Calculate match scores:** The LLM compares each candidate's profile with the job requirements and returns a score and supporting details.
6. **Rank candidates:** Candidates are sorted by their scores, and the application displays the top two and lowest two candidates.

## Project Structure

```text
day5/
├── resume_parser.py
├── resumes/              # Local sample resumes (not committed)
├── src/
│   └── day5/
│       └── __init__.py
├── .env                  # API key (not committed)
├── .env.example          # Example environment configuration
├── .gitignore
├── pyproject.toml
├── uv.lock
└── README.md
```

## Prerequisites

- Python version compatible with your project configuration
- A Groq API key
- Sample resumes in PDF or DOCX format
- [uv](https://docs.astral.sh/uv/) for dependency management, if using the existing `uv.lock` and `pyproject.toml`

## Installation and Setup

### 1. Clone the repository

```bash
git clone https://github.com/Abhay-sign/resumeParser.git
cd resumeParser
```

### 2. Install dependencies

If the project is configured for `uv`:

```bash
uv sync
```

Otherwise, install the dependencies declared in `pyproject.toml` using your chosen Python package manager.

### 3. Configure environment variables

Create a `.env` file in the project root:

```env
GROQ_API_KEY=your_groq_api_key_here
```

Never commit your real API key. Keep `.env` in `.gitignore`.

### 4. Add resumes

Create a `resumes/` folder and place the PDF and DOCX files you want to analyze inside it.

**Privacy note:** Only process resumes you have permission to use. Resumes contain personal information, so avoid uploading them to a public repository.

### 5. Run the application

```bash
uv run python resume_parser.py
```

If you are not using `uv`, activate your Python environment and run:

```bash
python resume_parser.py
```

## Example Output

The application prints the match score and evaluation details for each candidate, followed by ranked results.

```text
Processing: candidate_resume.pdf
Score: 85.0

TOP 2 CANDIDATES
Candidate A - 85.0 %
Candidate B - 72.0 %

LOWEST 2 CANDIDATES
Candidate C - 48.0 %
Candidate D - 35.0 %
```

*Illustrative output only. Actual scores and candidate details depend on the resumes, job description, and LLM responses.*

## Data Models

The application uses Pydantic models to represent structured data.

### Job Description

- Role
- Required skills
- Preferred skills
- Minimum experience
- Education requirements
- Responsibilities

### Resume

- Name, email, and phone
- Total experience in years
- Skills
- Work experience and internships
- Education
- Projects
- Certifications

### Match Result

- Overall match score
- Evaluation details, such as matching skills, missing skills, experience alignment, and final verdict

## Current Limitations

- The job description is currently defined in the Python source code.
- Resumes are read from a local directory rather than uploaded through a web interface.
- PDF text extraction may not work for scanned documents that require OCR.
- The application makes separate LLM calls for parsing resumes and evaluating candidates, which can increase latency and API usage.
- The match score is an AI-generated estimate, not a guaranteed measure of candidate suitability.
- The current implementation processes candidates sequentially and uses fixed delays between API calls.

## Future Improvements

- Add a web interface for uploading resumes and job descriptions.
- Support multiple job descriptions and configurable matching criteria.
- Add OCR support for scanned resumes.
- Export candidate rankings to CSV or Excel.
- Add automated tests, structured logging, and error handling.
- Improve batch processing, retry handling, and API rate-limit management.
- Add privacy controls and secure handling of candidate data.

## Security and Privacy

- Store API keys in environment variables.
- Never commit `.env` files or real credentials.
- Keep personal resumes out of public Git repositories.
- Review AI-generated candidate evaluations before making hiring decisions.

## Author

**Abhay Singh**

- GitHub: [Abhay-sign](https://github.com/Abhay-sign)

---

*Built as a Python project exploring LLM-based information extraction, structured data validation, and AI-assisted candidate-job matching.*
