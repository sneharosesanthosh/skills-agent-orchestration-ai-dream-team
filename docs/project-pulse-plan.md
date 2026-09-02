# Project Pulse Dashboard - Implementation Plan

## Summary

Build a lightweight static dashboard that displays Mona's team projects with real-time visibility into status, ownership, priority, and recent activity. The dashboard will be a self-contained web app served from the `app/` directory with HTML, CSS, and JSON data files, supported by a VS Code launch configuration for local development in Codespace. The Orchestrator will coordinate three specialized agents (Designer, Coder) using GitHub Copilot CLI to implement this in logical phases, each with clear file ownership and responsibility boundaries.

---

## Implementation Phases & Ordered Steps

### Phase 1: Foundation & Data (Steps 1–3)
Establish the project data structure and base application files.

#### Step 1: Create Project Data Structure
**Owner:** Coder  
**File:** `app/project-data.json`  
**Responsibility:**
- Define the `projects` array with sample project objects
- Each project includes: `name`, `owner`, `status`, `recentActivity`, `priority`
- Include 3–5 realistic sample projects representing active, at-risk, and completed statuses
- Ensure valid JSON syntax and structure

**Dependencies:** None (this is the foundation)  
**Parallel Work:** Can run in parallel with Step 2 (Designer research)  
**Validation:** 
- JSON validates with `jq . app/project-data.json` or similar
- All required fields present in each project object
- Sample data is realistic and representative

---

#### Step 2: Design System & Visual Guidelines
**Owner:** Designer  
**File:** None (produces design guidance and recommendations)  
**Responsibility:**
- Research and document component design (project cards, status badges, layout)
- Define color scheme, typography, and spacing system
- Create accessibility checklist (contrast ratios, focus states, semantic HTML)
- Outline responsive design approach (mobile, tablet, desktop)
- Produce design specifications document for Coder reference
- Recommend information hierarchy for project cards

**Dependencies:** Review of project-pulse-brief.md requirements  
**Parallel Work:** Runs in parallel with Step 1 (Coder data structure)  
**Validation:**
- Design specs include all required visual elements
- Accessibility guidelines are documented
- Coder receives clear component specifications

---

