# Gemini Frontend Clone

A fully functional, responsive, and visually appealing conversational AI chat application built with React, TypeScript, and modern web technologies.


## 📋 Features

### ✅ Core Features Implemented

#### 1. **Authentication**
- OTP-based login/signup with country code selection
- Real-time country data fetching from RestCountries API
- Form validation using React Hook Form + Zod
- Simulated OTP sending and validation (Demo OTP: `123456`)
- Persistent authentication state

#### 2. **Dashboard**
- Complete chatroom management (Create/Delete)
- Real-time chatroom listing with timestamps
- Debounced search functionality (300ms delay)
- Toast notifications for all actions
- Mobile-responsive sidebar with smooth animations

#### 3. **Chat Interface**
- Real-time messaging with user and AI responses
- Message timestamps with smart formatting
- "Gemini is typing..." indicator
- Throttled AI responses (2-4 second delay simulation)
- Auto-scroll to latest message
- Reverse infinite scroll for older messages
- Client-side pagination (20 messages per page)
- Image upload support with preview
- Copy-to-clipboard on message hover
- Loading skeletons for better UX

#### 4. **Global UX Features**
- Fully responsive design (mobile, tablet, desktop)
- Dark mode toggle with persistent preference
- Keyboard accessibility throughout
- LocalStorage for data persistence
- Smooth transitions and animations
- Professional toast notifications

## 🛠️ Tech Stack

| Feature | Technology |
|---------|-----------|
| Framework | React 18 + TypeScript |
| Build Tool | Vite |
| State Management | Zustand |
| Form Validation | React Hook Form + Zod |
| Styling | Tailwind CSS |
| Icons | Lucide React |
| Notifications | Sonner |
| Deployment | Vercel/Netlify |

## 📁 Project Structure

```
src/
├── components/
│   ├── ui/              # Reusable UI components
│   │   ├── Button.tsx
│   │   ├── Input.tsx
│   │   ├── Toast.tsx
│   │   └── Skeleton.tsx
│   ├── auth/            # Authentication components
│   │   └── LoginForm.tsx
│   ├── dashboard/       # Dashboard components
│   │   └── Sidebar.tsx
│   └── chat/            # Chat components
│       ├── ChatArea.tsx
│       └── ChatMessage.tsx
├── store/               # Zustand state management
│   ├── authStore.ts
│   ├── chatStore.ts
│   └── themeStore.ts
├── types/               # TypeScript type definitions
│   └── index.ts
├── lib/                 # Utility functions
│   └── utils.ts
├── App.tsx              # Main application component
├── main.tsx             # Application entry point
└── index.css            # Global styles

```

## 🚀 Getting Started

### Prerequisites

- Node.js (v18 or higher)
- npm or yarn

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/yourusername/gemini-clone.git
   cd gemini-clone
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Start development server**
   ```bash
   npm run dev
   ```

4. **Open in browser**
   ```
   Navigate to http://localhost:5173
   ```

### Building for Production

```bash
npm run build
npm run preview  # Preview production build locally
```

## 🔧 Key Implementation Details

### 1. **Throttling AI Responses**

The application simulates realistic AI response delays:

```typescript
const simulateAIResponse = (userMessage: string) => {
  setTyping(true);
  const delay = Math.random() * 2000 + 2000; // 2-4 seconds
  
  setTimeout(() => {
    addMessage(currentChatroom, {
      content: generateResponse(userMessage),
      sender: 'ai',
    });
    setTyping(false);
  }, delay);
};
```

### 2. **Infinite Scroll Implementation**

Reverse infinite scroll loads older messages when scrolling to top:

```typescript
const handleScroll = throttle(() => {
  const container = messagesContainerRef.current;
  if (container.scrollTop === 0) {
    loadMoreMessages(currentChatroom);
    // Maintain scroll position after loading
    container.scrollTop = container.scrollHeight - prevScrollHeight;
  }
}, 300);
```

### 3. **Client-Side Pagination**

Messages are paginated to improve performance:

```typescript
const messagesPerPage = 20;
const displayedMessages = messages.slice(-page * messagesPerPage);
```

### 4. **Form Validation with Zod**

Type-safe form validation:

```typescript
const phoneSchema = z.object({
  countryCode: z.string().min(1, 'Please select a country'),
  phone: z.string().min(10, 'Phone number must be at least 10 digits'),
});
```

### 5. **Debounced Search**

Search functionality with 300ms debounce:

```typescript
const debounce = (func: Function, delay: number) => {
  let timeoutId: NodeJS.Timeout;
  return (...args: any[]) => {
    clearTimeout(timeoutId);
    timeoutId = setTimeout(() => func(...args), delay);
  };
};
```

### 6. **LocalStorage Persistence**

All data persists across sessions:

```typescript
// Automatic save on state change
const saveToStorage = (state) => {
  localStorage.setItem('chat-storage', JSON.stringify(state));
};

// Load on initialization
const loadFromStorage = () => {
  const stored = localStorage.getItem('chat-storage');
  return stored ? JSON.parse(stored) : defaultState;
};
```

## 🎨 Design Decisions

1. **Component Architecture**: Modular, reusable components following separation of concerns
2. **State Management**: Zustand for lightweight, performant global state
3. **Styling**: Tailwind CSS for rapid development and consistent design
4. **Accessibility**: ARIA labels, keyboard navigation, focus management
5. **Performance**: Lazy loading, throttling, debouncing, and pagination
6. **UX**: Loading states, optimistic updates, smooth animations

## 📱 Responsive Design

- **Mobile** (< 768px): Full-screen with hamburger menu
- **Tablet** (768px - 1024px): Sidebar + chat area
- **Desktop** (> 1024px): Full layout with expanded sidebar

## ⌨️ Keyboard Shortcuts

- `Enter` - Send message / Submit forms
- `Esc` - Close modals
- `Tab` - Navigate between inputs

## 🧪 Testing Instructions

### Login Flow
1. Select a country from dropdown
2. Enter any 10-digit phone number
3. Use OTP: `123456` to login

### Chat Features
1. Create a new chatroom
2. Send text messages
3. Upload images (< 5MB)
4. Scroll to top to load older messages
5. Hover over messages to copy
6. Toggle dark mode


## 🐛 Known Issues & Future Enhancements

### Current Limitations
- Simulated backend (no real API)
- Demo OTP for all users
- Image storage in base64 (memory intensive)

### Future Improvements
- Real backend integration
- WebSocket for real-time messaging
- Voice message support
- File attachments
- Message reactions
- User profile management

## 👨‍💻 Development

### Code Quality
- TypeScript for type safety
- ESLint for code linting
- Consistent naming conventions
- Comprehensive comments

### Performance Optimizations
- React.memo for expensive components
- useCallback for event handlers
- Debouncing and throttling
- Virtual scrolling for large message lists

## 📄 License

This project is created for educational purposes as part of a technical assessment.

## 🙏 Acknowledgments

- Design inspiration from Google Gemini
- Icons by Lucide React
- Country data from RestCountries API
