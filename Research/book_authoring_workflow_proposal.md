# Book Authoring Workflow Proposal: Adapting TTS DevReq Framework

## Original Request

> look at the process used for /Users/alex/Dropbox/Projects/genai/TTS/ and create a proposal for adapting for the processes of book authoring, using this repo as a test case. Write your proposal to a md file under Research. Make sure that the proposed process is specifically suited to book authoring. Also use the internet to research other approaches to this, and integrate anything you find that would be of benefit into your proposal.

## Executive Summary

This proposal adapts the TTS Development Request Management Framework for collaborative book authoring, integrating insights from book sprint methodologies, academic publishing workflows, and modern documentation platforms like GitBook. The resulting system provides structured tracking for editorial requests, content changes, and review processes while maintaining the git-centric approach and LLM-friendly design of the original framework.

## Analysis of TTS Framework

### Key Components of TTS DevReq System

The TTS project uses a sophisticated request management system with these core elements:

**Core Tools:**
- `devreq` CLI tool for creating, managing, and tracking requests
- Templated markdown files for bug reports and feature requests
- Git integration with automatic commit tracking
- Structured workflow from creation → implementation → completion

**Key Features:**
- **Unique ID Generation**: BUG-YYYYMMDD-NN, FEAT-YYYYMMDD-NN format
- **Status Tracking**: OPEN → IN_PROGRESS → COMPLETED
- **Git Integration**: Automatic commit hash capture and linking
- **Template-Driven**: Consistent structured information capture
- **LLM-Optimised**: Human and machine-readable markdown format
- **File Organisation**: Clear separation between backlog and completed items

**Workflow Principles:**
- Always use git for all changes
- Commit after every task with clear conventional messages
- Update requests with commit hashes immediately
- Reference request IDs in commit messages
- Never mark complete without associated commit

## Research Findings: Book Authoring Best Practices

### Book Sprint Methodology

**Source**: Book Sprints organisation and academic literature on concurrent editorial processes

**Key Insights:**
- **Concurrent Writing and Editing**: Unlike traditional linear workflows, book sprints have simultaneous writing and editing
- **Role Specialisation**: Clear delineation between facilitators, writers, and editors
- **Rapid Iteration**: Content is refined in real-time rather than through lengthy review cycles
- **Shared Knowledge Base**: Group expertise forms the content foundation

### Academic Publishing Workflows

**Source**: Research on experimental book publishing and editorial workflows

**Key Insights:**
- **Combinatorial Editing**: Multiple editors working on different aspects simultaneously
- **Version Control Integration**: Git-based workflows increasingly common in academic publishing
- **Collaborative Platforms**: Tools like Overleaf provide real-time collaboration with academic rigour
- **Community-Led Editorial Management**: Editorial decisions distributed across expert communities

### Modern Documentation Platforms

**Source**: GitBook, technical writing platforms, and automated publishing workflows

**Key Insights:**
- **Change Request Systems**: Formal proposal and review processes similar to GitHub PRs
- **WYSIWYG + Markdown**: Dual editing modes for different user preferences
- **Review and Approval Workflows**: Structured editorial gatekeeping
- **Automated Publishing**: Integration between writing tools and publication platforms

## Proposed Framework: BookReq System

### Adaptation Philosophy

The TTS DevReq framework is adapted for book authoring by:

1. **Changing Request Types**: From bugs/features to editorial/content requests
2. **Adding Review Stages**: Multi-stage editorial review process
3. **Content-Specific Templates**: Templates designed for book authoring needs
4. **Chapter-Level Tracking**: Organisation around book structure rather than codebase files
5. **Quality Gates**: Editorial standards and approval processes

### Request Types for Book Authoring

#### 1. Content Requests (CONT-YYYYMMDD-NN)
For substantial content additions, modifications, or restructuring.

**Template Fields:**
- Content scope (chapter, section, full rewrite)
- Writing assignment or modification description
- Target word count and deadline
- Research requirements
- Integration points with existing content
- Acceptance criteria for completion

#### 2. Editorial Requests (EDIT-YYYYMMDD-NN)
For editorial review, fact-checking, style improvements, and quality assurance.

**Template Fields:**
- Editorial scope (copy-editing, developmental editing, fact-checking)
- Priority level (critical errors vs. style improvements)
- Specific chapters or sections affected
- Editorial standards to apply
- Expected review timeframe
- Dependencies on other editorial work

#### 3. Review Requests (REV-YYYYMMDD-NN)
For peer review, technical accuracy verification, and expert validation.

