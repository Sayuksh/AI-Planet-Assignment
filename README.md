# AI Strategy Analysis Tool

URL - https://ai-planet-assignment-ayush.streamlit.app/
## Overview
The AI Strategy Analysis Tool is a Streamlit-based application that helps businesses identify AI/ML opportunities and generate comprehensive strategy reports. The tool analyzes companies, determines their industry, conducts market research, generates use cases, and creates detailed proposals.

## Features
- **Industry Classification**: Automatically identifies a company's primary industry
- **Market Research**: Gathers relevant industry and company insights using Serper API
- **AI/ML Use Case Generation**: Creates tailored AI/ML use cases for the company
- **Resource Collection**: Finds relevant datasets and resources for each use case
- **Comprehensive Report Generation**: Produces a detailed AI strategy proposal in markdown format

## Technical Architecture

### Core Components
1. **MarketResearchAgent**: The main class that handles all analysis functionality
2. **Streamlit UI**: User interface for interacting with the application
3. **API Integrations**: Serper for web search and Groq for AI text generation

### Dependencies
- Python 3.8+
- Streamlit 1.30.0+
- Groq 0.4.0+
- Autogen 0.2.0+
- Python-dotenv 1.0.0+
- Exa_py 0.1.0+

## Setup and Installation

### Prerequisites
- Python 3.8 or higher
- pip package manager
- API keys for Groq and Exa

### Installation Steps
1. Clone the repository
2. Create a virtual environment:
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```
3. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
4. Create a `.env` file with the following variables:
   ```
   GROQ_API_KEY="your_groq_api_key"
   EXA_API_KEY="your_exa_api_key"
   ```
5. Run the application:
   ```bash
   streamlit run main.py
   ```

## Detailed Component Documentation

### MarketResearchAgent Class

#### `__init__(self)`
Initializes the agent with API clients for Exa and Groq.

#### `determine_industry(self, company_name)`
Determines the primary industry of a company using AI analysis.
- **Parameters**: `company_name` (str) - Name of the company to analyze
- **Returns**: `industry` (str) - The identified industry name
- **Process**:
  1. Constructs a prompt asking for industry classification
  2. Uses Groq's LLM to analyze the company
  3. Processes the response to extract just the industry name
  4. Handles verbose responses with regex pattern matching
  5. Falls back to "Technology" if no industry can be determined

#### `research_company(self, company_name)`
Conducts comprehensive company and industry research.
- **Parameters**: `company_name` (str) - Name of the company to analyze
- **Returns**: 
  - `research_results` (dict) - Dictionary of research insights
  - `industry` (str) - The identified industry
- **Process**:
  1. Determines the company's industry
  2. Constructs search queries for industry trends, company position, and future outlook
  3. Uses Exa to search for relevant information
  4. Organizes results into a structured format

#### `generate_use_cases(self, company_name, industry, research_insights)`
Generates AI/ML use cases based on company research.
- **Parameters**:
  - `company_name` (str) - Name of the company
  - `industry` (str) - Industry of the company
  - `research_insights` (dict) - Research data from previous step
- **Returns**: `use_cases` (list) - List of AI/ML use cases
- **Process**:
  1. Constructs a prompt with company and industry context
  2. Uses Groq's LLM to generate use cases
  3. Parses the response into a list of distinct use cases

#### `collect_resource_assets(self, use_cases)`
Collects dataset resources for each use case.
- **Parameters**: `use_cases` (list) - List of AI/ML use cases
- **Returns**: `resource_map` (dict) - Mapping of use cases to relevant resources
- **Process**:
  1. For each use case, searches for relevant datasets on platforms like Kaggle, Hugging Face, and GitHub
  2. Filters results to ensure they're relevant to the use case
  3. Creates a mapping between use cases and resources

#### `generate_final_proposal(self, company_name, industry, use_cases, resource_map, research_insights)`
Creates a comprehensive markdown proposal.
- **Parameters**:
  - `company_name` (str) - Name of the company
  - `industry` (str) - Industry of the company
  - `use_cases` (list) - Generated AI/ML use cases
  - `resource_map` (dict) - Mapping of use cases to resources
  - `research_insights` (dict) - Research data
- **Returns**: `proposal` (str) - Markdown-formatted proposal
- **Process**:
  1. Creates a structured markdown document
  2. Includes sections for research insights, use cases, and resources
  3. Formats everything in a professional, readable manner

### Main Function
The `main()` function sets up the Streamlit UI and orchestrates the analysis process:
1. Configures the Streamlit page
2. Creates the UI with custom styling
3. Takes the company name as input
4. Executes the analysis in phases with progress indicators
5. Displays results in organized tabs

## API Integration Details

### Exa API
- **Purpose**: Web search for company and industry research
- **Endpoint**: https://api.exa.com
- **Authentication**: API key in request header
- **Usage**: Used in the `research_company` method to gather market insights
- **Note**: Serper API (https://google.serper.dev/search) was also tested as an alternative search provider

### Groq API
- **Purpose**: AI text generation for industry classification, use case generation, and proposal creation
- **Model**: llama-3.1-8b-instant (previously qwen-qwq-32b)
- **Authentication**: API key in client initialization
- **Usage**: Used throughout the application for AI-powered analysis
- **Advantage**: Chosen specifically for its very fast inference speed compared to other LLM providers

## Error Handling
The application includes robust error handling:
- API failures are caught and displayed to the user
- Industry classification has fallback mechanisms
- Resource collection handles missing or invalid results
- All critical functions have try-except blocks to prevent crashes

## UI Components
The Streamlit UI includes:
- Input field for company name
- Progress indicators for the analysis process
- Tabs for organizing different aspects of the analysis
- Metrics display for key statistics
- Download button for the final report

## Future Enhancements
Potential areas for improvement:
1. Add support for more detailed company analysis
2. Implement caching to improve performance
3. Add visualization of industry trends
4. Support for comparing multiple companies
5. Integration with more data sources

## Troubleshooting
Common issues and solutions:
- **API Key Errors**: Ensure all API keys are correctly set in the .env file
- **Rate Limiting**: If you encounter rate limiting, reduce the number of requests or upgrade your API plan
- **Memory Issues**: For very large reports, you may need to increase your system's memory allocation

## License
This project is licensed under the MIT License - see the LICENSE file for details.

## Author
Ayush Aditya | 2025 | AI Planet Project
