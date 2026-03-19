```markdown
# 📚 RAG-Based AI Teaching Assistant

<div align="center">

![GitHub stars](https://img.shields.io/github/stars/AyushBorse/RAG-Based-AI-Teaching-Assistant?style=for-the-badge)](https://github.com/AyushBorse/RAG-Based-AI-Teaching-Assistant/stargazers)
[![GitHub forks](https://img.shields.io/github/forks/AyushBorse/RAG-Based-AI-Teaching-Assistant?style=for-the-badge)](https://github.com/AyushBorse/RAG-Based-AI-Teaching-Assistant/network)
[![GitHub issues](https://img.shields.io/github/issues/AyushBorse/RAG-Based-AI-Teaching-Assistant?style=for-the-badge)](https://github.com/AyushBorse/RAG-Based-AI-Teaching-Assistant/issues)
[![GitHub license](https://img.shields.io/github/license/AyushBorse/RAG-Based-AI-Teaching-Assistant?style=for-the-badge)](LICENSE) <!-- TODO: Add actual license file and link -->
[![Python](https://img.shields.io/badge/Python-3.8%2B-blue?style=for-the-badge&logo=python)](https://www.python.org/)

**Leverage Retrieval-Augmented Generation (RAG) to create an intelligent AI teaching assistant from video and audio content.**

</div>

## 📖 Overview

The RAG-Based AI Teaching Assistant is a Python-powered workflow designed to transform educational video and audio materials into an interactive knowledge base. It processes raw media (videos, MP3s), transcribes them, extracts relevant information, and then uses a Retrieval-Augmented Generation (RAG) system to answer user queries based on this content. This project enables educators and learners to create dynamic Q&A systems from their existing media archives, providing a personalized and efficient learning experience.

## ✨ Features

-   **Video to Audio Conversion**: Automatically converts video files (e.g., lectures, tutorials) into MP3 audio format.
-   **Audio Transcription**: Transcribes MP3 audio files into structured JSON text data, making spoken content searchable and processable.
-   **Text Preprocessing & Embedding**: Preprocesses transcribed text, chunking it into manageable segments and generating vector embeddings for efficient semantic search.
-   **Intelligent RAG Querying**: Utilizes the Retrieval-Augmented Generation (RAG) pattern to retrieve contextually relevant information from the processed knowledge base and synthesize accurate, informed responses using a Large Language Model (LLM).
-   **Customizable AI Prompt**: Allows easy modification of the AI's core instructions, persona, and response guidelines via a dedicated `prompt.txt` file.

## 🛠️ Tech Stack

This project is built primarily with Python and leverages several powerful tools and concepts for media processing and AI capabilities.

**Core Technologies:**
-   **Python**: The primary programming language for all scripts and orchestration.
-   **Retrieval-Augmented Generation (RAG)**: The architectural pattern enhancing LLM responses with external, domain-specific knowledge.
-   **Large Language Models (LLMs)**: Utilized for generating answers based on retrieved context (e.g., OpenAI GPT series, Llama, etc. - *requires external API access*).
-   **Vector Store/Database**: (Inferred for RAG) For efficient storage and semantic search of document embeddings (e.g., ChromaDB, FAISS).
-   **ffmpeg**: (External dependency) A robust, open-source tool essential for handling video and audio file conversions.

**Inferred Python Libraries (Common for this domain):**
-   [`python-dotenv`](https://pypi.org/project/python-dotenv/): For managing environment variables.
-   [`pydub`](https://pypi.org/project/pydub/): For high-level audio manipulation in Python.
-   [`SpeechRecognition`](https://pypi.org/project/SpeechRecognition/) / [`transformers`](https://huggingface.co/docs/transformers/model_doc/whisper) (Whisper): For converting speech to text.
-   [`LangChain`](https://python.langchain.com/) / [`LlamaIndex`](https://www.llamaindex.ai/): For orchestrating the RAG pipeline, including document loading, chunking, embedding, and LLM integration.
-   [`openai`](https://pypi.org/project/openai/): Python client for OpenAI API interaction.

## 🚀 Quick Start

Follow these steps to set up and run the RAG-Based AI Teaching Assistant locally.

### Prerequisites
-   **Python 3.8+**: Ensure Python is installed on your system.
-   **pip**: Python package installer.
-   **ffmpeg**: Required for video-to-audio conversion. Install it via your system's package manager (e.g., `sudo apt install ffmpeg` on Ubuntu, `brew install ffmpeg` on macOS, or download from [ffmpeg.org](https://ffmpeg.org/download.html)).
-   **OpenAI API Key** (or similar LLM provider): Essential for interacting with the Large Language Model.

### Installation

1.  **Clone the repository**
    ```bash
    git clone https://github.com/AyushBorse/RAG-Based-AI-Teaching-Assistant.git
    cd RAG-Based-AI-Teaching-Assistant
    ```

2.  **Install Python dependencies**
    *   **Note**: A `requirements.txt` file is not present in this repository, which typically lists all necessary Python libraries. You will need to manually install the libraries required for your chosen speech-to-text, LLM integration, and embedding models.
    *   **Example common installations**:
        ```bash
        pip install python-dotenv pydub SpeechRecognition moviepy # Basic media/env
        pip install langchain openai chromadb # Example RAG-related libraries
        # Add any other specific libraries based on your implementation
        ```

3.  **Environment setup**
    Create a `.env` file in the project's root directory to store your API keys and other sensitive configurations.
    ```bash
    # .env example
    OPENAI_API_KEY="YOUR_OPENAI_API_KEY_HERE"
    # Add other keys/configs as needed, e.g., HUGGINGFACE_API_KEY, ANTHROPIC_API_KEY
    ```

### Usage Workflow

The project consists of several Python scripts designed to be executed in a logical sequence to build and interact with the AI Teaching Assistant.

1.  **Convert Video to MP3 (Optional)**
    If your source material is in video format, convert it to an MP3 audio file first.
    ```bash
    python video_to_mp3.py <input_video_path> <output_mp3_path>
    ```
    *Example:* `python video_to_mp3.py "path/to/my_lecture.mp4" "path/to/my_lecture.mp3"`

2.  **Transcribe MP3 to JSON**
    Transcribe the MP3 audio files into a JSON format containing the raw text. This JSON will serve as the initial raw data for your knowledge base.
    ```bash
    python mp3_to_json.py <input_mp3_path> <output_json_path>
    ```
    *Example:* `python mp3_to_json.py "path/to/my_lecture.mp3" "path/to/my_lecture_transcript.json"`

3.  **Preprocess JSON Data**
    Process the generated JSON transcript. This script is responsible for steps like chunking the text into smaller, manageable pieces, generating vector embeddings for each chunk, and storing these embeddings in a vector database for efficient retrieval.
    ```bash
    python preprocess_json.py <input_json_path>
    ```
    *Example:* `python preprocess_json.py "path/to/my_lecture_transcript.json"`

4.  **Process Incoming Query (RAG)**
    This is the core script for running the RAG process. It takes a user query, performs a semantic search on your vector store to retrieve relevant document chunks, and then uses an LLM (guided by `prompt.txt`) to synthesize an informed answer.
    ```bash
    python process_incoming.py "<your_query_here>"
    ```
    *Example:* `python process_incoming.py "What were the key takeaways from the discussion on historical events?"`

    The `prompt.txt` file is dynamically loaded by `process_incoming.py` to establish the LLM's role and provide specific instructions, ensuring the AI maintains the persona of a teaching assistant.

## 📁 Project Structure

```
RAG-Based-AI-Teaching-Assistant/
├── .gitignore               # Specifies intentionally untracked files to ignore
├── Readme.md                # Project documentation (this file)
├── mp3_to_json.py           # Script to transcribe MP3 audio to JSON
├── preprocess_json.py       # Script for preparing JSON data for RAG (chunking, embeddings)
├── process_incoming.py      # Main script for handling RAG queries and generating responses
├── prompt.txt               # Customizable AI prompt/system message for the LLM
├── response.txt             # Placeholder or example for AI response output
├── video_to_mp3.py          # Script to convert video files to MP3 format
└── unused/                  # An empty directory (currently unused, may be for future features)
```

## ⚙️ Configuration

### Environment Variables
The `.env` file, which you will create, is used to store sensitive information and API keys required by the scripts.

| Variable | Description | Default | Required |
|----------|-------------|---------|----------|
| `OPENAI_API_KEY` | Your API key for accessing OpenAI's Large Language Models. | None | Yes |
| `[OTHER_LLM_API_KEY]` | API key for alternative LLM providers (e.g., Anthropic, Hugging Face). | None | No |

### Configuration Files
-   **`prompt.txt`**: This critical file contains the system prompt for the Large Language Model. Customize this file to define the AI's persona, its guiding principles, specific instructions for answering questions, and its overall teaching style.

## 🤝 Contributing

We welcome contributions to enhance the RAG-Based AI Teaching Assistant! If you're interested in improving this project, please consider:

-   Adding support for more media types (e.g., PDF, DOCX).
-   Integrating different speech-to-text services or local models.
-   Implementing various vector store options.
-   Improving the RAG pipeline with advanced chunking or retrieval strategies.
-   Enhancing the prompt engineering.

Please see our [Contributing Guide](CONTRIBUTING.md) <!-- TODO: Create CONTRIBUTING.md --> for details on how to get started.

### Development Setup for Contributors
Ensure you have all prerequisites installed and follow the "Quick Start" installation steps. Focus on maintaining modularity and clear code for each processing step.

## 📄 License

This project is currently without a specified license. Please consider adding a `LICENSE` file to define the terms of use and distribution. <!-- TODO: Add actual license file and link -->

## 🙏 Acknowledgments

-   The developer, [AyushBorse](https://github.com/AyushBorse), for initiating this valuable project.
-   The open-source community for providing powerful Python libraries and tools that make advanced AI applications like RAG possible.
-   The research on [Retrieval-Augmented Generation (RAG)](https://arxiv.org/abs/2005.11401) for the fundamental architectural pattern.

## 📞 Support & Contact

-   🐛 Issues: For bug reports or feature requests, please use the [GitHub Issues](https://github.com/AyushBorse/RAG-Based-AI-Teaching-Assistant/issues) page.

---

<div align="center">

**⭐ Star this repo if you find it helpful!**

Made with ❤️ by [AyushBorse](https://github.com/AyushBorse)

</div>
```
