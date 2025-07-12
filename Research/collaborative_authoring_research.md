# Collaborative Authoring Research: Edit Requests, In-line Proposals, and Workflow Management

## Original Prompt

> investigate options for tracking edit requests, in-line edit proposals, and overall collaborative authoring process. I'm thinking stuff like wikipedia. The final process will be managed using git, but will be managed by a process we create. Write your findings to a file, create the directory "Research" and write it to a markdown file in there. Include multiple options and give a recommendation. Include this prompt in the file. If you are adapting an existing approach, then please provide references to this and state any changes you have made. Check in but don't push.

## Executive Summary

Based on research into collaborative authoring systems, this document identifies four primary models for managing edit requests and collaborative authoring workflows: the Wikipedia model, GitHub Pull Request model, Google Docs suggestion mode, and academic peer review systems. Each offers distinct advantages for different collaboration scenarios. For a git-managed book project requiring quality control and structured review, a **hybrid GitHub PR + Wiki model** is recommended.

## Option 1: Wikipedia Editorial Model

### How It Works
Wikipedia uses a combination of direct editing with editorial oversight, protected pages, and discussion pages for coordination.

**Key Features:**
- **Talk Pages**: Discussion spaces for each article where editors coordinate changes
- **Edit Requests**: Template-based system for suggesting changes to protected pages  
- **Watchlists**: Editors subscribe to changes on specific pages
- **Recent Changes**: Stream of all edits for community review
- **Protection Levels**: Different editing permissions based on page sensitivity
- **Editorial Review**: Experienced editors review changes, especially on contentious topics

**References:** 
- Wikipedia's collaborative editing process has been extensively studied in academic literature, particularly in "How Did They Build the Free Encyclopedia? A Literature Review" (ACM Digital Library, 2023)
- Wikipedia's own documentation on editing policies and procedures

### Pros
- Proven at massive scale
- Democratic and transparent
- Good for rapid iteration
- Community self-governance
- Built-in version control via MediaWiki

### Cons
- Can become chaotic without strong moderation
- Quality can vary significantly
- Edit wars possible
- No formal approval process for sensitive content

## Option 2: GitHub Pull Request Model

### How It Works
The GitHub PR model treats document edits like code changes, with formal review and approval processes.

**Key Features:**
- **Fork & Branch**: Contributors create branches for proposed changes
- **Pull Requests**: Formal proposals with diff views and discussion threads
- **Code Review**: Line-by-line commenting and approval system
- **Required Reviews**: Configurable approval requirements before merge
- **Status Checks**: Automated quality checks (lint, build, tests)
- **Draft PRs**: Work-in-progress sharing without formal review
- **Suggested Changes**: In-line edit proposals reviewers can apply directly

**References:**
- GitHub's official documentation on pull request workflows
- Widely adopted in software development for collaborative code editing

### Pros
- Structured review process
- High quality control
- Clear audit trail
- Excellent diff visualization
- Integrates perfectly with git
- Automated quality checks possible

### Cons
- Higher barrier to entry
- Slower iteration cycle
- May intimidate non-technical contributors
- Overhead for small changes

## Option 3: Google Docs Suggestion Mode

### How It Works
Real-time collaborative editing with suggestion mode for tracked changes and approval workflows.

**Key Features:**
- **Suggestion Mode**: Changes appear as proposed edits requiring approval
- **Real-time Collaboration**: Multiple simultaneous editors
- **Threaded Comments**: Context-specific discussions
- **Resolution Workflow**: Accept/reject suggestions with one click
- **Version History**: Automatic change tracking
- **Access Controls**: View/comment/edit permissions
- **@Mentions**: Direct contributor notification

**References:**
- Google Workspace documentation on collaborative editing
- Academic studies on peer editing effectiveness in online collaborative writing environments

### Pros
- Low barrier to entry
- Real-time collaboration
- Intuitive suggestion system
- Good for rapid feedback cycles
- Familiar to most users

### Cons
- Limited version control
- No branching/merging
- Vendor lock-in
- Limited automation possibilities
- Not git-integrated

## Option 4: Academic Peer Review Model

### How It Works
Formal peer review process adapted from academic publishing, with structured review cycles and editorial oversight.

**Key Features:**
- **Editorial Board**: Senior editors with final approval authority
- **Peer Review Assignments**: Formal reviewer assignment process
- **Review Templates**: Structured feedback forms
- **Revision Cycles**: Formal rounds of review and revision
- **Anonymous Review**: Optional blinded review process
- **Publication Workflow**: Formal stages from submission to publication

**References:**
- Academic publishing standards from journals like Nature, Science
- Research on "Online peer editing: effects of comments and edits on academic writing" (PMC, 2022)
- Taylor & Francis guidelines on peer review processes

### Pros
- High quality standards
- Thorough review process
- Clear editorial authority
- Proven in academic context
- Good for authoritative content

### Cons
- Very slow iteration
- High overhead
- May discourage contributions
- Complex coordination required

## Recommended Approach: Hybrid GitHub PR + Wiki Model

### Recommendation

For this book project, I recommend adapting a **hybrid approach** combining GitHub's PR model with Wikipedia's discussion and edit request features:

**Core Workflow:**
1. **Main Branch Protection**: Protect main branch requiring PR reviews
2. **Chapter Branches**: Contributors work on feature branches for substantial changes
3. **Issue-Based Edit Requests**: Use GitHub Issues as "talk pages" for coordination
4. **Tiered Review**: Different approval requirements based on change scope
5. **Editorial Board**: Designated maintainers with merge permissions

### Proposed Implementation

**File Structure:**
```
├── chapters/           # Main content
├── discussions/        # Chapter-specific discussion logs  
├── editorial/          # Editorial guidelines and templates
├── .github/
│   ├── ISSUE_TEMPLATE/
│   │   ├── edit_request.yml
│   │   ├── chapter_review.yml
│   │   └── content_discussion.yml
│   └── pull_request_template.md
```

**Change Categories:**

1. **Minor Edits** (typos, formatting): Direct commit to chapter branches, single reviewer approval
2. **Content Changes** (additions, restructuring): PR with two reviewer approval  
3. **Structural Changes** (new chapters, major reorganisation): Issue discussion first, then PR with editorial board approval

**Adapted Features from Source Models:**

**From Wikipedia:**
- Discussion-driven coordination via GitHub Issues
- Edit request templates for protected content
- Watchlist equivalent via GitHub subscriptions
- Community transparency via public repository

**From GitHub PR Model:**
- Formal review process with required approvals
- Line-by-line commenting on changes
- Status checks for quality assurance (spelling, word count, etc.)
- Draft PR support for work-in-progress

**From Google Docs:**
- Suggested changes workflow via GitHub's suggestion feature
- @mention notifications in comments
- Real-time-ish collaboration via rapid PR cycles

**From Academic Review:**
- Editorial authority for final decisions
- Structured review templates
- Quality gates before publication

### Changes Made to Source Approaches

1. **GitHub Model Adaptations:**
   - Lighter-weight review for minor changes
   - Editorial board concept borrowed from academic model
   - Discussion-first approach for major changes (from Wikipedia)

2. **Wikipedia Model Adaptations:**
   - Formal approval process rather than post-hoc review
   - Structured review templates rather than free-form discussion
   - Git-based rather than wiki-based version control

3. **Quality Automation:**
   - Automated checks for word count, spelling, and style consistency
   - Chapter cross-reference validation
   - Table of contents synchronisation checks

This hybrid approach provides structure and quality control while maintaining git integration and allowing for both rapid iteration and thorough review as appropriate to the content changes.
