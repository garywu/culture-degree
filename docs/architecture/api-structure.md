# Culture Degree API Structure

## Overview

The API is built using tRPC for end-to-end type safety between the Next.js frontend and Node.js backend. All endpoints follow a resource-based structure with consistent patterns.

## Authentication

All authenticated endpoints require a valid session token provided by NextAuth.js.

## API Router Structure

```typescript
// Root Router
appRouter
├── auth
├── user
├── program
├── course
├── module
├── content
├── enrollment
├── progress
├── assessment
├── discussion
├── achievement
└── admin
```

## Endpoint Documentation

### Authentication (`auth`)

```typescript
auth.session
  - GET: Get current user session
  - Returns: User object or null

auth.signOut
  - POST: Sign out current user
  - Returns: Success status
```

### User Management (`user`)

```typescript
user.profile
  - GET: Get user profile
  - Auth: Required
  - Returns: User profile with preferences

user.updateProfile
  - PUT: Update user profile
  - Auth: Required
  - Input: { name?, avatar_url?, preferred_language?, timezone? }
  - Returns: Updated user profile

user.dashboard
  - GET: Get user dashboard data
  - Auth: Required
  - Returns: {
      active_enrollments: Enrollment[],
      recent_activity: Activity[],
      achievements: Achievement[],
      streak: number
    }
```

### Programs (`program`)

```typescript
program.list
  - GET: List all published programs
  - Auth: Optional
  - Input: { 
      page?: number,
      limit?: number,
      difficulty?: string,
      search?: string
    }
  - Returns: Paginated program list

program.getBySlug
  - GET: Get program details
  - Auth: Optional
  - Input: { slug: string }
  - Returns: Program with courses

program.enroll
  - POST: Enroll in a program
  - Auth: Required
  - Input: { program_id: string }
  - Returns: Enrollment object
```

### Courses (`course`)

```typescript
course.getBySlug
  - GET: Get course details
  - Auth: Optional (Required for progress)
  - Input: { program_slug: string, course_slug: string }
  - Returns: Course with modules and user progress

course.getModules
  - GET: Get course modules
  - Auth: Required
  - Input: { course_id: string }
  - Returns: Module[] with completion status

course.start
  - POST: Start a course
  - Auth: Required
  - Input: { course_id: string }
  - Returns: Progress object
```

### Modules (`module`)

```typescript
module.get
  - GET: Get module details with content
  - Auth: Required
  - Input: { module_id: string }
  - Returns: Module with content items

module.complete
  - POST: Mark module as complete
  - Auth: Required
  - Input: { module_id: string }
  - Returns: Updated progress
```

### Content (`content`)

```typescript
content.get
  - GET: Get content item
  - Auth: Required
  - Input: { content_id: string }
  - Returns: Content with type-specific data

content.trackProgress
  - POST: Track content progress
  - Auth: Required
  - Input: { 
      content_id: string,
      time_spent: number,
      progress_data?: object
    }
  - Returns: Progress update

content.complete
  - POST: Mark content as complete
  - Auth: Required
  - Input: { content_id: string }
  - Returns: Progress update with achievements
```

### Enrollments (`enrollment`)

```typescript
enrollment.list
  - GET: List user enrollments
  - Auth: Required
  - Input: { status?: string }
  - Returns: Enrollment[] with program details

enrollment.update
  - PUT: Update enrollment status
  - Auth: Required
  - Input: { 
      enrollment_id: string,
      status?: string,
      target_completion_date?: Date
    }
  - Returns: Updated enrollment

enrollment.getProgress
  - GET: Get detailed enrollment progress
  - Auth: Required
  - Input: { enrollment_id: string }
  - Returns: Detailed progress breakdown
```

### Progress Tracking (`progress`)

