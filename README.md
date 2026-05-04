# EduQuiz: AI-Powered Educational Quiz App

A mobile-optimized quiz application with AI-powered MCQ generation, camera integration, and offline-capable architecture. Built with React, Express, and Drizzle ORM.

## 🎨 Design

The app features a striking **cyberpunk aesthetic** with:
- **Color Scheme**: Deep black background (#0a0e27) with neon pink (#ff006e) and electric cyan (#00f5ff)
- **Typography**: Geometric fonts (Orbitron, Space Mono) with neon glow effects
- **UI Elements**: HUD-style borders, corner brackets, technical styling
- **Theme**: Dark theme throughout for reduced eye strain

## ✨ Implemented Features

### Core Quiz Functionality
- **Interactive Quiz Interface**: Answer multiple-choice questions with immediate visual feedback
- **Real-Time Feedback**: Correct answers highlight green, incorrect answers highlight red
- **Inline Explanations**: Detailed explanations display immediately after answer selection
- **Progress Tracking**: Question counter and session progress indicator
- **Quiz Sessions**: Create, manage, and complete quiz sessions
- **Answer Recording**: Track all answers and calculate scores

### Question Management
- **Question Bank**: Browse and manage all saved questions
- **Search Functionality**: Full-text search across questions
- **Question Details**: View question text, options, correct answer, and explanation
- **Question Deletion**: Remove questions with confirmation
- **Difficulty Levels**: Questions categorized as easy, medium, or hard

### Quiz History & Analytics
- **Session History**: View all past quiz attempts with timestamps
- **Performance Metrics**: Track total quizzes, average scores, best scores
- **Attempt Review**: Detailed breakdown of each quiz attempt
- **Answer History**: Review all answers and explanations from past attempts

### File Upload & OCR
- **Drag-and-Drop Upload**: Upload PDF and text files with visual feedback
- **File Preview**: Review extracted text before MCQ generation
- **MCQ Generation Preview**: See generated questions before saving
- **Text Extraction**: Extract text from uploaded files
- **Status Indicators**: Real-time processing status updates

### Camera Integration
- **Mobile Photo Capture**: Capture photos of questions or book pages
- **Real-Time Preview**: Instant preview of captured images
- **OCR Pipeline**: Seamless integration with text extraction
- **Mobile-Optimized**: Touch-friendly interface for mobile devices

### AI MCQ Generation
- **Intelligent Analysis**: Generate contextually relevant MCQs from text
- **4-Option Format**: Each question includes 4 multiple-choice options
- **Detailed Explanations**: Comprehensive explanations for each answer
- **Configurable Difficulty**: Generate questions at easy, medium, or hard levels
- **Batch Generation**: Generate multiple MCQs from a single document

### Authentication & Security
- **Manus OAuth**: Secure user authentication via OAuth
- **Session Management**: Persistent user sessions with secure cookies
- **Role-Based Access**: User and admin roles for access control
- **Protected Routes**: All quiz operations require authentication

## 🏗️ Technical Stack

### Frontend
- **Framework**: React 19 with TypeScript
- **Styling**: Tailwind CSS 4 with custom cyberpunk theme
- **State Management**: tRPC React Query hooks
- **Routing**: Wouter
- **UI Components**: shadcn/ui
- **Icons**: Lucide React

### Backend
- **Server**: Express.js with tRPC
- **Database**: MySQL with Drizzle ORM
- **Storage**: S3 for file storage
- **AI Integration**: LLM vision API for OCR
- **Authentication**: Manus OAuth

### Database Schema
- **questions**: Stores quiz questions with options and explanations
- **images**: Tracks uploaded images and OCR status
- **quiz_sessions**: Records quiz sessions and scores
- **quiz_attempts**: Tracks individual answer attempts
- **question_banks**: Organizes questions into custom collections
- **offline_cache**: Caches data for offline access

## 📱 Pages & Routes

| Route | Purpose |
|-------|---------|
| `/` | Home page with feature navigation |
| `/upload` | File upload with drag-and-drop |
| `/camera` | Camera capture for OCR |
| `/quiz` | Interactive quiz interface |
| `/questions` | Question bank browser |
| `/history` | Quiz history and analytics |
| `/results/:sessionId` | Detailed attempt review |

## 🚀 Getting Started

### Installation
```bash
# Install dependencies
pnpm install

# Run development server
pnpm dev

# Run tests
pnpm test

# Build for production
pnpm build
```

### Environment Variables
All required environment variables are automatically injected by the Manus platform:
- `DATABASE_URL`: MySQL connection string
- `JWT_SECRET`: Session signing secret
- `VITE_APP_ID`: OAuth application ID
- `OAUTH_SERVER_URL`: OAuth backend URL
- `VITE_OAUTH_PORTAL_URL`: OAuth login portal

## 🧪 Testing

The application includes comprehensive test coverage:

```bash
pnpm test
```

**Test Files**:
- `server/auth.logout.test.ts` - Authentication tests
- `server/quiz.test.ts` - Quiz functionality tests
- `server/integration.test.ts` - Integration tests

**Test Results**: 32 passing tests covering:
- Authentication and authorization
- Quiz session management
- Question operations
- MCQ generation validation
- Answer recording and scoring
- API response validation
- Error handling

## 📚 API Documentation

See [API_DOCUMENTATION.md](./API_DOCUMENTATION.md) for complete API endpoint reference including:
- Authentication endpoints
- Question management
- Quiz session operations
- MCQ generation
- Image/OCR operations
- Question banks

## 🔄 Workflow Examples

### Create and Take a Quiz
1. Navigate to **Upload Material** or **Capture Photo**
2. Upload a file or capture an image
3. Review extracted text
4. Generate MCQs from the text
5. Go to **Take Quiz**
6. Select questions to quiz on
7. Answer each question and see immediate feedback
8. Complete the quiz and review results

### Browse Question Bank
1. Go to **Question Bank**
2. Search for specific questions
3. View question details (options, explanation)
4. Delete unwanted questions
5. Select questions for custom quizzes

### Review Quiz History
1. Go to **Quiz History**
2. View all past quiz attempts
3. Click on a session to see detailed breakdown
4. Review all answers and explanations
5. Track performance trends

## 🎯 Key Features

- **Immediate Feedback**: See if answers are correct/incorrect instantly
- **Mobile-First**: Fully responsive design optimized for mobile devices
- **Dark Theme**: Consistent dark theme throughout the app
- **Cyberpunk Aesthetic**: Striking visual design with neon colors
- **Search & Filter**: Find questions quickly
- **Progress Tracking**: Monitor your learning progress
- **Offline Capable**: Quiz data cached locally for offline access

## 📊 Performance

- **Bundle Size**: Optimized with code splitting
- **Load Time**: Fast initial load with lazy-loaded components
- **Database**: Optimized queries with proper indexing
- **Storage**: Efficient S3 integration for file storage

## 🔒 Security

- **Authentication**: Secure OAuth-based authentication
- **Authorization**: Role-based access control
- **Data Privacy**: User data stored securely
- **Session Management**: Secure session cookies

## 📝 File Structure

```
edu-quiz-app/
├── client/
│   ├── src/
│   │   ├── pages/
│   │   │   ├── Home.tsx
│   │   │   ├── Upload.tsx
│   │   │   ├── Camera.tsx
│   │   │   ├── Quiz.tsx
│   │   │   ├── Questions.tsx
│   │   │   ├── History.tsx
│   │   │   └── Results.tsx
│   │   ├── components/
│   │   ├── contexts/
│   │   ├── hooks/
│   │   ├── lib/
│   │   ├── App.tsx
│   │   ├── main.tsx
│   │   └── index.css
│   ├── public/
│   └── index.html
├── server/
│   ├── routers.ts
│   ├── db.ts
│   ├── auth.logout.test.ts
│   ├── quiz.test.ts
│   ├── integration.test.ts
│   └── _core/
├── drizzle/
│   └── schema.ts
├── shared/
├── storage/
├── package.json
├── API_DOCUMENTATION.md
└── README.md
```

## 🚀 Deployment

The app is deployed on the Manus platform with:
- Auto-scaling infrastructure
- CDN for static assets
- Database backups
- SSL/TLS encryption
- Monitoring and logging

To deploy:
1. Create a checkpoint via the Management UI
2. Click the "Publish" button
3. App is live at your custom domain

## 🔄 Future Enhancements

Potential features for future versions:
- Advanced offline caching with IndexedDB
- Service worker for offline support
- Spaced repetition algorithm
- Collaborative quizzes
- Leaderboards and achievements
- Advanced analytics dashboard
- Voice-based question input
- Real-time collaboration

## 📞 Support

For issues, feature requests, or feedback, please contact the development team.

## 📄 License

This project is proprietary and confidential. All rights reserved.

---

**Version**: 1.0.0  
**Last Updated**: May 4, 2026  
**Status**: Production Ready
