# EduQuiz API Documentation

This document describes all available tRPC API endpoints in the EduQuiz application.

## Authentication

All endpoints except `auth.me` and `auth.logout` require authentication. Authentication is handled via Manus OAuth and session cookies.

### Auth Endpoints

#### `auth.me`
Get current authenticated user information.

**Type**: Public Query  
**Input**: None  
**Output**: 
```typescript
{
  id: number,
  openId: string,
  email: string,
  name: string,
  loginMethod: string,
  role: "user" | "admin",
  createdAt: Date,
  updatedAt: Date,
  lastSignedIn: Date
}
```

#### `auth.logout`
Clear user session and logout.

**Type**: Public Mutation  
**Input**: None  
**Output**:
```typescript
{ success: true }
```

---

## Question Management

### `questions.list`
Retrieve all questions for the current user with pagination.

**Type**: Protected Query  
**Input**:
```typescript
{
  limit: number (default: 100),
  offset: number (default: 0)
}
```
**Output**: Array of questions
```typescript
{
  id: number,
  questionText: string,
  options: string[],
  correctOptionIndex: number,
  explanation: string,
  category?: string,
  difficulty: "easy" | "medium" | "hard",
  createdAt: Date
}[]
```

### `questions.search`
Search questions by text query.

**Type**: Protected Query  
**Input**:
```typescript
{
  query: string
}
```
**Output**: Array of matching questions (same structure as `list`)

### `questions.delete`
Delete a question by ID.

**Type**: Protected Mutation  
**Input**:
```typescript
{
  id: number
}
```
**Output**:
```typescript
{
  success: boolean,
  message: string
}
```

---

## Quiz Session Management

### `quiz.createSession`
Create a new quiz session with selected questions.

**Type**: Protected Mutation  
**Input**:
```typescript
{
  title: string,
  questionIds: number[]
}
```
**Output**:
```typescript
{
  success: boolean,
  sessionId: number,
  totalQuestions: number
}
```

### `quiz.getSessions`
Retrieve all quiz sessions for the current user.

**Type**: Protected Query  
**Input**:
```typescript
{
  limit: number (default: 50)
}
```
**Output**: Array of sessions
```typescript
{
  id: number,
  title: string,
  totalQuestions: number,
  correctAnswers: number,
  createdAt: Date,
  completedAt?: Date
}[]
```

### `quiz.recordAnswer`
Record an answer to a quiz question.

**Type**: Protected Mutation  
**Input**:
```typescript
{
  sessionId: number,
  questionId: number,
  selectedOptionIndex: number
}
```
**Output**:
```typescript
{
  success: boolean,
  isCorrect: boolean,
  explanation: string
}
```

### `quiz.completeSession`
Mark a quiz session as complete.

**Type**: Protected Mutation  
**Input**:
```typescript
{
  sessionId: number
}
```
**Output**:
```typescript
{
  success: boolean,
  score: number,
  totalQuestions: number,
  percentage: number
}
```

---

## MCQ Generation

### `mcq.generate`
Generate MCQs from extracted text using AI.

**Type**: Protected Mutation  
**Input**:
```typescript
{
  text: string (min 10 chars, max 10000 chars),
  count: number (1-20, default: 5),
  difficulty?: "easy" | "medium" | "hard"
}
```
**Output**:
```typescript
{
  success: boolean,
  questions: {
    questionText: string,
    options: string[],
    correctOptionIndex: number,
    explanation: string,
    difficulty: string
  }[]
}
```

---

## Image & OCR Operations

### `images.upload`
Upload an image for OCR processing.

**Type**: Protected Mutation  
**Input**: File upload (multipart/form-data)
**Output**:
```typescript
{
  success: boolean,
  imageId: number,
  storageKey: string
}
```

### `images.getOCRStatus`
Get the OCR processing status of an uploaded image.

**Type**: Protected Query  
**Input**:
```typescript
{
  imageId: number
}
```
**Output**:
```typescript
{
  id: number,
  status: "pending" | "processing" | "completed" | "failed",
  extractedText?: string,
  createdAt: Date
}
```

---

## Question Banks

### `banks.create`
Create a new question bank.

**Type**: Protected Mutation  
**Input**:
```typescript
{
  name: string,
  description?: string
}
```
**Output**:
```typescript
{
  success: boolean,
  bankId: number
}
```

### `banks.list`
Get all question banks for the current user.

**Type**: Protected Query  
**Input**: None  
**Output**: Array of banks
```typescript
{
  id: number,
  name: string,
  description?: string,
  questionCount: number,
  createdAt: Date
}[]
```

### `banks.addQuestions`
Add questions to a question bank.

**Type**: Protected Mutation  
**Input**:
```typescript
{
  bankId: number,
  questionIds: number[]
}
```
**Output**:
```typescript
{
  success: boolean,
  addedCount: number
}
```

---

## Error Handling

All endpoints return errors in the following format:

```typescript
{
  code: string,
  message: string,
  data?: any
}
```

Common error codes:
- `UNAUTHORIZED`: User is not authenticated
- `FORBIDDEN`: User lacks permission for this operation
- `NOT_FOUND`: Requested resource not found
- `BAD_REQUEST`: Invalid input parameters
- `INTERNAL_SERVER_ERROR`: Server error

---

## Rate Limiting

- MCQ generation: 5 requests per minute per user
- File uploads: 10 requests per minute per user
- Other endpoints: 100 requests per minute per user

---

## Data Types

### Question
```typescript
interface Question {
  id: number;
  userId: number;
  questionText: string;
  options: string[];
  correctOptionIndex: number;
  explanation: string;
  category?: string;
  difficulty: "easy" | "medium" | "hard";
  sourceType: "camera" | "upload" | "manual";
  createdAt: Date;
}
```

### Quiz Session
```typescript
interface QuizSession {
  id: number;
  userId: number;
  title: string;
  totalQuestions: number;
  correctAnswers: number;
  createdAt: Date;
  completedAt?: Date;
}
```

### Quiz Attempt
```typescript
interface QuizAttempt {
  id: number;
  sessionId: number;
  questionId: number;
  selectedOptionIndex: number;
  isCorrect: boolean;
  createdAt: Date;
}
```

### Question Bank
```typescript
interface QuestionBank {
  id: number;
  userId: number;
  name: string;
  description?: string;
  createdAt: Date;
}
```

---

## Implementation Notes

- All timestamps are returned as ISO 8601 strings
- All IDs are positive integers
- Text fields support UTF-8 encoding
- Arrays are returned as JSON arrays
- Null values are omitted from responses
- All mutations are atomic (all-or-nothing)

---

**Last Updated**: May 4, 2026  
**API Version**: 1.0.0
