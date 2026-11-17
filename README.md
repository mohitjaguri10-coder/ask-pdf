# Ask-Pdf

This project is a full-stack application for PDF processing and question-answering using AI technologies. It consists of a Python backend API and a React frontend interface.

## 🏗️ Project Structure

```
Ask-Pdf/
├── backend/                 # Python Flask/FastAPI backend
│   ├── main.py             # Main application entry point
│   ├── clients/            # External service clients
│   │   ├── pinecone_client.py
│   │   └── supabase_client.py
│   ├── routes/             # API route handlers
│   │   ├── ask_question.py
│   │   ├── pdf_routes.py
│   │   └── process.py
│   └── services/           # Business logic services
│       ├── downloader.py
│       ├── embedder.py
│       ├── extractor.py
│       ├── llama_query.py
│       ├── pdf_service.py
│       └── processor.py
└── frontend/               # React frontend application
    ├── src/
    ├── public/
    └── package.json
```

## 🚀 Features

- **PDF Processing**: Upload and process PDF documents
- **AI-Powered Q&A**: Ask questions about uploaded documents
- **Vector Storage**: Efficient document embedding and retrieval
- **Modern UI**: React-based frontend with TypeScript support

## 🧠 AI Question Answering Capabilities

The system now supports **Hybrid AI Responses** that intelligently combine document-specific information with general knowledge:

### Question Types Supported:

1. **Document-Specific Questions**: 
   - "What does this document say about X?"
   - "Summarize this PDF"
   - "According to this document..."
   
2. **General Knowledge Questions**:
   - "What is artificial intelligence?"
   - "How does machine learning work?"
   - "Explain neural networks"

3. **Hybrid Questions** (Document + General Knowledge):
   - "How does this approach compare to industry standards?"
   - "What are the implications of these findings?"
   - "Can you explain the concepts mentioned here?"

### How It Works:

- **Smart Classification**: The system automatically classifies questions to determine the best response approach
- **Context Retrieval**: Retrieves relevant chunks from the uploaded PDF using vector similarity search  
- **Intelligent Prompting**: Creates tailored prompts based on question type and available context
- **Fallback Handling**: Gracefully handles cases where PDF content isn't relevant to the question
- **Source Attribution**: Clearly indicates whether information comes from the document or general knowledge

This ensures users get comprehensive, accurate answers whether they're asking about their specific document or seeking general information.

## 🛠️ Technologies Used

### Backend
- **Python** - Core programming language
- **Pinecone** - Vector database for embeddings
- **Supabase** - Database and backend services
- **LLaMA** - Large language model for question answering

### Frontend
- **React** - Frontend framework
- **TypeScript** - Type-safe JavaScript
- **Vite** - Build tool and development server

## 🏛️ System Architecture

### High-Level Architecture

```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   React Frontend│    │  FastAPI Backend│    │  External APIs  │
│                 │    │                 │    │                 │
│  - TypeScript   │◄──►│  - Python       │◄──►│  - Supabase DB  │
│  - Vite         │    │  - FastAPI      │    │  - Pinecone VDB │
│  - Tailwind CSS │    │  - Uvicorn      │    │  - Groq/LLaMA   │
└─────────────────┘    └─────────────────┘    └─────────────────┘
```

### Component Architecture

```
Frontend (React/TypeScript)
├── Components
│   ├── ChatInterface       # Main chat UI
│   ├── PDFUpload          # File upload component
│   ├── ThemeProvider      # Dark/Light mode
│   └── UI Components      # Reusable UI elements
├── Services
│   ├── API Client         # Backend communication
│   └── User Service       # User session management
└── State Management       # React state and context

Backend (FastAPI/Python)
├── Routes
│   ├── PDF Routes         # File upload/processing
│   ├── Chat Routes        # Chat management
│   ├── Question Routes    # Q&A endpoints
│   └── Process Routes     # PDF processing pipeline
├── Services
│   ├── PDF Service        # PDF handling and storage
│   ├── Embedder Service   # Text embedding generation
│   ├── LLaMA Query        # AI question answering
│   ├── Extractor Service  # Text extraction from PDFs
│   └── Processor Service  # Orchestrates PDF processing
├── Clients
│   ├── Supabase Client    # Database operations
│   └── Pinecone Client    # Vector database operations
└── Models                 # Pydantic data models

External Services
├── Supabase
│   ├── PostgreSQL DB     # Relational data (chats, messages)
│   └── Storage Bucket    # PDF file storage
├── Pinecone Vector DB    # Document embeddings
└── Groq/LLaMA API       # Large Language Model
```

### Data Flow

1. **PDF Upload & Processing**:
   ```
   User uploads PDF → FastAPI receives file → Store in Supabase Storage
   → Extract text → Generate embeddings → Store in Pinecone → Return file_id
   ```

2. **Chat Creation**:
   ```
   Frontend creates chat → Store chat metadata in Supabase
   → Associate with PDF file_id → Return chat_id
   ```

3. **Question Answering**:
   ```
   User asks question → Store message in DB → Query Pinecone for relevant context
   → Send context + question to LLaMA → Generate answer → Store assistant response
   → Return answer to frontend
   ```

4. **Chat Management**:
   ```
   Frontend requests chat history → Query Supabase for chats/messages
   → Return formatted chat data → Display in UI
   ```

### Technology Stack Flow

