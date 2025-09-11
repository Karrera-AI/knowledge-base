# Karrera AI - Client Application

This is the client-side application for Karrera AI, a comprehensive career development platform that combines neuroscience principles with AI-powered insights to help users build their professional journey.

## 🏗️ Architecture Overview

The application is built with **React + TypeScript** and follows a modular, component-based architecture with clear separation of concerns:

- **Components**: Reusable UI components organized by feature
- **Hooks**: Custom hooks for state management and business logic
- **Services**: API integration and business logic layer
- **Interfaces**: TypeScript definitions for type safety
- **Utils**: Utility functions and helpers

## 📁 Project Structure

```
client/
├── src/
│   ├── components/          # UI Components
│   │   ├── memory/         # Memory system components
│   │   ├── paths/          # Career paths components
│   │   ├── chat/           # Chat system components
│   │   ├── profile/        # User profile components
│   │   └── ui/             # Reusable UI components
│   ├── hooks/              # Custom React hooks
│   ├── lib/                # Core libraries and utilities
│   │   ├── Interfaces/     # TypeScript interfaces
│   │   ├── services/       # API services
│   │   └── Utils/          # Utility functions
│   ├── pages/              # Page components
│   └── data/               # Static data files
```

## 🧠 Core Features

### 1. Memory System
A neuroscience-based memory classification system implementing Kahneman's framework:

- **Memory Types**: Semantic, Episodic, Procedural, Emotional
- **Memory States**: Working, Long-term, Discarded
- **AI Classification**: Automatic memory type detection
- **Narrative Building**: Remembering Self construction
- **Experience Tracking**: Real-time Experiencing Self capture

**Key Components:**
- `MemoryClassificationEngine` - AI-powered classification
- `NarrativeBuilder` - Story construction from memories
- `ExperiencingSelfTracker` - Real-time experience logging
- `LegacyFilesVisualization` - Memory file management

### 2. Career Paths
Comprehensive career path exploration and management:

- **Path Discovery**: Browse available career paths
- **WorkDNA Integration**: Personality-based path matching
- **Progress Tracking**: Monitor learning progress
- **Community Features**: Connect with other learners

**Key Components:**
- `PathCard` - Individual path display
- `PathDetail` - Detailed path information
- `WorkDNARadar` - Personality visualization
- `PathsFilters` - Search and filtering

### 3. Chat System
AI-powered conversational interface:

- **Template-based Conversations**: Pre-defined conversation starters
- **Real-time Messaging**: Instant AI responses
- **Error Handling**: Robust error management with retry
- **Conversation History**: Persistent chat sessions

**Key Components:**
- `ChatInterface` - Main chat interface
- `ChatSidebar` - Conversation list
- `ChatMessages` - Message display
- `ChatInput` - Message input with suggestions

### 4. User Profile
Comprehensive user profile management:

- **WorkDNA Analysis**: Personality and skill assessment
- **Career Suggestions**: AI-powered career recommendations
- **Persona Management**: Multiple professional personas
- **Progress Visualization**: Career development tracking

**Key Components:**
- `ProfileHeader` - Profile overview
- `WorkDNAVisualization` - Personality visualization
- `CareerPathSuggestions` - AI recommendations
- `PersonaManagement` - Persona creation and editing

## 🔧 Technical Features

### State Management
- **Custom Hooks**: Centralized state management
- **React Query**: Server state management and caching
- **Local Storage**: Persistent data caching
- **Optimistic Updates**: Improved user experience

### Performance Optimizations
- **Component Memoization**: Reduced unnecessary re-renders
- **Lazy Loading**: Code splitting for better performance
- **Intelligent Caching**: 5-minute cache for API responses
- **Error Boundaries**: Graceful error handling

### Type Safety
- **TypeScript**: Full type coverage
- **Interface Definitions**: Comprehensive type definitions
- **Generic Components**: Reusable typed components
- **API Type Safety**: End-to-end type safety

## 🚀 Getting Started

### Prerequisites
- Node.js 18+
- npm or yarn

### Installation
```bash
npm install
```

### Development
```bash
npm run dev
```

### Build
```bash
npm run build
```

## 📚 Component Usage Examples

### Memory System
```tsx
import { MemorySection } from '@/components/memory';

function Dashboard() {
  return <MemorySection />;
}
```

### Career Paths
```tsx
import { usePaths } from '@/hooks/use-paths';
import { PathsList, PathsFilters } from '@/components/paths';

function PathsPage() {
  const { paths, filteredPaths, filters, updateFilter } = usePaths();
  
  return (
    <div>
      <PathsFilters filters={filters} onFilterChange={updateFilter} />
      <PathsList paths={filteredPaths} />
    </div>
  );
}
```

### Chat System
```tsx
import { useChat } from '@/hooks/use-chat';
import { ChatInterface, ChatSidebar } from '@/components/chat';

function ChatPage() {
  const chat = useChat();
  
  return (
    <div className="flex">
      <ChatSidebar {...chat.sidebarProps} />
      <ChatInterface {...chat.interfaceProps} />
    </div>
  );
}
```

### User Profile
```tsx
import { useProfile } from '@/hooks/use-profile';
import { ProfileHeader, WorkDNAVisualization } from '@/components/profile';

function ProfilePage() {
  const { user, workDNA, isLoading } = useProfile();
  
  if (isLoading) return <LoadingState />;
  
  return (
    <div>
      <ProfileHeader user={user} />
      <WorkDNAVisualization workDNA={workDNA} />
    </div>
  );
}
```

## 🎯 Key Benefits

### For Developers
- **Modular Architecture**: Easy to maintain and extend
- **Type Safety**: Reduced runtime errors
- **Reusable Components**: Faster development
- **Clear Separation**: Business logic separated from UI
- **Performance**: Optimized rendering and caching

### For Users
- **Intuitive Interface**: Clean and modern design
- **Fast Performance**: Optimized loading and interactions
- **Personalized Experience**: AI-powered recommendations
- **Comprehensive Features**: Complete career development toolkit
- **Reliable**: Robust error handling and data persistence

## 🔄 Development Patterns

### Component Organization
- **Single Responsibility**: Each component has one clear purpose
- **Composition over Inheritance**: Flexible component composition
- **Props Interface**: Clear component contracts
- **Default Props**: Sensible defaults for optional props

### State Management
- **Custom Hooks**: Encapsulated state logic
- **Service Layer**: API operations separated from components
- **Optimistic Updates**: Immediate UI feedback
- **Error Boundaries**: Graceful error handling

### Code Quality
- **TypeScript**: Full type coverage
- **ESLint**: Code quality enforcement
- **Prettier**: Consistent code formatting
- **Component Documentation**: Clear usage examples

## 📖 Documentation

Each major feature has its own detailed documentation:

- [Memory System](./src/components/memory/README-memory.md)
- [Career Paths](./src/components/paths/README-path.md)
- [Chat System](./src/components/chat/README.md)
- [User Profile](./src/components/profile/README.md)
- [Cache System](./src/hooks/README-cache.md)

## 🤝 Contributing

1. Follow the established component patterns
2. Maintain TypeScript type safety
3. Add documentation for new features
4. Write tests for new components
5. Follow the existing code style

## 📄 License

This project is part of the Karrera AI platform.
