# School Assistant Agent - Requirements Definition

## 1. Project Overview

### 1.1 Purpose
Develop an AI assistant agent to support programming school students in autonomous learning. This agent aims to facilitate students' thinking processes and develop problem-solving abilities rather than providing direct answers.

### 1.2 Background
- In programming education, providing immediate answers prevents deep understanding and self-solving abilities
- Need to reduce instructor workload and provide 24/7 learning support
- Appropriate guidance tailored to each student's level and comprehension is required

### 1.3 Scope
- Q&A support for programming learning
- Providing hints and step-by-step guidance
- Code review and feedback
- Tracking learning progress

## 2. Stakeholders

### 2.1 Primary Stakeholders
- **Students**: Learners studying programming (beginner to intermediate level)
- **Instructors**: School teachers and mentors
- **School Administrators**: Managers responsible for curriculum and educational effectiveness

### 2.2 User Personas
- **Beginner Students**: Just starting to learn programming basics
- **Intermediate Students**: Understanding basic syntax but struggling with applied problems
- **Instructors**: Responding to student questions and monitoring progress

## 3. Functional Requirements

### 3.1 Question Response Functionality

#### 3.1.1 Question Understanding and Analysis
- Accept questions from students in natural language
- Analyze question intent and identify where students are struggling
- Determine the difficulty level of questions

#### 3.1.2 Progressive Hint Provision
- Provide step-by-step hints rather than direct answers
- Adjust hint detail level according to student comprehension
- Guide thinking through Socratic questioning

**Example**:
```
Student: "My for loop isn't working"
Agent: "First, how many times do you expect the loop to execute?"
Student: "10 times"
Agent: "Let's check together how many times the current range specification will execute the loop. What does range(10) return?"
```

#### 3.1.3 Error Analysis Support
- Teach how to interpret error messages
- Explain error types (syntax errors, logic errors, runtime errors)
- Guide debugging procedures

### 3.2 Code Review Functionality

#### 3.2.1 Code Evaluation
- Analyze structure of submitted code
- Evaluate correctness, readability, and efficiency
- Provide constructive feedback on improvements

#### 3.2.2 Best Practice Suggestions
- Suggest better coding styles
- Introduce language-specific idioms and patterns
- Advice from security and performance perspectives

#### 3.2.3 Alternative Approach Presentation
- Show multiple solution methods and explain pros/cons
- Deepen understanding by having students make their own choices

### 3.3 Learning Progress Management

#### 3.3.1 Learning History Recording
- Save student question history
- Identify common stumbling points
- Analyze learning patterns

#### 3.3.2 Comprehension Assessment
- Estimate student understanding through dialogue
- Identify weak areas and encourage review
- Provide feedback based on achievement level

#### 3.3.3 Learning Recommendations
- Suggest next topics appropriate to student's current level
- Introduce related learning resources
- Generate customized practice problems

### 3.4 Instructor Support Features

#### 3.4.1 Student Status Monitoring
- View each student's learning progress on dashboard
- Aggregate and visualize common stumbling points
- Identify students needing support

#### 3.4.2 Intervention Timing Notifications
- Notify instructors when students struggle with same problem for extended time
- Alert when many students stumble on specific concept
- Escalate questions to instructors that are difficult for agent to handle

### 3.5 Multi-language Support

#### 3.5.1 Supported Programming Languages (Initial Version)
- Python
- JavaScript
- Java
- C/C++

#### 3.5.2 Natural Languages
- Japanese (primary)
- English (secondary)

## 4. Non-Functional Requirements

### 4.1 Usability
- Intuitive chat interface
- Response time: average within 3 seconds
- Mobile device support

### 4.2 Performance
- Concurrent active users: maximum 100
- Uptime of 99.5% or higher
- p95 response time within 5 seconds

### 4.3 Security and Privacy
- Protection of student code and personal information
- Mandatory HTTPS communication
- Access log recording
- Compliance with GDPR and privacy protection laws