**Template Fields:**
- Review type (technical accuracy, peer review, sensitivity review)
- Required reviewer expertise
- Specific aspects to validate
- Review deadline
- Review criteria and standards
- Feedback format requirements

#### 4. Production Requests (PROD-YYYYMMDD-NN)
For formatting, publishing preparation, and technical publication tasks.

**Template Fields:**
- Production task type (formatting, indexing, citation checking)
- Publication target (audiobook, ebook, print)
- Technical requirements
- Dependencies on content completion
- Quality standards for output

### Enhanced CLI Tool: `bookreq`

**Adapted from TTS `devreq` with book-specific functionality:**

```bash
# Create different request types
bookreq create content    # Content writing/modification
bookreq create editorial  # Editorial review and improvement
bookreq create review     # Expert/peer review
bookreq create production # Publishing preparation

# List requests by type and status
bookreq list backlog --type=content
bookreq list review --priority=high
bookreq list completed --chapter=03

# Enhanced filtering for books
bookreq show --chapter=05 --type=editorial
bookreq assign EDIT-20250107-01 --reviewer="technical expert"

# Integration with book structure
bookreq stats --chapter=all  # Progress overview
bookreq dependencies REV-20250107-02  # Show blocking requests
```

### Directory Structure

**Adapted from TTS `.dev/` structure:**

```
.bookreq/
├── bookreq                 # Main CLI tool (adapted from devreq)
├── config/
│   ├── chapters.yml       # Chapter structure and metadata
│   ├── reviewers.yml      # Reviewer assignments and expertise
│   └── standards.yml      # Editorial and quality standards
├── templates/
│   ├── content_request.md
│   ├── editorial_request.md
│   ├── review_request.md
│   └── production_request.md
├── backlog/
│   ├── content/           # Active content requests
│   ├── editorial/         # Active editorial requests
│   ├── review/           # Active review requests
│   └── production/       # Active production requests
├── completed/
│   └── [same structure as backlog]
├── git-hooks/            # Automated git integration
└── reports/              # Progress and quality reports
```

### Workflow Integration

#### Git Integration (Enhanced from TTS)

**Conventional Commit Messages for Books:**
```bash
content: add CONT-20250107-01 - complete section 3.2 on transformer architectures
editorial: fix EDIT-20250107-02 - correct technical terminology in chapter 5
review: address REV-20250107-03 - incorporate peer feedback on reasoning models
production: complete PROD-20250107-04 - format citations for academic style
```

**Branch Strategy:**
- `main` - published/final content
- `editorial` - content under editorial review
- `chapter-XX` - individual chapter development
- `review-YYYY-MM` - review cycles

#### Quality Gates (Inspired by Academic Publishing)

**Multi-Stage Review Process:**
1. **Draft Stage**: Content creation and initial self-review
2. **Editorial Stage**: Professional editing and fact-checking
3. **Review Stage**: Expert peer review and validation
4. **Production Stage**: Formatting and publication preparation

**Automated Checks** (Enhanced from TTS git hooks):
- Word count tracking and targets
- Citation format validation
- Cross-reference consistency checking
- Style guide compliance
- Technical accuracy flags

### Template Examples

#### Content Request Template
```markdown
# Content Request

**ID**: CONT-{{YYYYMMDD}}-{{NN}}
**Created**: {{DATE}}
**Status**: OPEN
**Priority**: HIGH|MEDIUM|LOW
**Assignee**: AUTHOR|CONTRIBUTOR|AI
**Chapter**: {{CHAPTER_NUMBER}}
**Section**: {{SECTION_REFERENCE}}

## Content Scope
Brief description of content to be written or modified

## Writing Assignment
- Target word count: XXX words
- Key topics to cover:
  - Topic 1
  - Topic 2
- Integration requirements with existing content
- Research requirements and sources

## Acceptance Criteria
- [ ] Content meets word count target (±10%)
- [ ] All key topics adequately covered
- [ ] Integrates smoothly with surrounding content
- [ ] References and citations properly formatted
- [ ] Technical accuracy verified

## Dependencies
- Requires completion of: [other request IDs]
- Blocks progress on: [other request IDs]

## Notes
Any additional context, style requirements, or constraints

---
**Resolution Notes** (filled after completion):
- Writing commit: 
- Review commit: 
- Final edit commit:
- Word count achieved: 
- Resolution summary: 
```

