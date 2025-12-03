# Week 1 Learning Syllabus - Foundation Architecture & Prompt Engineering

## Core Concepts Overview

### What You're Learning This Week
1. **System Architecture** - How to design the blueprint of DressUp's entire technical structure
2. **Prompt Engineering** - How to write instructions that make AI do exactly what you need
3. **Decision Frameworks** - Mental models for making fast, logical product decisions
4. **Fashion Industry Basics** - Understanding the business context DressUp operates in

### Why Each Concept Matters for DressUp
- **System Architecture:** You need to design how user data, outfit logic, and recommendations flow through DressUp before building anything
- **Prompt Engineering:** DressUp will use 50+ AI prompts to analyze outfits, generate recommendations, and understand user preferences
- **Decision Frameworks:** You'll face 100+ feature decisions; frameworks prevent analysis paralysis
- **Fashion Industry:** Understanding retail economics shows why DressUp is valuable to both users AND businesses

---

## PART 1: SYSTEM ARCHITECTURE

### 1.1 What is System Architecture?

#### Clear Definition
System architecture is the complete blueprint of how a software application is structured - like an architect's plan for a building showing all rooms, how they connect, and what goes where. It defines what components exist, how data flows between them, and how users interact with the system.

#### How It Works (Mental Model)
Think of system architecture as designing a restaurant:
- **Entities** = The things in your restaurant (tables, menu items, customers, orders)
- **Relationships** = How things connect (customers sit at tables, orders contain menu items)
- **Data Flow** = The journey from entrance to exit (customer enters → seated → orders → food prepared → served → payment → exit)
- **System Layers** = Different areas with different purposes (dining room for customers, kitchen for cooking, office for management)

#### Industry Terminology
- **Architecture:** The high-level structure and design of a system
- **System Design:** The process of defining architecture, components, and data flow
- **Technical Architecture:** The specific technologies and how they integrate
- **Solution Architecture:** How the system solves the business problem
- **Enterprise Architecture:** How this system fits with other systems (awareness only)

#### Practical Application to DressUp
Your DressUp architecture must define:
- What data you store (users, wardrobe items, outfits, weather)
- How components interact (weather API → outfit logic → recommendation → user interface)
- Where processing happens (in Glide, in Google Sheets, in external APIs)
- How users move through the app (onboarding → wardrobe → daily outfit → feedback)

#### Depth Required
**Practitioner Level:** You need to actually create architecture diagrams and documentation that another person could use to understand and build DressUp.

#### Common Misconceptions
- **Wrong:** Architecture is only about technology choices
- **Right:** Architecture is about structure and relationships; technology is just implementation
- **Wrong:** Architecture is fixed once designed
- **Right:** Architecture evolves but core structure should be stable

---

### 1.2 Entities: The Building Blocks

#### Clear Definition
An entity is any "thing" in your system that you need to track information about. In database terms, each entity typically becomes a table. Entities have attributes (properties) that describe them.

#### How It Works (Mental Model)
Think of entities as nouns in your system's story:
- **User** = A person using DressUp
- **WardrobeItem** = A piece of clothing
- **Outfit** = A combination of wardrobe items
- **Weather** = Today's weather conditions

Each entity is like a filing cabinet drawer - you have one drawer for Users, one for WardrobeItems, etc.

#### Industry Terminology
- **Entity:** A distinct thing you track in your system
- **Attribute:** A property or characteristic of an entity (User has name, email)
- **Instance/Record:** One specific example of an entity (John Smith is one User instance)
- **Entity-Relationship Diagram (ERD):** Visual diagram showing entities and how they connect
- **Domain Model:** All entities and relationships that represent your business

#### Practical Application to DressUp
Your core entities:
1. **User:** name, email, style_preference, location
2. **WardrobeItem:** type, color, formality, weather_appropriate, image_url
3. **Outfit:** date, weather_context, items_included, user_rating
4. **StyleProfile:** formality_preference, color_preferences, fit_preferences
5. **WeatherData:** date, temperature, precipitation, wind

#### How to Identify Entities
Ask yourself:
1. What nouns appear repeatedly when describing DressUp?
2. What do I need to remember between user sessions?
3. What would each database table represent?

Rule: If you need to track multiple instances of something, it's probably an entity.

#### Depth Required
**Practitioner Level:** You must identify all entities, define their attributes, and document them clearly.

#### Common Misconceptions
- **Wrong:** Every concept needs to be an entity
- **Right:** Only things you need to track and store become entities
- **Wrong:** Entities are independent
- **Right:** Entities are often connected through relationships

---

### 1.3 Relationships: How Entities Connect

#### Clear Definition
A relationship describes how two entities are associated with each other. Relationships have cardinality (how many of each entity can be connected).

#### How It Works (Mental Model)
Relationships are like the verbs connecting your nouns:
- User **owns** WardrobeItems
- Outfit **contains** WardrobeItems  
- User **rates** Outfits
- Weather **influences** Outfit recommendations

#### Types of Relationships

**One-to-One (1:1)**
- Definition: Each instance of Entity A relates to exactly one instance of Entity B
- Example: User has one StyleProfile, StyleProfile belongs to one User
- Implementation: Foreign key in either table

**One-to-Many (1:N)**
- Definition: One instance of Entity A relates to multiple instances of Entity B
- Example: User owns many WardrobeItems, each WardrobeItem belongs to one User
- Implementation: Foreign key in the "many" table pointing to the "one"

**Many-to-Many (M:N)**
- Definition: Multiple instances of Entity A relate to multiple instances of Entity B
- Example: Outfit contains many WardrobeItems, WardrobeItem appears in many Outfits
- Implementation: Requires junction/bridge table

#### Industry Terminology
- **Cardinality:** The count relationship (one-to-one, one-to-many, many-to-many)
- **Foreign Key:** Field in one table that references primary key in another table
- **Primary Key:** Unique identifier for each record in a table
- **Junction/Bridge/Associative Table:** Table that implements many-to-many relationships
- **Referential Integrity:** Ensuring relationships point to valid records

#### Practical Application to DressUp
Key relationships:
1. User → WardrobeItems (One-to-Many: User has many items)
2. Outfit ↔ WardrobeItems (Many-to-Many: Outfit has multiple items, items in multiple outfits)
3. User → Outfits (One-to-Many: User has many outfit recommendations)
4. Weather → Outfits (One-to-Many: One weather condition, multiple outfit options)

#### Depth Required
**Practitioner Level:** You need to identify all relationships and know how to implement them in your data model.

#### Common Misconceptions
- **Wrong:** Many-to-many relationships can be implemented directly
- **Right:** Many-to-many always requires a junction table
- **Wrong:** Relationships are optional
- **Right:** Relationships are crucial for data integrity

---

### 1.4 Data Flow & System Layers