### 4.4 Scalability
- Easy addition of new programming languages
- Customization according to curriculum
- Design allowing AI model updates

### 4.5 Maintainability
- Logging and error tracking system
- Version control and rollback functionality
- Documentation maintenance

## 5. System Architecture Overview

### 5.1 Main Components

```
┌─────────────────────────────────────────────────────────┐
│                      Frontend                           │
│              (Web/Mobile Chat Interface)               │
└─────────────┬───────────────────────────────────────────┘
              │
┌─────────────▼───────────────────────────────────────────┐
│                   API Gateway                           │
│         (Authentication, Routing, Rate Limiting)        │
└─────────────┬───────────────────────────────────────────┘
              │
    ┌─────────┴─────────┬─────────────┬─────────────┐
    │                   │             │             │
┌───▼────────┐  ┌───────▼──────┐  ┌──▼──────┐  ┌──▼──────┐
│ Dialogue   │  │ Code         │  │ Learning│  │ Notif.  │
│ Manager    │  │ Analyzer     │  │ Analytics│ │ Service │
└───┬────────┘  └───────┬──────┘  └──┬──────┘  └──┬──────┘
    │                   │             │             │
    └─────────┬─────────┴─────────────┴─────────────┘
              │
    ┌─────────▼─────────────────────────────────────┐
    │           LLM Orchestrator                    │
    │    (Prompt Management, Context Control)       │
    └─────────┬─────────────────────────────────────┘
              │
    ┌─────────▼─────────────────────────────────────┐
    │       Large Language Model (LLM)              │
    │        (GPT-4, Claude, or Open Source)        │
    └───────────────────────────────────────────────┘
              
    ┌─────────────────────────────────────────────┐
    │           Data Storage Layer                │
    │  ┌──────────┐  ┌──────────┐  ┌──────────┐  │
    │  │ User DB  │  │ Chat     │  │Analytics │  │
    │  │          │  │ History  │  │ Data     │  │
    │  └──────────┘  └──────────┘  └──────────┘  │
    └─────────────────────────────────────────────┘
```

### 5.2 Technology Stack Candidates

#### Frontend
- React or Vue.js
- WebSocket (real-time communication)

#### Backend
- Python (FastAPI or Flask)
- Node.js (Express)

#### Database
- PostgreSQL (main database)
- Redis (cache, session management)
- MongoDB (conversation logs, unstructured data)

#### AI/ML
- OpenAI API (GPT-4)
- Anthropic Claude API
- Or LangChain + Open Source LLM

#### Infrastructure
- Docker / Kubernetes
- AWS / GCP / Azure

## 6. Use Cases

### 6.1 Use Case 1: Basic Question Response

**Actor**: Beginner Student

**Preconditions**: Student is logged in

**Flow**:
1. Student asks "What's the difference between lists and arrays in Python?"
2. Agent understands question intent
3. Counter-questions: "First, what data structures do you commonly use in Python?"
4. Explains step-by-step based on student response
5. Asks questions to confirm understanding
6. Confirms student comprehension and suggests related practice problems

**Postconditions**: Conversation history is saved, learning progress is updated

### 6.2 Use Case 2: Code Review Request

**Actor**: Intermediate Student

**Preconditions**: Student has completed assignment code

**Flow**:
1. Student submits code to agent
2. Agent analyzes code
3. Confirms intent: "What processing should this code perform?"
4. Questions for operation verification: "What is the expected output?"
5. Questions to help student notice code issues step-by-step
6. Guides student to think of improvements themselves
7. Final feedback and best practice presentation

**Postconditions**: Review results are saved and added to student growth record

### 6.3 Use Case 3: Error Resolution Support

**Actor**: Beginner Student

**Preconditions**: Student encounters error during program execution