#### Editorial Request Template
```markdown
# Editorial Request

**ID**: EDIT-{{YYYYMMDD}}-{{NN}}
**Created**: {{DATE}}
**Status**: OPEN
**Priority**: HIGH|MEDIUM|LOW
**Editor**: PROFESSIONAL|CONTRIBUTOR|AI
**Editorial Type**: DEVELOPMENTAL|COPY|TECHNICAL|STYLE

## Editorial Scope
Description of editorial work required

## Content Location
- **Chapter(s)**: XX
- **Section(s)**: X.X
- **Word count**: ~XXX words
- **Files involved**: 
  - `XX_chapter_name.md`

## Editorial Focus
- [ ] Clarity and readability
- [ ] Technical accuracy
- [ ] Style consistency
- [ ] Fact-checking
- [ ] Citation verification
- [ ] Structure and flow

## Standards to Apply
- Style guide: [British/US academic]
- Technical level: [Expert/Intermediate/General]
- Citation style: [Academic/Industry]
- TTS optimisation requirements

## Deadline
Target completion: {{DATE}}

---
**Resolution Notes** (filled after completion):
- Editorial commit: 
- Issues found: 
- Changes made: 
- Quality assessment: 
```

### Book-Specific Enhancements

#### Chapter Management Integration
- **Progress Tracking**: Word count and completion status per chapter
- **Dependency Management**: Cross-chapter references and prerequisites
- **Content Coordination**: Avoid duplication and ensure logical flow

#### Quality Assurance (Inspired by Academic Publishing)
- **Technical Accuracy**: Expert review for technical content
- **Style Consistency**: Automated and manual style checking
- **Citation Management**: Reference tracking and validation
- **TTS Optimisation**: Content review for audio narration quality

#### Stakeholder Management (From Book Sprint Methodology)
- **Role Assignment**: Clear author, editor, reviewer responsibilities
- **Review Coordination**: Manage multiple concurrent reviews
- **Expertise Matching**: Assign reviewers based on subject expertise
- **Conflict Resolution**: Editorial authority for content disputes

## Implementation Plan for This Repository

### Phase 1: Framework Setup
1. Create `.bookreq/` directory structure
2. Implement basic `bookreq` CLI tool adapted from TTS `devreq`
3. Create book-specific templates
4. Configure git hooks for automated tracking

### Phase 2: Content Request Workflow
1. Create content requests for remaining chapter improvements
2. Test editorial request workflow on existing chapters
3. Implement chapter progress tracking
4. Set up quality gates for each chapter

### Phase 3: Review Integration
1. Set up review request system for technical accuracy
2. Implement peer review coordination
3. Create production request workflow for audiobook preparation
4. Test full workflow with complete chapter revision

### Phase 4: Quality Automation
1. Implement automated word count tracking
2. Set up citation format validation
3. Create cross-reference consistency checking
4. Integrate with existing editorial guidelines

## Benefits of This Approach

### For Authors
- **Clear Task Management**: Structured approach to writing and revision
- **Progress Visibility**: Track completion status across entire book
- **Quality Assurance**: Built-in editorial review process
- **Collaboration Support**: Multiple contributors can work simultaneously

### For Editors
- **Systematic Review**: Organised approach to editorial work
- **Priority Management**: Clear prioritisation of editorial tasks
- **Quality Tracking**: Monitor editorial standards and consistency
- **Workflow Integration**: Seamless integration with author workflow

### For AI/LLM Integration
- **Structured Templates**: Machine-readable request formats
- **Git Integration**: Automatic progress tracking and version control
- **Context Preservation**: Full context available for AI assistance
- **Quality Gates**: Automated checks for common issues

## Conclusion

This proposal adapts the proven TTS DevReq framework for book authoring by incorporating best practices from book sprints, academic publishing, and modern documentation platforms. The resulting system provides structured editorial management while maintaining the git-centric, LLM-friendly approach that makes the original framework effective.

The framework is specifically designed for technical book authoring with multiple contributors, editorial review cycles, and publication in multiple formats including audiobook preparation. It balances the need for quality control with the flexibility required for creative and technical writing projects.

**References:**
- TTS Development Request Management Framework (analyzed from `/Users/alex/Dropbox/Projects/genai/TTS/.dev/`)
- Book Sprints methodology (booksprints.net)
- Academic publishing workflows (Commonplace research on experimental book publishing)
- GitBook collaborative editing model (gitbook.com documentation)
- Technical writing automation workflows (Medium articles on automated publishing)
