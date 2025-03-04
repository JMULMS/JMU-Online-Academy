# erDiagram

## USERS Table
    USERS {
      UUID user_id PK
      VARCHAR first_name
      VARCHAR last_name
      VARCHAR email
      TEXT password_hash
      ENUM role
      TEXT profile_image
      ENUM status
      TIMESTAMP created_at
      TIMESTAMP updated_at
    }
    
    
## COURSES Table
    COURSES {
      UUID course_id PK
      VARCHAR course_name
      ENUM course_level
      VARCHAR provider_type
      TEXT learning_objectives
      TEXT description
      TEXT thumbnail_url
      TIMESTAMP created_at
    }
    
## ENROLLMENTS Table
    ENROLLMENTS {
      UUID enrollment_id PK
      UUID user_id FK
      UUID course_id FK
      ENUM status
      TIMESTAMP enrolled_at
    }
    
## COURSE_CONTENT Table
    COURSE_CONTENT {
      UUID content_id PK
      UUID course_id FK
      ENUM content_type
      TEXT content_url
      BOOLEAN extra_credit
    }
    
## ASSESSMENTS Table
    ASSESSMENTS {
      UUID assessment_id PK
      UUID course_id FK
      ENUM assessment_type
      INT total_points
    }
    
## DISCUSSIONS (Tag & Talk Discussions) Table
    DISCUSSIONS {
      UUID discussion_id PK
      UUID course_id FK
      TEXT tagged_content
      TEXT tagged_content_url
      VARCHAR discussion_title
      TEXT discussion_content
      DATE discussion_date
    }
    
## INSTRUCTOR_ASSESSMENTS Table
    INSTRUCTOR_ASSESSMENTS {
      UUID assessment_id PK
      UUID instructor_id FK
      ENUM assessment_type
      INT score
      ENUM status
    }
    
## USER_ASSESSMENTS Table 
    USER_ASSESSMENTS {
      UUID user_assessment_id PK
      UUID assessment_id FK
      UUID user_id FK
      INT score
      ENUM status
    }
    
## DISCUSSION_COMMENTS Table
    DISCUSSION_COMMENTS {
      UUID comment_id PK
      UUID discussion_id FK
      UUID user_id FK
      TEXT comment_text
      TIMESTAMP created_at
    }
    
# Relationships
    USERS ||--o{ ENROLLMENTS : "enrolls in"

    COURSES ||--o{ ENROLLMENTS : "has enrollments"
    
    USERS ||--o{ INSTRUCTOR_ASSESSMENTS : "takes"
    
    USERS ||--o{ DISCUSSION_COMMENTS : "writes"
    
    USERS ||--o{ USER_ASSESSMENTS : "completes"
    
    COURSES ||--o{ COURSE_CONTENT : "has content"
    
    COURSES ||--o{ ASSESSMENTS : "has assessments"

    ASSESSMENTS ||--o{ USER_ASSESSMENTS : "records"
    
    COURSES ||--o{ DISCUSSIONS : "hosts discussions"

    DISCUSSIONS ||--o{ DISCUSSION_COMMENTS : "contains"