#### Step 3: VS Code Launch Configuration
**Owner:** Coder  
**File:** `.vscode/launch.json`  
**Responsibility:**
- Create or update `.vscode/launch.json` with a **"Run Project Pulse Dashboard"** configuration
- Configure to serve the `app/` directory with a local HTTP server (e.g., Python's `http.server` or similar)
- Set the server to open `index.html` on launch
- Port: use a standard development port (e.g., 5500 or 8000)
- Ensure configuration works in Codespace environment

**Dependencies:** None (can run in parallel)  
**Parallel Work:** Runs in parallel with Steps 1–2  
**Validation:**
- Launch configuration is valid JSON
- Configuration points to correct directory and file
- Can be tested locally or in Codespace

---

### Phase 2: HTML & Layout (Steps 4–5)
Create the application structure and semantic markup.

#### Step 4: HTML Markup & Page Structure
**Owner:** Coder  
**File:** `app/index.html`  
**Responsibility:**
- Create semantic HTML with proper heading hierarchy
- Build responsive layout container (header, main content, footer optional)
- Create project card template structure (will be populated by JavaScript)
- Include placeholders for status badges, owner information, and recent activity
- Link to CSS file (`styles.css`) and JSON data file (`project-data.json`)
- Include JavaScript that:
  - Loads `project-data.json` on page load
  - Iterates over projects array and renders cards
  - Populates dynamic content (name, owner, status, activity, priority)
- Ensure valid HTML5 semantics

**Dependencies:** Step 1 (project data structure defined), Step 2 (design specifications)  
**Parallel Work:** Runs in sequence after data structure and design are complete  
**Validation:**
- HTML validates (W3C or similar)
- Data loads from `project-data.json` without errors
- All projects render as expected
- JavaScript console has no errors

---

#### Step 5: CSS Styling & Responsive Design
**Owner:** Designer + Coder collaboration  
**File:** `app/styles.css`  
**Responsibility:**
- **Designer role:** Provide design tokens, spacing guidance, color values, typography specs
- **Coder role:** Implement CSS based on design specs
- Build responsive layout (mobile-first approach)
- Style project cards with clear visual hierarchy
- Style status badges with semantic color coding (e.g., green=active, yellow=at-risk, gray=completed)
- Implement focus states for keyboard navigation
- Ensure sufficient color contrast (WCAG AA minimum)
- Add hover/active states for interactive elements
- Include utility classes if needed for consistent spacing and alignment

**Dependencies:** Step 4 (HTML structure defined), Step 2 (design guidelines)  
**Parallel Work:** Runs after HTML structure is ready  
**Validation:**
- Layout is responsive and functional on mobile, tablet, and desktop
- All elements meet accessibility contrast requirements
- No layout shift or overflow issues
- Dashboard opens without CSS errors in browser DevTools

---

### Phase 3: Integration & Polish (Steps 6–7)
Finalize and validate the complete dashboard.

#### Step 6: Data Integration & JavaScript Functionality
**Owner:** Coder  
**File:** `app/index.html` (update JavaScript section)  
**Responsibility:**
- Implement robust error handling for JSON loading
- Add filtering or sorting features if time permits (e.g., by status, priority, owner)
- Ensure no console errors or warnings
- Test with sample data
- Optimize for performance (minimal reflows, efficient DOM updates)
- Add comments to JavaScript for maintainability

**Dependencies:** Steps 1, 4 (data and HTML structure)  
**Parallel Work:** Runs after Steps 4–5 complete  
**Validation:**
- All projects load and render correctly
- No JavaScript errors in console
- Dashboard handles data updates gracefully
- Performance is acceptable (no lag on card rendering)

---

#### Step 7: Accessibility & Cross-Browser Testing
**Owner:** Designer + Coder collaboration  
**File:** All dashboard files  
**Responsibility:**
- **Designer:** Review visual accessibility (colors, contrast, readability)
- **Coder:** Test keyboard navigation (Tab, arrow keys, Enter), screen reader compatibility, and focus order
- Verify all interactive elements are keyboard accessible
- Test on multiple browsers (Chrome, Firefox, Safari if available)
- Ensure launch configuration works reliably in Codespace
- Perform final visual and functional review

**Dependencies:** Steps 4–6 (all implementation complete)  
**Parallel Work:** Final validation step (not parallelizable)  
**Validation:**
- Keyboard navigation works without mouse
- Focus indicators are visible
- Screen reader announces cards and interactive elements
- Dashboard renders correctly on Chrome and Firefox
- Launch configuration opens dashboard without manual intervention

---

## File Ownership Summary

| File | Owner | Responsibility |
|------|-------|-----------------|
| `app/project-data.json` | Coder | Sample project data structure and content |
| `app/index.html` | Coder | Semantic markup, page structure, JavaScript for rendering |
| `app/styles.css` | Designer + Coder | Layout, typography, colors, responsive design, accessibility |
| `.vscode/launch.json` | Coder | VS Code launch configuration for local development |

---

## Dependencies Between Steps

```
Step 2 (Design System)
       ↓
Step 1 (Project Data) → Step 4 (HTML Markup) → Step 6 (Data Integration)
       ↓
Step 3 (Launch Config)  → Step 5 (CSS Styling) → Step 7 (Accessibility)
```

**Critical Path:**
1. Steps 1–3 can begin in parallel
2. Steps 4–5 must wait for Steps 1–2
3. Step 6 must wait for Steps 4–5
4. Step 7 must wait for Steps 4–6

---

## Parallel Work Opportunities

1. **Phase 1 (Parallel):**
   - Step 1 (Coder: Data structure) + Step 2 (Designer: Design specs) + Step 3 (Coder: Launch config)
   - These three can run concurrently; no dependencies between them

2. **Phase 2 (Sequential, but Designer can start design specs earlier):**
   - Step 4 (HTML) and Step 5 (CSS) can partially overlap if Designer produces specs before HTML is complete

3. **Orchestrator Role in Parallel Execution:**
   - The Orchestrator will use GitHub Copilot CLI to coordinate these agents
   - Orchestrator launches Steps 1, 2, 3 in parallel (as separate agent tasks)
   - Orchestrator waits for Phase 1 to complete, then launches Phase 2
   - Orchestrator provides status updates and facilitates communication between Designer and Coder

---

## Sequential Work Requirements

1. **Data structure must precede HTML rendering** (Step 1 → Step 4)
   - HTML JavaScript needs to know the data schema to render correctly

2. **HTML structure must precede styling** (Step 4 → Step 5)
   - CSS targets HTML elements; elements must exist first

3. **All implementation must precede accessibility testing** (Steps 1–6 → Step 7)
   - Final validation requires complete, working dashboard

4. **Launch configuration can be tested anytime after creation** (Step 3 standalone)
   - Independent of dashboard content; can validate earlier

---

## Edge Cases & Risk Areas

1. **JSON Loading Failures:**
   - Handle cases where `project-data.json` is missing or malformed
   - Provide fallback or error message instead of blank page

2. **No Projects in Data:**
   - Handle empty `projects` array gracefully (show "No projects" message)

3. **Missing or Incomplete Project Fields:**
   - Validate each project object has required fields
   - Provide default values or skip incomplete entries

4. **Responsive Design Edge Cases:**
   - Very long project names or owner names should truncate or wrap gracefully
   - Very long activity descriptions should be truncated with ellipsis
   - Very narrow screens (< 320px) should still be usable

5. **Launch Configuration in Different Environments:**
   - Ensure port is available or auto-select alternative port
   - Handle cases where `http.server` is not available (provide fallback instructions)

6. **Accessibility Edge Cases:**
   - Ensure status badges have semantic meaning (not just color)
   - Focus order should match visual layout
   - Touch targets should be at least 44×44px for mobile

---

## Validation Expectations

### Per-Step Validation:

**Step 1:** `project-data.json` is valid JSON with sample projects  
**Step 2:** Design specifications document is complete and reviewed by Coder  
**Step 3:** `.vscode/launch.json` is valid and correctly configured  
**Step 4:** HTML renders without errors; projects load from JSON  
**Step 5:** CSS applied correctly; layout is responsive  
**Step 6:** All projects render; no JavaScript errors; performance acceptable  
**Step 7:** Keyboard navigation works; accessibility standards met  

### Final Validation Checklist:

- [ ] Dashboard opens in browser via VS Code launch configuration
- [ ] All projects from `project-data.json` render as cards
- [ ] Visual design matches Designer specifications
- [ ] Responsive layout works on mobile, tablet, desktop
- [ ] Keyboard navigation (Tab, arrow keys) works without mouse
- [ ] Focus indicators are visible
- [ ] Status badges have semantic color coding
- [ ] Recent activity and owner information are clearly displayed
- [ ] No console errors or warnings
- [ ] No layout shift or reflow issues
- [ ] Performance is acceptable (no noticeable lag)
- [ ] Dashboard works in Codespace environment

---

## Open Questions

1. **Project Status Enum:**
   - What are the valid status values? (e.g., "active", "at-risk", "completed", "blocked")
   - Should the CSS include predefined colors for each status?

2. **Recent Activity Format:**
   - How should "recent activity" be formatted? (e.g., timestamp, description, both?)
   - Should it include author/contributor name?

3. **Priority Levels:**
   - What are the valid priority values? (e.g., "high", "medium", "low", numeric scale?)
   - Should priority be displayed as text, icon, or both?

4. **Sorting/Filtering:**
   - Should the initial MVP include sorting by status, priority, or owner?
   - Should users be able to filter projects (e.g., by status)?
   - These features could extend beyond the basic plan if needed

5. **Project Count:**
   - How many sample projects should the test data include? (3–5 recommended)
   - Should production data be pulled from an external API, or is static JSON sufficient?

6. **Branding/Logo:**
   - Should the dashboard include a team logo, project logo, or branding?
   - Any specific color palette to follow?

7. **Footer/Links:**
   - Should the dashboard include links to team documentation, repo, or other resources?
   - Should there be a "Last Updated" timestamp?

8. **Local Development:**
   - Should developers be able to edit `project-data.json` directly for local testing?
   - Or will data be populated from a CI/CD process?

---

## Orchestrator Coordination Notes

The **Orchestrator** will use **GitHub Copilot CLI** to coordinate this work:

1. **Launch Phase 1 Agents (Parallel):**
   ```
   copilot task --agent Coder --name "Create Project Data" --prompt "..."
   copilot task --agent Designer --name "Design System" --prompt "..."
   copilot task --agent Coder --name "Configure Launch" --prompt "..."
   ```

2. **Monitor Completion:**
   - Orchestrator waits for all Phase 1 tasks to complete
   - Reviews outputs and addresses any blockers

3. **Launch Phase 2 (Sequential):**
   - Once Phase 1 complete, launch Coder for HTML
   - Once HTML is ready, launch Designer and Coder for CSS

4. **Launch Phase 3 (Final):**
   - Once Phases 1–2 complete, launch final integration and accessibility review

5. **Communicate Status:**
   - Orchestrator provides status updates to all agents
   - Shares outputs from each phase to inform next steps
   - Facilitates Designer-Coder collaboration on shared responsibilities (CSS, accessibility)

---

## Summary of Responsibilities

### Designer Responsibilities:
- Define visual design, color scheme, typography, and spacing
- Create accessibility guidelines and component specifications
- Provide CSS design tokens and styling guidance
- Collaborate with Coder on responsive design and accessibility testing
- Review final dashboard against design specifications

### Coder Responsibilities:
- Create `app/project-data.json` with sample data
- Build `app/index.html` with semantic markup and JavaScript
- Implement `app/styles.css` based on Designer specifications
- Create `.vscode/launch.json` for local development
- Implement data loading, error handling, and JavaScript functionality
- Conduct JavaScript and performance testing
- Collaborate with Designer on accessibility testing

### Orchestrator Responsibilities (GitHub Copilot CLI):
- Coordinate agent launches and task sequencing
- Ensure file ownership is clear to prevent conflicts
- Facilitate communication between Designer and Coder
- Monitor progress and address blockers
- Trigger Phase transitions when prerequisites are met
- Consolidate outputs and guide final validation

---

## Notes for Implementation

- **GitHub Copilot CLI in Codespace:** The learner will use Copilot CLI to launch agents and orchestrate the workflow, practicing agent coordination without doing all work in a single monolithic prompt.
- **Static First:** This is a static dashboard; no database or backend API in the initial MVP.
- **Minimal Dependencies:** Use vanilla JavaScript; avoid heavy frameworks to keep the bundle small and the development fast.
- **Incremental Delivery:** Each phase delivers a working increment; phases can be validated and adjusted before proceeding.
