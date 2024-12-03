# AI-Powered Chat Application

A modern chat application built with AI capabilities, leveraging OpenAI's API for intelligent interactions. The application is fully hosted on Vercel's platform with a serverless architecture and uses Supabase for data persistence.

## System Architecture

![alt text](overall_architecture.png)

### Overview

- **Frontend**: Single page application hosted on Vercel
- **Backend**: Serverless functions running on Vercel's infrastructure
- **Database**: PostgreSQL database hosted on Supabase
- **Authentication**: NextAuth for secure JWT-based authentication
- **AI Integration**: OpenAI API integration via AI SDK

### Key Components

- Frontend and backend are both hosted on Vercel's platform
- REST API communication between frontend and backend
- Secured endpoints using JWT tokens
- Real-time data storage in Supabase
- AI-powered chat interactions through OpenAI's API

## Frontend

The frontend is a modern web application with the following features:

- Clean and intuitive user interface
- Real-time chat capabilities
- Document viewing and management
- Voting system for messages
- Suggestion system for content improvement

### API Endpoints

- `/chat`: Handle chat interactions
- `/history`: Manage chat history
- `/suggestions`: Process and manage suggestions
- `/vote`: Handle voting on messages

## Backend

The backend is built using Vercel Serverless Functions with these key features:

- Stateless architecture for scalability
- Secure API endpoints
- Integration with OpenAI's API
- Database operations with Supabase

### Key Features

- Message processing and storage
- User authentication and authorization
- Document management
- Suggestion processing
- Voting system implementation

## Data Model

The application uses a relational database with the following core entities:

![alt text](database_schema.png)

### User

- `id` (uuid): Primary key
- `email` (varchar): User's email address
- `password` (varchar): Hashed password

### Chat

- `id` (uuid): Primary key
- `createdAt` (timestamp): Chat creation time
- `userId` (uuid): Reference to User
- `title` (text): Chat title

### Message

- `id` (uuid): Primary key
- `chatId` (uuid): Reference to Chat
- `role` (varchar): Message role (user/assistant)
- `content` (json): Message content
- `createdAt` (timestamp): Message timestamp

### Document

- `id` (uuid): Primary key
- `title` (text): Document title
- `content` (text): Document content
- `userId` (uuid): Reference to User
- `createdAt` (timestamp): Document creation time

### Suggestion

- `id` (uuid): Primary key
- `documentId` (uuid): Reference to Document
- `originalText` (text): Original document text
- `suggestedText` (text): Suggested improvement
- `description` (text): Suggestion description
- `isResolved` (bool): Resolution status
- `userId` (uuid): Reference to User
- `createdAt` (timestamp): Suggestion creation time
- `documentCreatedAt` (timestamp): Referenced document creation time

### Vote

- `chatId` (uuid): Reference to Chat
- `messageId` (uuid): Reference to Message
- `isUpvoted` (bool): Vote status

### Relationships

- Users can create multiple Chats and Documents
- Each Chat contains multiple Messages
- Documents can have multiple Suggestions
- Messages can receive multiple Votes
- All entities maintain proper foreign key relationships for data integrity

## Environment Variables

| Variable         | Description                                                                                              | Required | Example                           |
| ---------------- | -------------------------------------------------------------------------------------------------------- | -------- | --------------------------------- |
| `OPENAI_API_KEY` | API key for OpenAI services. Get it from [OpenAI Platform](https://platform.openai.com/account/api-keys) | Yes      | sk-abcd1234...                    |
| `AUTH_SECRET`    | Secret key for authentication. Generate using `npx auth secret`                                          | Yes      | xkjjk329...                       |
| `POSTGRES_URL`   | Connection string for Supabase                                                                           | Yes      | postgres://user:pass@host:5432/db |

## Prerequisites

1. Install Vercel CLI:

```bash
npm i -g vercel
```

2. Link local instance with Vercel and GitHub accounts (creates `.vercel` directory):

```bash
vercel link
```

3. Download your environment variables:

```bash
vercel env pull
```

## Local Development

1. Install dependencies and start development server:

```bash
pnpm install
pnpm dev
```

## Deployment

Deploy your application to production:

```bash
vercel --prod
```

## Future Improvements

### Authentication Enhancements

1. Add email verification for new sign ups (currently email-only registration without verification)
2. Implement password reset capability
3. Enable third-party authentication providers

### Chat Functionality

1. Expand beyond text-only messages to support rich media inputs (images, audio files, video content)