#### Clear Definition
Data flow describes how information moves through your system from input to output. System layers organize functionality into logical groupings with specific responsibilities.

#### How It Works (Mental Model)
**Data Flow - Like Water Through Pipes:**
1. **Input** → User adds wardrobe item
2. **Processing** → System categorizes and stores item
3. **Transformation** → Combine with weather to generate outfits
4. **Output** → Display recommended outfit to user

**System Layers - Like Floors in a Building:**
- **Presentation Layer (Top Floor):** What users see and interact with (Glide interface)
- **Business Logic Layer (Middle Floor):** Rules and processing (outfit matching logic)
- **Data Layer (Ground Floor):** Storage and retrieval (Google Sheets database)
- **Integration Layer (Basement):** External connections (Weather API, future ML)

#### Industry Terminology
- **State Management:** How system tracks current status/data
- **Data Pipeline:** Series of processing steps data goes through
- **ETL:** Extract, Transform, Load - moving data between systems
- **Business Logic:** Rules that determine how data is processed
- **Separation of Concerns:** Each layer handles specific responsibilities

#### Practical Application to DressUp
Your data flow:
1. **Morning Trigger:** 7 AM scheduled task fires
2. **Weather Fetch:** Get today's forecast from API
3. **Outfit Generation:** Apply rules to match weather + wardrobe
4. **Notification:** Send outfit recommendation
5. **User Response:** Open app, view outfit, provide rating
6. **Feedback Loop:** Store rating, improve future recommendations

#### Depth Required
**Practitioner Level:** Create data flow diagrams showing every major path through DressUp.

---

### 1.5 Architecture Documentation

#### Clear Definition
Architecture documentation is the written and visual representation of your system design that others can understand and use to build or maintain the system.

#### How It Works (Mental Model)
Like a building's blueprints include floor plans, electrical diagrams, and plumbing schematics, architecture documentation includes:
- System overview (the big picture)
- Component diagrams (the parts)
- Data flow diagrams (how information moves)
- Entity-relationship diagrams (data structure)
- Decision rationale (why you designed it this way)

#### What Notation to Use
**Simple Box-and-Arrow Diagrams:**
- Rectangles = Components/Entities
- Arrows = Data flow/Relationships
- Cylinders = Databases
- Clouds = External services

**Standard Notations (Awareness):**
- UML (Unified Modeling Language) - Industry standard but complex
- C4 Model - Context, Containers, Components, Code
- ERD notation - Crow's foot for relationships

For MVP: Use simple, clear diagrams with a legend explaining your symbols.

#### Practical Application to DressUp
You'll create:
1. **System Overview:** One-page diagram showing all major components
2. **Entity-Relationship Diagram:** All entities and their relationships
3. **Data Flow Diagram:** Morning notification flow, user interaction flow
4. **Architecture Decision Records:** Why you chose Glide, why Google Sheets, etc.

#### Depth Required
**Working Knowledge:** Create clear diagrams others can understand; don't need formal UML.

---

## PART 2: PROMPT ENGINEERING

### 2.1 What is Prompt Engineering?

#### Clear Definition
Prompt engineering is the skill of writing instructions (prompts) that consistently get AI language models to produce the exact output you need. It's like being a precise instructor who knows exactly how to explain tasks to get perfect results.

#### How It Works (Mental Model)
Think of prompt engineering like writing a recipe for someone who's never cooked before:
- **Bad recipe:** "Make pasta" (unclear, inconsistent results)
- **Good recipe:** "Boil 4 cups water, add 1 tsp salt, cook 200g spaghetti for 8 minutes until al dente, drain, serve with sauce" (precise, repeatable)

AI models are like brilliant but literal assistants - they need clear, specific, complete instructions.

#### Why It's a Skill
Prompt engineering requires:
- Understanding how AI models interpret instructions
- Knowing what information to include/exclude
- Testing systematically and debugging failures
- Optimizing for consistency and quality
- Managing token limits and costs

#### Industry Terminology
- **Prompt:** The instruction/question you give to AI
- **Completion:** The AI's response to your prompt
- **Token:** Basic unit of text (roughly 4 characters or 0.75 words)
- **Context Window:** Maximum tokens the model can process at once
- **System Prompt:** Persistent instructions that shape all responses
- **Few-shot Learning:** Providing examples in the prompt
- **Prompt Template:** Reusable prompt structure with variables

#### Practical Application to DressUp
You'll write prompts for:
- Analyzing outfit compatibility ("Rate how well these items work together")
- Generating outfit suggestions ("Suggest professional outfit for 65°F rainy day")
- Understanding user preferences ("Extract style preferences from this feedback")
- Creating style descriptions ("Describe this outfit's aesthetic")

#### Depth Required
**Practitioner Level:** You need to write, test, and optimize 50+ production prompts.

#### Common Misconceptions
- **Wrong:** Good prompts are about using magic words
- **Right:** Good prompts are about clear structure and complete context
- **Wrong:** One perfect prompt works for everything
- **Right:** Different tasks need different prompt strategies

---

### 2.2 The RTCC Framework

#### Clear Definition
RTCC (Role, Task, Context, Constraints) is a structured approach to writing comprehensive prompts that consistently produce high-quality outputs.

#### How Each Component Works

**ROLE - Who the AI Should Be**
- Definition: The perspective, expertise, or persona the AI should adopt
- Purpose: Shapes tone, depth, and approach
- Example: "You are a professional fashion stylist with 10 years of experience"
- Why it matters: Different roles produce different outputs

**TASK - What the AI Should Do**
- Definition: The specific action or output required
- Purpose: Clear, actionable instruction
- Example: "Analyze this outfit and provide a compatibility score from 1-10"
- Why it matters: Vague tasks get vague results

**CONTEXT - Background Information**
- Definition: All relevant information needed to complete the task
- Purpose: Provides necessary knowledge and parameters
- Example: "The user is attending a business conference in Seattle in March"
- Why it matters: Context determines appropriate responses

**CONSTRAINTS - Rules and Limitations**
- Definition: Boundaries, format requirements, and must-not-dos
- Purpose: Ensures output meets specific requirements
- Example: "Limit response to 3 sentences. Only suggest items from user's wardrobe."
- Why it matters: Prevents unwanted variations

#### Full RTCC Example for DressUp

```
ROLE: You are an expert fashion stylist specializing in practical, everyday outfit coordination.

TASK: Analyze the compatibility of these wardrobe items for a professional setting and provide a compatibility score.

CONTEXT: 
- Items: Navy blazer, white t-shirt, black jeans, brown loafers
- Occasion: Client presentation at tech company
- Weather: 68°F, partly cloudy
- User style preference: Smart casual

CONSTRAINTS:
- Score from 1-10 with explanation
- Identify any issues
- Suggest one improvement using existing items
- Keep response under 100 words
```

