# MentorHub Vision - Peer-to-Peer Learning Platform Architecture

## Overview
Transform MentorHub into a gamified peer-to-peer learning platform where users can both seek and provide help, with AI-powered skill assessment and social features.

## Core User Flow Architecture

### 1. Authentication & Onboarding
- **Single Login System**: ✅ Already implemented
- **Welcome Flow**: Post-login assessment prompt
- **Skill Assessment**: Optional AI-generated tests for specialization

### 2. Enhanced Homepage Layout

#### Current State
- Traditional course browsing with search
- Add course functionality
- Basic navbar with profile

#### Proposed New Layout
```
┌─────────────────────────────────────────────────────┐
│ MentorHub    [Home] [Sessions]     🔥3 [👤Profile] │
├─────────────────────────────────────────────────────┤
│                                                     │
│        "Learn together, grow together"              │
│                                                     │
│    ┌─────────────────┐  ┌─────────────────┐        │
│    │   🤝 GET HELP   │  │ 🧠 PROVIDE HELP │        │
│    │                 │  │                 │        │
│    │ • Search topics │  │ • Answer Qs in  │        │
│    │ • Browse tutors │  │   your skills   │        │
│    │ • Book sessions │  │ • Build streak  │        │
│    └─────────────────┘  └─────────────────┘        │
│                                                     │
└─────────────────────────────────────────────────────┘
```

### 3. Component Structure Plan

#### New Components Needed
1. **SkillAssessmentModal** - AI-generated skill tests
2. **HelpRequestCard** - Display questions needing help
3. **QuestionFeed** - Stream of questions for helpers
4. **StreakIndicator** - Snapchat-style streak counter
5. **HelpMatchingSystem** - Connect help seekers with providers
6. **LiveTutorSession** - Enhanced virtual classroom with time management
7. **SubscriptionManager** - Premium features (video recap, AI PDFs)

#### Enhanced Existing Components
1. **HomePage** → **SmartHomepage** with dual action cards
2. **Navbar** → Add streak counter and simplified navigation
3. **VirtualClassroom** → Add time management and extension features
4. **Dashboard** → Include help history and streak tracking

### 4. Data Models

#### User Profile Enhancement
```typescript
interface UserProfile {
  id: string;
  email: string;
  name: string;
  avatar?: string;
  
  // New fields for peer-to-peer learning
  skills: Skill[];
  verifiedSkills: string[];
  streakCount: number;
  lastActiveDate: string;
  helperRating: number;
  totalHelpSessions: number;
  subscriptionType: 'free' | 'premium';
}

interface Skill {
  subject: string;
  level: 'beginner' | 'intermediate' | 'advanced';
  verified: boolean;
  testScore?: number;
}
```

#### Help Request System
```typescript
interface HelpRequest {
  id: string;
  seekerId: string;
  topic: string;
  subject: string;
  description: string;
  urgency: 'low' | 'medium' | 'high';
  estimatedDuration: number; // minutes
  status: 'open' | 'matched' | 'in_session' | 'completed';
  matchedHelperId?: string;
  sessionId?: string;
  createdAt: Date;
}

interface HelpSession {
  id: string;
  helpRequestId: string;
  seekerId: string;
  helperId: string;
  scheduledDuration: number;
  actualDuration: number;
  extensionTime: number; // The extra 3 minutes
  status: 'scheduled' | 'active' | 'completed' | 'cancelled';
  startTime: Date;
  endTime?: Date;
}
```

### 5. Key Features Implementation Plan

#### Phase 1: Core Structure
1. **New Homepage Layout**
   - Two main action cards: "Get Help" and "Provide Help"
   - Profile corner with streak indicator
   - Clean, modern design matching your vision

2. **Skill Assessment System**
   - Optional post-login assessment prompt
   - AI-generated questions based on subject areas
   - Skill verification and badging system

3. **Help Request Flow**
   - Topic/subject search interface
   - Tutor browsing with skills and availability
   - Request submission system

#### Phase 2: Matching & Sessions
1. **Question Feed for Helpers**
   - Display help requests matching helper's skills
   - "Request to Help" button functionality
   - Acceptance/rejection system

2. **Enhanced Virtual Classroom**
   - Time management with session timer
   - Automatic 3-minute extension for helpers
   - Better session controls and UI

#### Phase 3: Gamification & Social
1. **Streak System**
   - Daily activity tracking
   - Snapchat-style streak counter
   - Achievement badges and rewards

2. **Social Features**
   - Helper profiles with ratings and streaks
   - Community leaderboards
   - Achievement sharing

#### Phase 4: Premium Features
1. **AI-Powered Session Recap**
   - Automatic video highlights
   - AI-generated PDF summaries
   - Session analytics and insights

2. **Subscription Management**
   - Free vs Premium feature gating
   - Payment integration
   - Feature upgrade prompts

### 6. Technical Considerations

#### State Management
- Use React Context or Zustand for global state
- User profile, skills, and streak data
- Real-time session management
- Help request matching state

#### Real-time Features
- WebSocket connections for live matching
- Real-time chat and session updates
- Live streak updates and notifications

#### AI Integration
- Skill assessment question generation
- Session recap and PDF creation
- Intelligent tutor matching
- Content moderation and safety

### 7. Migration Strategy

#### From Current to New System
1. **Preserve Existing Data**: Current courses and sessions
2. **Gradual Feature Rollout**: Add new features alongside existing ones
3. **User Migration**: Gentle transition with onboarding for new features
4. **A/B Testing**: Test new homepage layout against current version

### 8. Development Priority Order

1. ✅ **Foundation**: Enhanced authentication and user profiles
2. 🔄 **Core UI**: New homepage layout with action cards
3. 📝 **Help System**: Request creation and question feed
4. 🤝 **Matching**: Helper-seeker connection system
5. ⏱️ **Sessions**: Enhanced virtual classroom with timing
6. 🔥 **Gamification**: Streak system and social features
7. 💎 **Premium**: Subscription and AI-powered features

## Next Steps

This architecture provides a clear roadmap for transforming your existing MentorHub into the peer-to-peer learning platform you envision. The modular approach allows for incremental development while maintaining your current functionality.

Would you like me to start implementing any specific component or feature from this plan?