```
React Frontend ──HTTP/REST──► FastAPI Backend
                                    │
                                    ├──► Supabase (PostgreSQL)
                                    │    ├── chats table
                                    │    ├── messages table
                                    │    └── storage bucket
                                    │
                                    ├──► Pinecone Vector DB
                                    │    └── document embeddings
                                    │
                                    └──► Groq/LLaMA API
                                         └── text generation
```

## 📋 Prerequisites

- Python 3.8+
- Node.js 16+
- npm or yarn

## 🔧 Installation

### Backend Setup

1. Navigate to the backend directory:
   ```bash
   cd backend
   ```

2. Create a virtual environment:
   ```bash
   python -m venv venv
   ```

3. Activate the virtual environment:
   - Windows: `venv\Scripts\activate`
   - macOS/Linux: `source venv/bin/activate`

4. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

5. Set up environment variables:
   - Create a `.env` file in the backend directory
   - Add your API keys and configuration

6. Run the backend server:
   ```bash
   python main.py
   ```

### Frontend Setup

1. Navigate to the frontend directory:
   ```bash
   cd frontend
   ```

2. Install dependencies:
   ```bash
   npm install
   ```

3. Start the development server:
   ```bash
   npm run dev
   ```

## 🔑 Environment Variables

Create a `.env` file in the backend directory with the following variables:

```env
PINECONE_API_KEY=your_pinecone_api_key
SUPABASE_URL=your_supabase_url
SUPABASE_KEY=your_supabase_key
LLAMA_API_KEY=your_llama_api_key
```

## 📚 API Endpoints

### PDF Management

#### Upload PDF
- **POST** `/pdf-upload`
- **Description**: Upload a PDF file to Supabase storage
- **Headers**: 
  - `X-User-ID` (optional): User identifier
- **Body**: Multipart form data
  - `file`: PDF file (required)
- **Response**: Upload confirmation with file details

### Question & Answer

#### Ask Question
- **POST** `/ask-question`
- **Description**: Ask a question about a specific PDF file using AI
- **Body**:
```json
{
  "file_id": "unique-file-id",
  "question": "What is the main topic of this document?"
}
```
- **Response**:
```json
{
  "answer": "The main topic of this document is..."
}
```

### Chat Management

#### Create Chat
- **POST** `/chat/create`
- **Description**: Create a new chat session when PDF is uploaded
- **Body**:
```json
{
  "title": "Chat about Document Title",
  "pdf_document_id": "document-id",
  "file_id": "unique-file-id",
  "user_id": "user-123" // optional
}
```
- **Response**:
```json
{
  "id": "chat-id",
  "title": "Chat about Document Title",
  "pdf_document_id": "document-id",
  "file_id": "unique-file-id",
  "user_id": "user-123",
  "created_at": "2025-06-24T10:30:00Z",
  "updated_at": "2025-06-24T10:30:00Z"
}
```

#### Send Message
- **POST** `/chat/message`
- **Description**: Store a message in the database
- **Body**:
```json
{
  "chat_id": "chat-id",
  "content": "Hello, what is this document about?",
  "sender": "user" // "user" or "assistant"
}
```
- **Response**:
```json
{
  "id": "message-id",
  "chat_id": "chat-id",
  "content": "Hello, what is this document about?",
  "sender": "user",
  "created_at": "2025-06-24T10:35:00Z"
}
```

#### Get All Chats
- **GET** `/chat/all`
- **Description**: Get all chats (for when user_id is empty)
- **Response**:
```json
[
  {
    "id": "chat-id",
    "title": "Chat about Document Title",
    "pdf_document_id": "document-id",
    "file_id": "unique-file-id",
    "user_id": "user-123",
    "created_at": "2025-06-24T10:30:00Z",
    "updated_at": "2025-06-24T10:30:00Z"
  }
]
```

#### Get User Chats
- **GET** `/chat/user/{user_id}/chats`
- **Description**: Get all chats for a specific user
- **Parameters**:
  - `user_id` (path): User identifier
- **Response**: Array of chat objects (same format as above)

#### Get Chat with Messages
- **GET** `/chat/{chat_id}`
- **Description**: Fetch a chat with all its messages
- **Parameters**:
  - `chat_id` (path): Chat identifier
- **Response**:
```json
{
  "chat": {
    "id": "chat-id",
    "title": "Chat about Document Title",
    "pdf_document_id": "document-id",
    "file_id": "unique-file-id",
    "user_id": "user-123",
    "created_at": "2025-06-24T10:30:00Z",
    "updated_at": "2025-06-24T10:30:00Z"
  },
  "messages": [
    {
      "id": "message-id",
      "chat_id": "chat-id",
      "content": "Hello, what is this document about?",
      "sender": "user",
      "created_at": "2025-06-24T10:35:00Z"
    }
  ]
}
```

#### Delete Chat
- **DELETE** `/chat/{chat_id}`
- **Description**: Delete a chat and all its messages
- **Parameters**:
  - `chat_id` (path): Chat identifier
- **Response**:
```json
{
  "message": "Chat deleted successfully"
}
```

### General

#### Health Check
- **GET** `/`
- **Description**: Basic health check endpoint
- **Response**:
```json
{
  "Hello": "World"
}
```

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🆘 Support

If you encounter any issues or have questions, please open an issue on the GitHub repository.

---