#### Practical Application to DressUp
Every DressUp prompt should have:
- Role: Fashion expert who understands practical constraints
- Task: Specific analysis or generation needed
- Context: User's wardrobe, weather, occasion, preferences
- Constraints: Use only available items, appropriate for weather, match style preference

#### Depth Required
**Practitioner Level:** Use RTCC for all complex prompts in DressUp.

---

### 2.3 Prompt Types and Techniques

#### System Prompts vs User Prompts

**System Prompts**
- Definition: Persistent instructions that apply to all interactions
- Purpose: Set baseline behavior, personality, constraints
- When to use: For consistent behavior across all outputs
- Example: "You are DressUp's fashion AI. Always be encouraging but honest. Never suggest buying new items unless asked."

**User Prompts**
- Definition: Specific requests within a conversation
- Purpose: Handle individual tasks or queries
- When to use: For specific, one-time requests
- Example: "Rate this outfit for a summer wedding"

#### Few-Shot Prompting

**Zero-Shot**
- Definition: No examples provided
- When to use: Simple, clear tasks
- Example: "Is this outfit formal or casual?"

**One-Shot**
- Definition: One example provided
- When to use: Need specific format
- Example: "Rate this outfit like this example: [Example]. Now rate: [New outfit]"

**Few-Shot**
- Definition: Multiple examples provided (usually 3-5)
- When to use: Complex patterns or specific style needed
- Example: Providing 3 outfit ratings examples before asking for a new rating

#### Chain-of-Thought Prompting

**Definition:** Making the AI show its reasoning step-by-step

**How it works:**
Add "Think step by step" or "Show your reasoning" to prompts

**Example for DressUp:**
```
Analyze if this outfit works for a job interview. Think through:
1. Formality level of each item
2. How items work together
3. Appropriateness for interview context
4. Final recommendation
```

**Why use it:**
- More accurate results
- Can debug wrong answers
- Users understand the logic

#### Depth Required
**Practitioner Level:** Master all techniques, know when to use each.

---

### 2.4 Prompt Optimization & Testing

#### How to Debug Bad Prompts

**Common Failure Patterns:**
1. **Inconsistent outputs** → Add more constraints
2. **Wrong format** → Provide explicit format example
3. **Missing information** → Add more context
4. **Too verbose** → Add length constraints
5. **Off-topic** → Clarify role and task

**Debugging Process:**
1. Identify what's wrong with output
2. Hypothesize cause (missing context? unclear task?)
3. Adjust one element
4. Test 5-10 times
5. If fixed, document. If not, try next hypothesis

#### Testing Systematically

**Test Cases for Each Prompt:**
- Edge cases (empty wardrobe, extreme weather)
- Typical cases (normal outfit, normal weather)
- Adversarial cases (conflicting constraints)

**Quality Metrics:**
- Accuracy: Does it give correct recommendations?
- Consistency: Same input = similar output?
- Format: Follows specified structure?
- Tone: Appropriate for DressUp brand?

#### Prompt Libraries

**Organization Structure:**
```
/prompts
  /analysis
    - outfit_compatibility.txt
    - style_identification.txt
  /generation  
    - outfit_suggestion.txt
    - style_description.txt
  /user_interaction
    - feedback_interpretation.txt
    - preference_extraction.txt
```

**Version Control:**
- Keep versions: outfit_compatibility_v1.txt, _v2.txt
- Document changes and why
- Track performance metrics

#### Depth Required
**Practitioner Level:** Build systematic testing process, maintain organized library.

---

### 2.5 Model Differences & Parameters

#### Claude vs ChatGPT Strengths

**Claude Strengths:**
- Longer context window (100k+ tokens)
- Better at following complex instructions
- More consistent formatting
- Stronger at analysis tasks

**ChatGPT Strengths:**
- Faster response times
- Better at creative variations
- Stronger visual understanding (GPT-4V)
- More accessible API pricing

**For DressUp:**
Use Claude for complex outfit analysis, ChatGPT for quick suggestions

#### Temperature and Parameters

**Temperature (0.0 to 1.0)**
- Definition: Controls randomness/creativity
- 0.0 = Deterministic, same output every time
- 0.7 = Balanced creativity and consistency
- 1.0 = Maximum creativity, different every time
- DressUp setting: 0.3-0.5 for consistency with slight variation

**Other Parameters (Awareness):**
- **Top-p:** Alternative to temperature, controls probability distribution
- **Max_tokens:** Maximum response length
- **Stop_sequences:** Text that stops generation
- **Frequency_penalty:** Reduces repetition

#### Token Limits and Context Windows

**What's a Token:**
- Roughly 4 characters or 0.75 words
- "Hello world" = 2 tokens
- Longer words might be multiple tokens

**Context Window:**
- Total tokens model can process (input + output)
- GPT-4: 8k-32k tokens
- Claude: 100k+ tokens

**For DressUp:**
- Keep prompts under 500 tokens
- Reserve space for wardrobe data (possibly 1000+ tokens)
- Output typically 100-200 tokens

**Cost Implications:**
- Charged per token (input + output)
- Optimize prompts for brevity without losing clarity
- Cache common responses

#### Depth Required
**Working Knowledge:** Understand differences, set appropriate parameters.

---

## PART 3: DECISION FRAMEWORKS

### 3.1 The Kano Model

#### Clear Definition
The Kano Model categorizes features based on how they affect user satisfaction. It helps you understand which features are essential, which improve satisfaction linearly, and which delight users.

#### Three Categories

**Must-Have (Basic/Threshold)**
- Definition: Features users expect; absence causes dissatisfaction
- Satisfaction curve: Absence = very unhappy, presence = neutral
- DressUp examples:
  - Save wardrobe items
  - See outfit recommendations
  - Works on mobile

**Performance (Linear)**
- Definition: More is better; satisfaction increases linearly
- Satisfaction curve: Linear relationship with satisfaction
- DressUp examples:
  - Outfit variety (more options = happier)
  - Recommendation accuracy
  - Loading speed

**Delighters (Excitement)**
- Definition: Unexpected features that create joy
- Satisfaction curve: Absence = neutral, presence = very happy
- DressUp examples:
  - Color coordination analysis
  - Packing list for trips
  - Style evolution insights

#### How to Use Kano for DressUp

**Classification Process:**
1. List potential features
2. Ask: "How would users feel if this exists?" 
3. Ask: "How would users feel if this doesn't exist?"
4. Plot on Kano matrix
5. Prioritize must-haves first, then performance, then delighters

**Week 1 Application:**
Classify your 50+ feature ideas into Kano categories to identify MVP must-haves.

#### Depth Required
**Working Knowledge:** Use to classify features, don't need academic depth.

#### Common Misconceptions
- **Wrong:** Build delighters first to stand out
- **Right:** Must-haves first or product fails regardless of delighters
- **Wrong:** All features fit neatly in one category
- **Right:** Features can move between categories over time