**Flow**:
1. Student pastes error message
2. Agent identifies error type
3. Questions: "Which part of this error message do you think is important?"
4. Teaches how to read error messages
5. "Did you find the line number where the error occurred?"
6. Guides debugging steps progressively
7. Supports student to solve independently
8. Advice on avoiding similar errors

**Postconditions**: Error resolution process is recorded and added to common errors database

### 6.4 Use Case 4: Instructor Progress Check

**Actor**: Instructor

**Preconditions**: Instructor accesses dashboard

**Flow**:
1. Instructor logs into dashboard
2. Checks overall class learning progress
3. Views detailed activity history of specific students
4. Reviews "students needing support" list identified by agent
5. Decides on direct intervention as needed

**Postconditions**: Instructor confirmation record is saved

## 7. Success Criteria

### 7.1 Quantitative Metrics

- **Student Satisfaction**: User rating 4.0/5.0 or higher
- **Problem Resolution Rate**: 70% or higher rate of students solving problems independently with agent support
- **Response Time**: Average response time within 3 seconds
- **Usage Rate**: Weekly usage rate of active users 60% or higher
- **Escalation Rate**: Question escalation rate to instructors 20% or lower

### 7.2 Qualitative Metrics

- Students feel they "understood on their own" rather than "were told the answer"
- Instructor question response time is reduced
- Students' self-solving abilities improve
- Learning motivation for programming is maintained/improved

## 8. Constraints

### 8.1 Technical Constraints
- LLM API usage cost limit: Within monthly budget
- Response time: Long processes complete within 10 seconds
- Data retention period: Personal data maximum 2 years

### 8.2 Business Constraints
- Development period: 3 months to initial version release
- Budget: Development cost within budget
- Target student count: Maximum 100 students in initial phase

### 8.3 Legal Constraints
- Compliance with privacy protection laws
- Parental consent for handling minor data
- Adherence to ethical guidelines for AI-assisted education

## 9. Risks and Countermeasures

### 9.1 Technical Risks

| Risk | Impact | Countermeasure |
|------|--------|----------------|
| LLM generates inappropriate responses | High | Response filtering mechanism, human review system |
| API cost overrun | Medium | Usage monitoring, caching strategy, alternative LLM consideration |
| System downtime | High | Redundancy, automatic failover, regular backups |

### 9.2 Educational Risks

| Risk | Impact | Countermeasure |
|------|--------|----------------|
| Students become too dependent on agent | Medium | Usage limits, progressive hint design, instructor monitoring |
| Agent gives away too many answers | High | Prompt engineering optimization, continuous improvement |
| Student motivation decline | Medium | Engagement features, growth visualization, gamification |

## 10. Future Enhancement Plan

### Phase 1 (Initial Release: 3 months)
- Basic question response functionality
- Python support
- Web chat interface
- Basic learning history recording

### Phase 2 (6 months)
- JavaScript, Java support
- Full code review functionality implementation
- Instructor dashboard
- Mobile app support

### Phase 3 (12 months)
- Advanced learning analytics
- Personalized learning paths
- Peer review functionality
- Gamification elements
- Integration with other LMS (Learning Management System)

## 11. Appendix

### 11.1 Glossary

- **Socratic Method**: Educational technique of encouraging thinking through questions and helping find answers themselves
- **Escalation**: Transferring questions that AI cannot handle to human instructors
- **LLM (Large Language Model)**: Models like GPT-4 and Claude
- **Prompt Engineering**: Techniques for giving appropriate instructions to AI

### 11.2 References

- Research on prior cases of programming education
- Papers on AI-assisted educational support systems
- Educational informatization guidelines

### 11.3 Approval

| Role | Name | Approval Date | Signature |
|------|------|---------------|-----------|
| Project Owner | | | |
| Technical Lead | | | |
| Education Lead | | | |

---

**Document Version**: 1.0  
**Created**: January 19, 2026  
**Last Updated**: January 19, 2026  
**Author**: School Assistant Agent Development Team