```typescript
progress.getByContent
  - GET: Get progress for specific content
  - Auth: Required
  - Input: { content_id: string }
  - Returns: Progress object or null

progress.getCourseProgress
  - GET: Get overall course progress
  - Auth: Required
  - Input: { course_id: string }
  - Returns: {
      completed_modules: number,
      total_modules: number,
      time_spent: number,
      last_activity: Date
    }

progress.getProgramProgress
  - GET: Get overall program progress
  - Auth: Required
  - Input: { program_id: string }
  - Returns: {
      completed_courses: number,
      total_courses: number,
      current_course: Course,
      estimated_completion: Date
    }
```

### Assessments (`assessment`)

```typescript
assessment.get
  - GET: Get assessment details
  - Auth: Required
  - Input: { assessment_id: string }
  - Returns: Assessment without answers

assessment.start
  - POST: Start assessment attempt
  - Auth: Required
  - Input: { assessment_id: string }
  - Returns: Attempt object with questions

assessment.submit
  - POST: Submit assessment
  - Auth: Required
  - Input: { 
      attempt_id: string,
      answers: object
    }
  - Returns: {
      score: number,
      passed: boolean,
      feedback: object
    }

assessment.getAttempts
  - GET: Get user's assessment attempts
  - Auth: Required
  - Input: { assessment_id: string }
  - Returns: Attempt[] history
```

### Discussions (`discussion`)

```typescript
discussion.list
  - GET: List discussions
  - Auth: Optional
  - Input: { 
      module_id?: string,
      course_id?: string,
      page?: number,
      limit?: number
    }
  - Returns: Paginated discussions

discussion.create
  - POST: Create discussion
  - Auth: Required
  - Input: { 
      title: string,
      content: object,
      module_id?: string,
      course_id?: string
    }
  - Returns: Created discussion

discussion.addComment
  - POST: Add comment to discussion
  - Auth: Required
  - Input: { 
      discussion_id: string,
      content: object,
      parent_id?: string
    }
  - Returns: Created comment

discussion.getComments
  - GET: Get discussion comments
  - Auth: Optional
  - Input: { 
      discussion_id: string,
      page?: number
    }
  - Returns: Paginated comments tree
```

### Achievements (`achievement`)

```typescript
achievement.list
  - GET: List all achievements
  - Auth: Optional
  - Returns: Achievement[] with user progress

achievement.getUserAchievements
  - GET: Get user's achievements
  - Auth: Required
  - Returns: UserAchievement[] with details

achievement.getProgress
  - GET: Get achievement progress
  - Auth: Required
  - Input: { achievement_id: string }
  - Returns: Progress towards achievement
```

### Admin (`admin`)

```typescript
admin.programs.create
  - POST: Create new program
  - Auth: Required (Admin)
  - Input: Program data
  - Returns: Created program

admin.programs.update
  - PUT: Update program
  - Auth: Required (Admin)
  - Input: Program updates
  - Returns: Updated program

admin.content.upload
  - POST: Upload content
  - Auth: Required (Admin)
  - Input: File data
  - Returns: Upload URL and metadata

admin.analytics.overview
  - GET: Get platform analytics
  - Auth: Required (Admin)
  - Returns: Analytics dashboard data
```

## Error Handling

All endpoints return consistent error responses:

```typescript
{
  code: 'ERROR_CODE',
  message: 'Human readable message',
  details?: object
}
```

Common error codes:
- `UNAUTHORIZED`: Missing or invalid authentication
- `FORBIDDEN`: Insufficient permissions
- `NOT_FOUND`: Resource not found
- `VALIDATION_ERROR`: Invalid input data
- `RATE_LIMITED`: Too many requests
- `INTERNAL_ERROR`: Server error

## Rate Limiting

- Authenticated users: 100 requests per minute
- Unauthenticated users: 20 requests per minute
- File uploads: 10 per hour

## Websocket Events (Future)

For real-time features:
- `progress.update`: Real-time progress updates
- `discussion.new_comment`: New discussion comments
- `achievement.earned`: Achievement notifications
- `course.peer_activity`: See other learners' progress