---

### 3.2 MoSCoW Method

#### Clear Definition
MoSCoW is a prioritization framework that forces clear decisions about what to build by categorizing features into Must have, Should have, Could have, Won't have.

#### Categories Explained

**Must Have**
- Definition: Core features without which product doesn't work
- Test: If missing, does the product fail its basic purpose?
- DressUp Must Haves:
  - Add wardrobe items
  - Get daily outfit recommendation
  - Weather integration

**Should Have** 
- Definition: Important but product works without them
- Test: Painful to leave out but not fatal
- DressUp Should Haves:
  - Rate outfits
  - Style preference quiz
  - Multiple outfit options

**Could Have**
- Definition: Nice to have if time/resources allow
- Test: Would improve experience but not essential
- DressUp Could Haves:
  - Social sharing
  - Outfit history
  - Color analysis

**Won't Have (This Release)**
- Definition: Explicitly excluded from current scope
- Test: Good ideas for later versions
- DressUp Won't Haves:
  - Shopping recommendations
  - Social features
  - AI-generated outfit images

#### Ruthless Prioritization

**The 60-20-20 Rule:**
- 60% effort on Must Haves
- 20% on Should Haves
- 20% on Could Haves
- 0% on Won't Haves

**How to Be Ruthless:**
1. Start with everything in "Could Have"
2. Fight to promote to "Should Have"
3. Fight harder to promote to "Must Have"
4. Be explicit about "Won't Have" to prevent scope creep

#### Depth Required
**Practitioner Level:** You'll use this weekly to make scope decisions.

---

### 3.3 ICE Scoring

#### Clear Definition
ICE stands for Impact × Confidence × Ease. It's a framework for prioritizing features by scoring each on these dimensions and multiplying for a total score.

#### The Formula

**Impact (1-10)**
- Definition: How much this improves user experience or business metrics
- 10 = Transforms user experience
- 5 = Noticeable improvement
- 1 = Minimal difference

**Confidence (1-10)**
- Definition: How sure you are about Impact
- 10 = Certain based on data/research
- 5 = Educated guess
- 1 = Wild speculation

**Ease (1-10)**
- Definition: How easy to implement
- 10 = Few hours
- 5 = Few days
- 1 = Weeks of work

**Total Score = Impact × Confidence × Ease**
- Maximum: 1000
- Minimum: 1
- Higher score = Higher priority

#### Application to DressUp Features

Example Scoring:
- Weather integration: Impact(9) × Confidence(8) × Ease(7) = 504
- Social sharing: Impact(4) × Confidence(5) × Ease(9) = 180
- ML recommendations: Impact(10) × Confidence(7) × Ease(2) = 140

Build in order of score.

#### Depth Required
**Working Knowledge:** Use for quick prioritization decisions.

---

### 3.4 Game Theory Basics for Product Design

#### Clear Definition
Game theory in product design means understanding the incentives, motivations, and behaviors that drive user actions, and designing systems that align user and product goals.

#### Key Concepts

**Incentives**
- Definition: What motivates users to take action
- DressUp incentives:
  - Save time (decision fatigue)
  - Look good (social approval)
  - Use wardrobe fully (economic value)
  - Learn style (self-improvement)

**Friction**
- Definition: Anything that makes actions harder
- Good friction: Confirmation before deleting wardrobe
- Bad friction: Too many steps to add items
- Balance: Remove bad friction, keep protective friction

**Feedback Loops**
- Definition: Output of system influences future input
- Positive loop: Good recommendations → More usage → Better data → Better recommendations
- Negative loop: Bad recommendations → Less usage → Less data → Worse recommendations
- Design goal: Create positive loops

**Equilibrium**
- Definition: Stable state system settles into
- DressUp equilibrium: Daily usage becomes habit
- Design for: Easy to start, rewarding to continue, hard to leave

#### Depth Required
**Awareness Level:** Understand concepts, apply basic thinking.

---

## PART 3.5: INTRODUCTION TO AGENTIC AI THINKING

### 3.5.1 What Are AI Agents?

#### Clear Definition
AI agents are systems that can break down complex tasks into steps, use multiple tools or prompts in sequence, maintain context across interactions, and make decisions about what to do next - unlike single prompts that produce one-shot outputs.

#### How It Works (Mental Model)
Think of the difference between a chef and a recipe:
- **Single Prompt** = Following one recipe step (chop onions)
- **AI Agent** = The chef who plans the meal, checks ingredients, adjusts for preferences, coordinates multiple dishes, and explains choices

Or in assistant terms:
- **Single Prompt Assistant:** Answers your specific question
- **AI Agent Assistant:** Understands your goal, asks clarifying questions, breaks down the problem, executes multiple steps, and verifies the result

#### Single Prompt vs Agent Example

**Single Prompt Approach:**
```
User: "Generate an outfit for tomorrow"
AI: "Here's an outfit: blue shirt, black pants, brown shoes"
Done.
```

**Agentic Approach:**
```
Agent Process:
1. Check tomorrow's weather forecast
2. Review user's calendar for occasions
3. Analyze wardrobe inventory
4. Consider recent outfit history
5. Apply style preferences
6. Generate 3 options with reasoning
7. Explain trade-offs between options

User gets: "Based on tomorrow's 65°F partly cloudy weather and your 
client meeting, here are 3 options:
1. Professional: Navy blazer... (because client meeting)
2. Smart casual: Cardigan... (balanced comfort/professional)
3. Bold choice: Patterned shirt... (make an impression)
Each rated for: comfort, appropriateness, style impact"
```

#### Industry Terminology
- **Agent:** Autonomous system that can plan and execute multi-step tasks
- **Tool Use:** Agent's ability to call different functions/APIs
- **Chain of Thought:** Sequential reasoning through problems
- **Task Decomposition:** Breaking complex goals into steps
- **Context Management:** Maintaining state across interactions
- **Orchestration:** Coordinating multiple sub-tasks
- **ReAct Pattern:** Reasoning + Acting in loops
- **Agentic Workflow:** Multi-step process with decision points

#### Why Agents Matter for AI Systems

**Limitations of Single Prompts:**
- Can't gather additional information
- No ability to verify outputs
- Fixed process, no adaptation
- Single attempt at solution

**Agent Advantages:**
- Break complex problems into manageable steps
- Use different tools for different parts
- Verify and correct mistakes
- Adapt based on intermediate results
- Explain reasoning process

#### Components of an AI Agent

**1. Planning Module**
- Understands the goal
- Breaks down into subtasks
- Determines execution order

**2. Execution Module**
- Carries out each step
- Calls appropriate tools/prompts
- Handles errors

**3. Memory Module**
- Tracks conversation context
- Stores intermediate results
- Maintains user preferences

**4. Decision Module**
- Evaluates results
- Decides next actions
- Knows when task is complete

