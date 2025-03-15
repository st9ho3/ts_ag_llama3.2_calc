# Weather & Calculation AI Assistant

This project is an AI assistant built to provide practical weather advice and perform numerical calculations based on user prompts. It integrates with external APIs for real-time weather data and leverages local or cloud-based language models to process queries. The assistant can answer questions like "Should I take a jacket to LA?" or "What’s the sum of 5 and 10?" with clear, human-friendly responses.

## Features

1. **Weather Assistance**:
   - Normalizes abbreviated city names (e.g., "LA" to "Los Angeles").
   - Fetches real-time weather data using the OpenWeatherMap API.
   - Provides actionable advice (e.g., "Take a jacket if it’s chilly!").

2. **Numerical Calculations**:
   - Supports basic arithmetic operations: addition, subtraction, multiplication, and division.
   - Uses dedicated tools to ensure precise calculations with numerical inputs only.

3. **Dual Model Support**:
   - **Google Gemini**: Connects to the `gemini-2.0-flash` model via API for weather-related queries.
   - **Ollama with Llama 3.1**: Runs locally using the `llama3.1:latest` model for both weather and calculation tasks.

4. **Tool Integration**:
   - Custom tools for calculations and weather retrieval, defined with schemas using `zod`.
   - Extensible architecture for adding more tools.

## Prerequisites

- **Node.js**: Version 18.x or higher.
- **npm**: For package management.
- **dotenv**: To manage environment variables (e.g., API keys).
- **OpenWeatherMap API Key**: Required for weather data. Sign up [here](https://openweathermap.org/api) to get one.
- **Ollama**: For local model execution (optional, see below).

## Installation

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/your-username/your-repo-name.git
   cd your-repo-name
   ```

2. **Install Dependencies**:
   ```bash
   npm install
   ```
   This installs required packages, including:
   - `@google/generative-ai`
   - `@langchain/ollama`
   - `@langchain/core`
   - `zod`
   - `dotenv`

3. **Set Up Environment Variables**:
   Create a `.env` file in the root directory and add the following:
   ```env
   LLM_API=your-google-generative-ai-key  # Optional, for Google Gemini
   API_KEY=your-openweathermap-api-key    # Required for weather data
   ```
   - Replace `your-google-generative-ai-key` with your Google Generative AI API key (if using Gemini).
   - Replace `your-openweathermap-api-key` with your OpenWeatherMap API key.

4. **Install Ollama (For Local Model)**:
   - Download and install Ollama from [ollama.ai](https://ollama.ai/).
  
     ```bash
     ollama run llama3.1:latest
     ```
 
     Ensure it runs on `http://localhost:11434` (default).

## Usage

### Running with Google Gemini
Edit the prompt in `calGemini.ts` to test different queries (e.g., "Should I wear shorts in Seattle?"). Then run:
```bash
ts-node src/LLM/geminiLLM.ts
```
Requires `LLM_API` in `.env`.

### Running with Ollama (Local)
Edit the prompt in `llama.ts` (e.g., "Should I take a jacket to LA?"). Then run:
```bash
ts-node src/LLM/llama.ts
```
Requires Ollama running locally with `llama3.1:latest`.

### Example Outputs
- **Weather Query**: "Should I take a jacket to LA?"
  - Response: "In Los Angeles, it’s warm today, so you might not need a jacket—just a light layer should do!"
- **Calculation Query**: "What’s 5 plus 10?"
  - Response: "The sum of 5 and 10 is 15."

## Project Structure

- **`geminiLLM.ts`**: Handles weather queries using Google Gemini.
- **`llama.ts`**: Manages both weather and calculation queries using Ollama locally.
- **`tools.ts`**: Defines calculation and weather tools with `zod` schemas.
- **`api.ts`**: Implements the weather API call to OpenWeatherMap.
- **`messages.ts`**: Contains system prompts for weather and calculation logic.

## Extending the Assistant

- **Add New Tools**: Define new functions in `tools.ts` and register them in the `tools` array.
- **Custom Prompts**: Modify `messages.ts` to tweak the assistant’s behavior or tone.

## Limitations

- Requires an internet connection for weather data and Google Gemini.
- Local Ollama execution depends on sufficient hardware (e.g., RAM for `llama3.1`).
- Error handling assumes undefined responses are gracefully managed.

## Contributing

Feel free to submit issues or pull requests to enhance functionality, fix bugs, or improve documentation.

## License

MIT License. See [LICENSE](LICENSE) for details.