#### Practical Application to DressUp

**Current (Single Prompt) Approach:**
```python
# Simple prompt for outfit
def generate_outfit(weather, wardrobe):
    prompt = f"Given {weather} and {wardrobe}, suggest outfit"
    return ai_complete(prompt)
```

**Future (Agentic) Approach:**
```python
class OutfitAgent:
    def plan_outfit(self, user, date):
        # Step 1: Gather context
        weather = self.check_weather(date)
        calendar = self.check_calendar(user, date)
        wardrobe = self.analyze_wardrobe(user)
        recent_outfits = self.get_history(user, days=7)
        
        # Step 2: Determine requirements
        requirements = self.assess_needs(
            weather, calendar, user.preferences
        )
        
        # Step 3: Generate options
        candidates = self.create_outfits(
            wardrobe, requirements, recent_outfits
        )
        
        # Step 4: Evaluate and rank
        scored_outfits = self.evaluate_options(
            candidates, requirements
        )
        
        # Step 5: Explain reasoning
        explanations = self.explain_choices(
            scored_outfits, requirements
        )
        
        return scored_outfits[:3], explanations
```

#### Agentic Possibilities for DressUp (Brainstorm Exercise)

**Week 1 Preview (You'll Document These):**

1. **Wardrobe Optimization Agent**
   - Analyzes entire wardrobe
   - Identifies gaps and redundancies
   - Suggests items that maximize outfit combinations
   - Creates capsule wardrobe plans

2. **Style Evolution Agent**
   - Tracks style changes over time
   - Identifies emerging preferences
   - Suggests gradual style transitions
   - Learns from fashion inspiration sources

3. **Shopping Assistant Agent**
   - Monitors wardrobe gaps
   - Tracks sales and deals
   - Evaluates items against existing wardrobe
   - Calculates cost-per-wear value

4. **Packing Agent**
   - Checks trip destination weather
   - Considers planned activities
   - Minimizes items while maximizing outfits
   - Creates day-by-day outfit plan

5. **Closet Cleanup Agent**
   - Identifies unworn items
   - Suggests donation candidates
   - Finds forgotten gems to reintegrate
   - Reorganizes by frequency of use

#### Connection to Week 3

**What You'll Learn in Week 3:**
- How agents decompose complex tasks
- Prompt chaining strategies
- State management across steps
- Error handling and recovery
- When to use agents vs simple prompts

**Week 1 Foundation Enables:**
- Understanding base prompts that agents will chain
- System architecture that supports multi-step processes
- Decision frameworks agents will use
- Clear requirements agents must meet

#### Implementation Considerations

**Start Simple (Week 1-2):**
- Single prompts for each function
- Manual coordination between steps
- Basic decision logic

**Evolve to Agents (Week 3+):**
- Automated task decomposition
- Dynamic prompt chaining
- Adaptive decision-making
- Self-correcting processes

#### Depth Required
**Awareness Level:** Understand the concept and possibilities, not implementation details. You'll document ideas, not build agents yet.

#### Common Misconceptions
- **Wrong:** Agents are just fancy chatbots
- **Right:** Agents actively decompose and execute complex tasks
- **Wrong:** Every AI task needs an agent
- **Right:** Use agents for multi-step, decision-rich processes
- **Wrong:** Agents are always better than single prompts
- **Right:** Simple tasks should stay simple; agents add complexity

---

## PART 4: FASHION INDUSTRY BASICS

### 4.1 Fashion Calendar & Seasons

#### Clear Definition
The fashion calendar is the industry-wide schedule that determines when new collections are designed, produced, shown, and sold.

#### Traditional Fashion Seasons

**Spring/Summer (S/S)**
- Design: September-November (previous year)
- Fashion Shows: September (prior year)
- Production: December-February
- In Stores: February-July
- Clearance: July-August

**Fall/Winter (F/W)**
- Design: March-May
- Fashion Shows: February
- Production: June-August
- In Stores: August-January
- Clearance: January-February

#### Why This Matters for DressUp
- Users' wardrobes follow seasonal patterns
- Outfit recommendations must consider seasonality
- "New arrivals" in stores affect what users want to wear
- Clearance periods = users adding to wardrobe

#### Depth Required
**Awareness Level:** Understand timing, don't memorize exact dates.

---

### 4.2 Supply Chain Flow

#### Clear Definition
The fashion supply chain is the complete journey from design concept to customer purchase, including all steps of production and distribution.

#### The Flow

**Design → Production → Distribution → Retail**

1. **Design** (3-6 months)
   - Trend research
   - Sketches and prototypes
   - Material selection
   - Tech packs (specifications)

2. **Production** (3-4 months)
   - Sourcing materials
   - Manufacturing
   - Quality control
   - Shipping to distribution centers

3. **Distribution** (2-4 weeks)
   - Receive at warehouses
   - Allocate to stores/online
   - Ship to retail locations

4. **Retail** (2-6 months)
   - Display/market
   - Full price selling
   - Markdowns
   - Clearance

**Total Timeline:** 9-12 months traditional, 3-6 weeks fast fashion

#### How DressUp Provides Value
- Helps users maximize existing wardrobe (reduces impulse buying)
- Data shows what's missing from wardrobe (targeted shopping)
- Aggregate data reveals demand patterns (valuable to brands)

#### Depth Required
**Working Knowledge:** Understand timeline and pain points.

---

### 4.3 Inventory Management & Return Economics

#### Key Metrics

**Inventory Turnover**
- Definition: How many times inventory sells per year
- Calculation: Cost of Goods Sold / Average Inventory
- Good turnover: 4-6x for fashion
- Why it matters: Tied-up cash in unsold inventory

**Sell-Through Rate**
- Definition: % of inventory sold at full price
- Target: 70-80% before markdowns
- Reality: Often 40-60%
- Impact: Markdowns erode margin

**Return Rate**
- Definition: % of purchased items returned
- Online fashion average: 20-30%
- In-store average: 8-10%
- Cost per return: $15-30 (shipping, processing, restocking)

#### The Return Problem

**Why High Returns Hurt:**
- Shipping costs (both ways)
- Processing labor
- Items often can't be resold as new
- Tied-up inventory
- Environmental impact

**Common Return Reasons:**
- Doesn't fit (40%)
- Looks different than expected (25%)
- Doesn't match existing wardrobe (20%)
- Changed mind (15%)

**How DressUp Reduces Returns:**
- Shows how items work with existing wardrobe
- Sets realistic expectations
- Helps users make confident decisions
- "Try before you buy" virtually

#### Depth Required
**Working Knowledge:** Understand economics and DressUp's value proposition.

---

### 4.4 Fashion Business Models

#### Traditional Retail
- Buy wholesale, sell retail (2-3x markup)
- Seasonal collections
- Physical stores + online
- Challenge: Inventory risk, markdowns

#### Fast Fashion
- Rapid production cycles (3-6 weeks)
- Lower prices, lower quality
- Trend-driven
- Challenge: Sustainability, quality

#### Direct-to-Consumer (DTC)
- Brand sells directly, no wholesale
- Higher margins
- Control full experience
- Challenge: Customer acquisition cost

#### Subscription/Rental
- Rent the Runway: Rent designer items
- Stitch Fix: Curated boxes
- Challenge: Logistics, inventory management

#### Where DressUp Fits
- Not selling clothes (no inventory risk)
- Complementary to all models
- Data valuable to all fashion businesses
- Platform/marketplace potential

#### Depth Required
**Awareness Level:** Understand different models and where DressUp adds value.

---

## Learning Resources

### System Architecture Resources

**Required Reading (4 hours):**
1. "System Design Primer" on GitHub - Search: "github system design primer"
   - Read: Intro, Basic Concepts, Data Flow sections
   - Time: 1.5 hours
   
2. "Entity Relationship Diagram Tutorial" - Search: "lucidchart ERD tutorial"
   - Complete: Full tutorial with examples
   - Time: 1 hour

3. "Introduction to System Architecture" - Search: "system architecture basics software"
   - Read: First comprehensive article
   - Time: 1.5 hours

**Video Resources (2 hours):**
1. YouTube Search: "system design for beginners"
   - Watch: Top result over 100k views
   - Time: 30 minutes

2. YouTube Search: "entity relationship diagram explained"
   - Watch: Most visual/clear explanation
   - Time: 30 minutes

3. YouTube Search: "data flow diagram tutorial"
   - Watch: Practical example walkthrough
   - Time: 30 minutes

**What to Ask Claude:**
- "Show me an example entity relationship diagram for an e-commerce system"
- "Explain the difference between one-to-many and many-to-many relationships with examples"
- "Help me identify the entities for a fashion recommendation app"
- "What's the difference between logical and physical architecture?"

### Prompt Engineering Resources

**Required Reading (3 hours):**
1. OpenAI's Prompt Engineering Guide - Search: "openai prompt engineering guide"
   - Read: Entire guide
   - Time: 1 hour

2. Anthropic's Claude Prompting Guide - Search: "anthropic claude prompt engineering"
   - Read: Complete documentation
   - Time: 1 hour

3. "Few-Shot Prompting Explained" - Search: "few-shot prompting examples"
   - Read: Technical blog post with examples
   - Time: 1 hour

**Video Resources (1.5 hours):**
1. YouTube Search: "prompt engineering course 2024"
   - Watch: Most comprehensive recent course
   - Time: 1 hour

2. YouTube Search: "chain of thought prompting"
   - Watch: Technical explanation with examples
   - Time: 30 minutes

**Practice Exercises (2 hours):**
1. Write 10 prompts for outfit analysis using RTCC framework
2. Test each prompt 5 times, document variations
3. Debug and improve prompts based on results

**What to Ask Claude:**
- "Critique this prompt and suggest improvements: [your prompt]"
- "Show me how to convert this task into a well-structured prompt: [task description]"
- "What's the difference between system and user prompts with examples?"
- "Debug why this prompt gives inconsistent results: [prompt]"

### Decision Frameworks Resources

**Required Reading (2 hours):**
1. "Kano Model Explained" - Search: "kano model product management"
   - Read: Comprehensive guide with examples
   - Time: 45 minutes

2. "MoSCoW Prioritization Method" - Search: "moscow method examples"
   - Read: Practical application guide
   - Time: 30 minutes

3. "ICE Scoring Framework" - Search: "ice scoring prioritization"
   - Read: Tutorial with calculation examples
   - Time: 45 minutes

**What to Ask Claude:**
- "Help me categorize these features using the Kano model: [feature list]"
- "Show me how to apply MoSCoW to an MVP feature list"
- "Calculate ICE scores for these features: [features with estimates]"

### Agentic AI Resources

**Required Reading (30 minutes):**
1. "AI Agents vs Chatbots" - Search: "autonomous AI agents explained"
   - Understand: Multi-step reasoning
   - Time: 15 minutes

2. "ReAct Pattern in AI" - Search: "ReAct reasoning acting AI"
   - Learn: How agents think and act
   - Time: 15 minutes

**Practice Exercise (30 minutes):**
1. List 5 multi-step tasks in DressUp that could benefit from agents
2. Choose one task and break it into agent steps
3. Document in 1-page "Agentic Possibilities for DressUp"

**What to Ask Claude:**
- "Explain the difference between a single prompt and an AI agent with an example"
- "How would an AI agent approach outfit planning differently than a simple prompt?"
- "Break down 'packing for a trip' into agent steps for DressUp"
- "What makes a task suitable for an agentic approach vs single prompt?"

### Fashion Industry Resources

**Required Reading (3 hours):**
1. "Fashion Supply Chain Explained" - Search: "fashion industry supply chain"
   - Read: Industry overview article
   - Time: 1 hour

2. Business of Fashion's "Fashion Return Rates" - Search: "online fashion return rates statistics"
   - Read: Latest statistics and analysis
   - Time: 30 minutes

3. Case Studies:
   - Search: "Stitch Fix business model analysis"
   - Search: "Rent the Runway case study"
   - Search: "Thread fashion AI case study"
   - Time: 1.5 hours total

**What to Ask Claude:**
- "Explain the economics of fashion retail markdowns"
- "Why are return rates so high for online fashion?"
- "How does fast fashion differ from traditional retail cycles?"
- "What data would be valuable to fashion retailers?"

---

## Knowledge Checkpoints

### System Architecture Checkpoints

**You Must Be Able To:**
- [ ] List all entities for DressUp with their attributes
- [ ] Draw an entity-relationship diagram showing all relationships
- [ ] Explain the difference between 1:1, 1:N, and M:N relationships
- [ ] Create a data flow diagram for the morning outfit recommendation
- [ ] Identify which layer handles each DressUp function
- [ ] Document architecture decisions with clear rationale

**Practical Tests:**
1. Can you sketch DressUp's complete architecture on a whiteboard in 10 minutes?
2. Can you explain why User→WardrobeItem is one-to-many, not many-to-many?
3. Can you identify what tables you need and their relationships?
4. Can you trace data flow from weather API to outfit notification?

**Red Flags (You're Not Ready):**
- You can't explain what an entity is
- You don't understand why many-to-many needs a junction table
- You can't identify the relationships between your entities
- Your architecture diagram is just boxes with no clear connections

### Prompt Engineering Checkpoints

**You Must Be Able To:**
- [ ] Write a complete RTCC prompt for any DressUp feature
- [ ] Debug a failing prompt and fix it systematically
- [ ] Explain when to use system vs user prompts
- [ ] Create few-shot examples that improve output quality
- [ ] Set appropriate temperature for different tasks
- [ ] Organize prompts in a maintainable library structure

**Practical Tests:**
1. Can you write a prompt that consistently rates outfit compatibility?
2. Can you fix this broken prompt in <10 minutes? (Give them broken prompt)
3. Can you explain why a prompt gives different outputs each time?
4. Can you reduce a 1000-token prompt to 300 tokens without losing quality?

**Red Flags (You're Not Ready):**
- Your prompts give wildly different outputs each run
- You can't explain what's wrong with a failing prompt
- You don't know when to use examples vs instructions
- You haven't tested prompts systematically

### Decision Frameworks Checkpoints

**You Must Be Able To:**
- [ ] Classify 20 features into Kano categories in 10 minutes
- [ ] Create MoSCoW list for MVP features with clear rationale
- [ ] Calculate ICE scores and defend your ratings
- [ ] Identify friction points in user journey
- [ ] Explain feedback loops in DressUp

**Practical Tests:**
1. Given 30 feature ideas, can you identify the 5 must-haves?
2. Can you explain why "social sharing" is a Could Have, not Must Have?
3. Can you calculate ICE scores for 10 features in 5 minutes?
4. Can you identify 3 positive feedback loops in DressUp?

**Red Flags (You're Not Ready):**
- Everything feels like a "Must Have"
- You can't explain your prioritization logic
- You spend >30 minutes deciding on one feature's priority

### Fashion Industry Checkpoints

**You Must Be Able To:**
- [ ] Explain the fashion supply chain timeline
- [ ] Calculate why returns are expensive
- [ ] Identify 3 ways DressUp helps fashion retailers
- [ ] Explain seasonal inventory challenges
- [ ] Compare fast fashion vs traditional retail models

**Practical Tests:**
1. Can you explain why DressUp reduces return rates?
2. Can you identify 3 data points valuable to retailers?
3. Can you explain the fashion calendar to a non-industry person?
4. Can you calculate the cost of a 30% return rate on $1M sales?

**Red Flags (You're Not Ready):**
- You don't understand why returns matter
- You can't explain DressUp's value to retailers
- You don't see the connection between wardrobe data and supply chain

---

## Concept Dependencies

### Prerequisites (What You Should Know Before Week 1)
- Basic spreadsheet understanding (rows, columns, formulas)
- How web applications work (client, server, database - basic level)
- What APIs do (services talking to each other)

### What Week 1 Unlocks for Later Weeks

**System Architecture Unlocks:**
- Week 2: You'll implement this architecture in Glide/Sheets
- Week 3: You'll add AI components to this architecture
- Week 4: You'll add automation layers to this architecture

**Prompt Engineering Unlocks:**
- Week 2: You'll implement prompts in Glide's AI columns
- Week 3: You'll create sophisticated recommendation prompts
- Week 4-6: You'll refine prompts based on user testing

**Decision Frameworks Unlock:**
- Every week: You'll use these to make scope decisions
- Week 2: Deciding which features to build first
- Week 3: Choosing recommendation algorithm approach
- Week 6: Prioritizing user feedback

**Fashion Industry Knowledge Unlocks:**
- Week 3: Informs recommendation logic
- Week 5: Shapes business model and positioning
- Week 6: Guides case study narrative

---

## Common Learning Pitfalls

### System Architecture Pitfalls

**Pitfall 1: Over-Engineering**
- Symptom: Designing for 1M users when you have 0
- Solution: Design for 100 users, note how to scale

**Pitfall 2: Under-Documenting**
- Symptom: "I'll remember how this works"
- Solution: Document as if someone else will build it

**Pitfall 3: Analysis Paralysis**
- Symptom: 3 days designing, 0 days building
- Solution: 80% solution documented is better than 100% in your head

### Prompt Engineering Pitfalls

**Pitfall 1: Not Testing Systematically**
- Symptom: "It worked once so it's fine"
- Solution: Test 10x minimum, document variations

**Pitfall 2: Prompt Bloat**
- Symptom: 2000-token prompts for simple tasks
- Solution: Start minimal, add only what improves output

**Pitfall 3: Model Anthropomorphism**
- Symptom: "The AI understands what I mean"
- Solution: AI is pattern matching, not understanding; be explicit

### Decision Framework Pitfalls

**Pitfall 1: Everything is Must Have**
- Symptom: 20 "Must Have" features
- Solution: True Must Haves ≤5 for MVP

**Pitfall 2: Skipping Frameworks**
- Symptom: "I'll just use intuition"
- Solution: Intuition + framework = better decisions

**Pitfall 3: Over-Analyzing**
- Symptom: 2-hour ICE scoring session
- Solution: Time-box to 30 minutes max

### Fashion Industry Pitfalls

**Pitfall 1: Underestimating Complexity**
- Symptom: "Fashion is just selling clothes"
- Solution: Understand the full supply chain complexity

**Pitfall 2: Ignoring Business Reality**
- Symptom: "Retailers don't need our data"
- Solution: Understand their actual pain points (returns, inventory)

**Pitfall 3: Feature-First Thinking**
- Symptom: "Cool features will sell themselves"
- Solution: Start with industry problems, design solutions

---

## Week 1 Learning Schedule

### Day 1 (Monday): System Architecture Fundamentals
**Morning (2 hours):**
- Read: System Design Primer
- Watch: System design for beginners video
- Ask Claude: Architecture questions

**Afternoon (2 hours):**
- Create: List of DressUp entities
- Draw: First entity-relationship diagram
- Document: Why each entity exists

### Day 2 (Tuesday): Architecture Deep Dive
**Morning (2 hours):**
- Read: ERD tutorial
- Practice: Relationship types
- Refine: DressUp ERD

**Afternoon (1.5 hours):**
- Create: Data flow diagrams
- Document: Architecture decisions
- Review: With Claude for feedback

### Day 3 (Wednesday): Prompt Engineering Basics
**Morning (2 hours):**
- Read: OpenAI & Anthropic guides
- Watch: Prompt engineering course
- Practice: Write 5 RTCC prompts

**Afternoon (2 hours):**
- Test: Each prompt 10x
- Debug: Failed prompts
- Document: What works/doesn't

### Day 4 (Thursday): Advanced Prompting
**Morning (1.5 hours):**
- Learn: Few-shot prompting
- Practice: Chain-of-thought
- Create: Prompt templates

**Afternoon (1.5 hours):**
- Build: Prompt library structure
- Write: 15+ production prompts
- Test: Systematically

### Day 5 (Friday): Frameworks, Agentic AI & Industry
**Morning (2 hours):**
- Read: All framework guides
- Apply: Kano to features
- Create: MoSCoW list
- Calculate: ICE scores

**Afternoon (4 hours):**
- **Hour 1: Introduction to Agentic AI (30 min reading + 30 min documenting)**
  - Read: Agent vs single prompt concepts
  - Compare: Single prompt vs multi-step agent examples
  - Brainstorm: 5 agentic possibilities for DressUp
  - Document: 1-page "Agentic Possibilities" deliverable
- **Hours 2-4: Fashion Industry Deep Dive**
  - Read: Fashion industry articles
  - Study: Stitch Fix case
  - Analyze: Return economics
  - Document: DressUp value prop

### Weekend: Integration & Documentation
**Saturday (2 hours):**
- Review: All week's learning
- Complete: Knowledge checkpoints
- Fix: Any gaps identified

**Sunday (2 hours):**
- Create: Week 1 case study
- Finalize: All documentation
- Prepare: For Week 2

---

## Success Metrics for Week 1

By end of Week 1, you should have:

1. **Complete System Architecture**
   - ERD with all entities and relationships
   - Data flow diagrams for key processes
   - Architecture decision document
   - Clear documentation someone else could build from

2. **Production-Ready Prompt Library**
   - 15+ tested prompts using RTCC framework
   - Organized library structure
   - Testing documentation showing consistency
   - Debugging notes for common issues

3. **Prioritized Feature List**
   - Features classified in Kano model
   - MoSCoW prioritization complete
   - ICE scores for top 10 features
   - Clear MVP scope (5-7 Must Haves)

4. **Agentic AI Understanding**
   - Clear grasp of agents vs single prompts
   - 1-page "Agentic Possibilities for DressUp" document
   - 5+ multi-step agent ideas brainstormed
   - Connection to Week 3 learning understood

5. **Industry Knowledge Foundation**
   - Can explain fashion supply chain
   - Understand return economics
   - Clear value proposition for retailers
   - Competitive landscape mapped

6. **Published Case Study**
   - 1200+ word article
   - Covers architecture decisions
   - Shows prompt engineering process
   - Demonstrates framework application
   - Mentions agentic AI possibilities (preview)

---

## How to Know You're Ready for Week 2

**Green Lights (Proceed to Week 2):**
- ✅ All knowledge checkpoints passed
- ✅ Architecture fully documented
- ✅ 15+ prompts tested and working
- ✅ Clear MVP scope defined
- ✅ Understanding of fashion industry context

**Yellow Lights (Finish These First):**
- ⚠️ Architecture sketched but not documented
- ⚠️ Prompts written but not tested
- ⚠️ Rough feature prioritization done
- ⚠️ Basic industry understanding

**Red Lights (Not Ready):**
- ❌ Can't explain what entities are
- ❌ No clear data model
- ❌ Prompts giving random results
- ❌ Everything is "Must Have"
- ❌ Don't understand why DressUp matters to fashion industry

---

## INTJ-Specific Learning Optimizations

### Leverage Your Strengths
1. **Systems Thinking:** You'll grasp architecture faster than most. Spend that saved time on documentation.

2. **Pattern Recognition:** You'll see connections between concepts quickly. Document these insights—they're valuable.

3. **Strategic Planning:** You'll naturally think long-term. Channel this into architecture that scales.

### Manage Your Challenges
1. **Perfectionism:** Set timers. When timer ends, move on. Document what you'd improve in v2.

2. **Over-Abstracting:** Balance conceptual learning with practical application. For every hour of theory, do 30 minutes of practice.

3. **Analysis Paralysis:** Use frameworks as forcing functions. They give you permission to decide and move on.

4. **Impatience with Repetition:** Testing prompts 10x feels redundant but is necessary. Frame it as data collection, not repetition.

### Your Week 1 Mantra
"Architecture excellence comes from iteration, not perfection. Ship the 80% solution, document the 20% improvement."

---

## Questions to Ask Claude During Week 1

**When Stuck on Architecture:**
- "Review my entity relationship diagram for a fashion app: [your ERD]. What am I missing?"
- "I'm trying to model outfit recommendations. What entities and relationships do I need?"
- "Explain why this relationship should be many-to-many vs one-to-many: [specific example]"

**When Debugging Prompts:**
- "This prompt gives inconsistent results: [prompt]. How can I fix it?"
- "I need to extract style preferences from user feedback. Write a prompt using RTCC framework."
- "What's the optimal temperature setting for outfit compatibility scoring?"

**When Making Decisions:**
- "I have these 20 features: [list]. Help me apply MoSCoW prioritization for an MVP."
- "Calculate ICE scores for these features given these estimates: [features with data]"
- "Is [feature] a Must Have or Should Have for an MVP fashion app?"

**When Learning Industry:**
- "Explain why fashion retailers have 30% return rates online"
- "How would wardrobe data be valuable to fashion brands?"
- "What's the difference between fast fashion and traditional retail timelines?"

---

## End of Week 1 Checklist

Before moving to Week 2, ensure:

### Documentation Complete
- [ ] System architecture diagram (visual)
- [ ] Entity-relationship diagram with all attributes
- [ ] Data flow diagrams for core processes
- [ ] Architecture decision record (why you chose this design)
- [ ] Feature prioritization with rationale

### Prompts Ready
- [ ] 15+ prompts written in RTCC format
- [ ] Each prompt tested 10+ times
- [ ] Test results documented
- [ ] Prompts organized in library structure
- [ ] Version 1 tagged and saved

### Conceptual Understanding
- [ ] Can explain all Week 1 concepts without notes
- [ ] Understand how concepts connect to each other
- [ ] See clear path from architecture to implementation
- [ ] Grasp why each decision matters for DressUp

### Practical Application
- [ ] Architecture ready to implement in Week 2
- [ ] Prompts ready to use in Glide
- [ ] Features prioritized for building
- [ ] Industry knowledge informing decisions

### Published Work
- [ ] Week 1 case study written
- [ ] Published on LinkedIn/Medium
- [ ] Shared for feedback
- [ ] Link saved for portfolio

---

## Your Week 1 Success Formula

1. **Start with Why:** Every concept you learn, ask "How does this help DressUp succeed?"

2. **Document as You Go:** Don't wait until Sunday to document. Write as you learn.

3. **Test Everything:** Assumptions kill products. Test architecture logic, test prompts, test priorities.

4. **Time Box Decisions:** Set 20-minute timer for decisions. When it rings, decide and move on.

5. **Ship on Sunday:** Whatever state your work is in Sunday evening, publish the case study. Perfect is the enemy of done.

Remember: Week 1 is your foundation. It doesn't need to be perfect, but it needs to be solid. Build it well enough that Week 2 can build on top of it, not rebuild it.

You have all the conceptual ability needed. Your challenge is execution. Start Monday morning, follow the schedule, and by Sunday night you'll have a foundation that 90% of builders never achieve.

The journey from idea to implementation starts with architecture. Week 1 is where DressUp transitions from dream to blueprint.

Ready? Start with the System Design Primer. Your timer starts now.