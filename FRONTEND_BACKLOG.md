# Ocean Frontend - Development Backlog

**Project**: Ocean Frontend (Next.js 15 + TypeScript + shadcn/ui)
**Repository**: `ainative-studio/ocean-frontend`
**Sprint Duration**: 1 week sprints
**Total Estimate**: 2-3 weeks (3 sprints)

---

## Sprint 1: Foundation & Layout (Week 1)

### Epic 1.1: Project Setup & Infrastructure
**Story Points**: 5 points

#### Issue #1: Initialize Next.js 15 project with TypeScript
**Type**: Setup
**Priority**: Critical
**Estimate**: 2 points

**Description**:
Set up Next.js 15 project with TypeScript, Tailwind CSS, and essential configuration.

**Tasks**:
- [ ] Initialize Next.js 15 with App Router
- [ ] Configure TypeScript (tsconfig.json)
- [ ] Set up Tailwind CSS + PostCSS
- [ ] Install shadcn/ui CLI and dependencies
- [ ] Configure path aliases (@/components, @/lib)
- [ ] Set up ESLint + Prettier
- [ ] Create base folder structure

**Acceptance Criteria**:
- [ ] `npm run dev` starts successfully
- [ ] TypeScript compilation works without errors
- [ ] Tailwind CSS compiles correctly
- [ ] shadcn/ui components can be added

**Commands**:
```bash
npx create-next-app@latest ocean-frontend --typescript --tailwind --app
npx shadcn@latest init
```

---

#### Issue #2: Set up authentication with NextAuth.js v5
**Type**: Authentication
**Priority**: Critical
**Estimate**: 3 points

**Description**:
Integrate NextAuth.js v5 with AINative backend JWT authentication.

**Tasks**:
- [ ] Install NextAuth.js v5
- [ ] Create auth API route handler
- [ ] Configure Credentials provider
- [ ] Implement JWT callback for backend integration
- [ ] Create login page (`/login`)
- [ ] Create signup page (`/signup`)
- [ ] Add session provider to root layout
- [ ] Create auth middleware for protected routes

**Acceptance Criteria**:
- [ ] Users can log in with email/password
- [ ] JWT token stored in session
- [ ] Protected routes redirect to login
- [ ] Session persists across refreshes

**Files**:
- `app/api/auth/[...nextauth]/route.ts`
- `app/(auth)/login/page.tsx`
- `middleware.ts`

---

#### Issue #3: Create workspace layout with sidebar
**Type**: UI/Layout
**Priority**: High
**Estimate**: 3 points

**Description**:
Build main workspace layout with collapsible sidebar and top navigation.

**Tasks**:
- [ ] Create WorkspaceLayout component
- [ ] Create Sidebar component with sections
- [ ] Create TopNav component
- [ ] Add responsive behavior (collapsible on mobile)
- [ ] Implement sidebar state persistence (localStorage)
- [ ] Add keyboard shortcut to toggle sidebar (Cmd+\\)

**Acceptance Criteria**:
- [ ] Sidebar shows on desktop, collapsible
- [ ] Top nav displays user info and search
- [ ] Layout responsive on tablet (768px+)
- [ ] Sidebar state persists across sessions

**Components**:
- `components/layout/WorkspaceLayout.tsx`
- `components/sidebar/Sidebar.tsx`
- `components/layout/TopNav.tsx`

---

### Epic 1.2: Page Tree & Navigation
**Story Points**: 8 points

#### Issue #4: Implement page tree in sidebar
**Type**: Feature
**Priority**: High
**Estimate**: 5 points

**Description**:
Create hierarchical page tree with drag-and-drop, collapsible nodes, and inline actions.

**Tasks**:
- [ ] Create PageTree component
- [ ] Create PageTreeItem component
- [ ] Implement collapsible tree nodes
- [ ] Add drag-and-drop reordering (dnd-kit)
- [ ] Add hover actions (favorite, archive, more)
- [ ] Implement inline rename (click to edit)
- [ ] Add keyboard navigation (arrow keys)
- [ ] Fetch pages from API on mount

**Acceptance Criteria**:
- [ ] Pages display in hierarchical tree
- [ ] Can expand/collapse parent pages
- [ ] Drag-and-drop changes page parent
- [ ] Inline rename updates page title
- [ ] Keyboard navigation works

**Dependencies**:
```bash
npm install @dnd-kit/core @dnd-kit/sortable
```

---

#### Issue #5: Implement TanStack Query for data fetching
**Type**: Infrastructure
**Priority**: High
**Estimate**: 3 points

**Description**:
Set up TanStack Query (React Query v5) for server state management with optimistic updates.

**Tasks**:
- [ ] Install @tanstack/react-query
- [ ] Create QueryClient provider
- [ ] Create API client (`lib/api/client.ts`)
- [ ] Create custom hooks for pages (`hooks/usePages.ts`)
- [ ] Create custom hooks for blocks (`hooks/useBlocks.ts`)
- [ ] Implement optimistic updates for mutations
- [ ] Add error handling and retry logic

**Acceptance Criteria**:
- [ ] QueryClient configured in root layout
- [ ] All API calls use React Query hooks
- [ ] Optimistic updates provide instant feedback
- [ ] Errors handled gracefully with toast notifications

**Hooks**:
- `usePages()`, `useCreatePage()`, `useUpdatePage()`, `useDeletePage()`
- `useBlocks()`, `useCreateBlock()`, `useUpdateBlock()`, `useDeleteBlock()`

---

#### Issue #6: Create page header component
**Type**: UI Component
**Priority**: Medium
**Estimate**: 2 points

**Description**:
Build page header with editable title, breadcrumb, metadata, and actions.

**Tasks**:
- [ ] Create PageHeader component
- [ ] Add editable title (inline editing)
- [ ] Add breadcrumb navigation
- [ ] Add metadata display (last edited, author)
- [ ] Add action buttons (add icon, add cover, share)
- [ ] Implement auto-save on title change

**Acceptance Criteria**:
- [ ] Title editable on click
- [ ] Breadcrumb shows page hierarchy
- [ ] Metadata displays correctly
- [ ] Auto-save works with 500ms debounce

---

## Sprint 2: Block Editor & Search (Week 2)

### Epic 2.1: Block Editor Implementation
**Story Points**: 13 points

#### Issue #7: Set up Tiptap editor with custom nodes
**Type**: Editor
**Priority**: Critical
**Estimate**: 5 points

**Description**:
Initialize Tiptap editor with custom block nodes and basic configuration.

**Tasks**:
- [ ] Install Tiptap packages
- [ ] Create BlockEditor component
- [ ] Configure Tiptap with StarterKit extension
- [ ] Create custom TaskNode extension
- [ ] Create custom PageLinkNode extension
- [ ] Add markdown shortcuts
- [ ] Configure placeholder text

**Acceptance Criteria**:
- [ ] Tiptap editor renders correctly
- [ ] Markdown shortcuts work (**bold**, *italic*, etc.)
- [ ] Custom nodes render properly
- [ ] Editor has placeholder text

**Dependencies**:
```bash
npm install @tiptap/react @tiptap/starter-kit @tiptap/extension-placeholder
```

---

#### Issue #8: Implement all 6 block types
**Type**: Feature
**Priority**: Critical
**Estimate**: 8 points

**Description**:
Create React components for all 6 block types with full editing capabilities.

**Tasks**:
- [ ] Create TextBlock component
- [ ] Create HeadingBlock component (H1, H2, H3)
- [ ] Create ListBlock component (bullet + numbered)
- [ ] Create TaskBlock component (checkbox + text)
- [ ] Create LinkBlock component (URL + title)
- [ ] Create PageLinkBlock component (page selector)
- [ ] Add block type conversion menu
- [ ] Implement block dragging (reorder)

**Acceptance Criteria**:
- [ ] All 6 block types functional
- [ ] Can convert between block types
- [ ] Drag-and-drop reordering works
- [ ] All blocks save correctly to API

**Components**:
- `components/editor/blocks/TextBlock.tsx`
- `components/editor/blocks/HeadingBlock.tsx`
- `components/editor/blocks/ListBlock.tsx`
- `components/editor/blocks/TaskBlock.tsx`
- `components/editor/blocks/LinkBlock.tsx`
- `components/editor/blocks/PageLinkBlock.tsx`

---

#### Issue #9: Implement slash command menu
**Type**: Feature
**Priority**: High
**Estimate**: 3 points

**Description**:
Create slash command menu (/) for quick block creation.

**Tasks**:
- [ ] Create SlashCommandMenu component
- [ ] Detect `/` key press in editor
- [ ] Show command menu with block types
- [ ] Implement fuzzy search filtering
- [ ] Add keyboard navigation (up/down/enter)
- [ ] Convert current block on selection

**Acceptance Criteria**:
- [ ] Typing `/` shows command menu
- [ ] Can filter commands by typing
- [ ] Keyboard navigation works
- [ ] Selecting command creates block

**Commands**:
```
/text, /h1, /h2, /h3, /list, /task, /link, /page
```

---

#### Issue #10: Implement keyboard shortcuts
**Type**: Feature
**Priority**: High
**Estimate**: 3 points

**Description**:
Add comprehensive keyboard shortcuts for editor actions.

**Tasks**:
- [ ] Implement Ctrl+B (bold)
- [ ] Implement Ctrl+I (italic)
- [ ] Implement Ctrl+K (link)
- [ ] Implement Ctrl+/ (show slash menu)
- [ ] Implement Ctrl+D (duplicate block)
- [ ] Implement Ctrl+Shift+X (toggle task)
- [ ] Implement Ctrl+Up/Down (move block)
- [ ] Implement Tab/Shift+Tab (indent/unindent)
- [ ] Add keyboard shortcut help modal (Ctrl+Shift+?)

**Acceptance Criteria**:
- [ ] All shortcuts work as expected
- [ ] Shortcuts documented in help modal
- [ ] No conflicts with browser shortcuts

---

### Epic 2.2: Search Functionality
**Story Points**: 5 points

#### Issue #11: Implement global search (Cmd+K)
**Type**: Feature
**Priority**: High
**Estimate**: 5 points

**Description**:
Create global search modal with semantic search integration.

**Tasks**:
- [ ] Install cmdk package
- [ ] Create GlobalSearch component
- [ ] Implement Cmd+K trigger
- [ ] Add search input with debouncing (300ms)
- [ ] Integrate with backend search API
- [ ] Display results with highlighting
- [ ] Add recent searches section
- [ ] Add keyboard navigation
- [ ] Show block type icons in results

**Acceptance Criteria**:
- [ ] Cmd+K opens search modal
- [ ] Search updates as user types (debounced)
- [ ] Results ranked by relevance
- [ ] Clicking result navigates to page
- [ ] Recent searches displayed

**Dependencies**:
```bash
npm install cmdk
```

---

#### Issue #12: Implement search filters
**Type**: Feature
**Priority**: Medium
**Estimate**: 2 points

**Description**:
Add filtering options to search (block type, tags, date).

**Tasks**:
- [ ] Add filter UI to search modal
- [ ] Implement block type filter
- [ ] Implement tag filter
- [ ] Implement date range filter
- [ ] Update search API calls with filters
- [ ] Show active filters in UI

**Acceptance Criteria**:
- [ ] Can filter by block type
- [ ] Can filter by tags
- [ ] Can filter by date range
- [ ] Active filters displayed

---

## Sprint 3: Linking, Tags & Polish (Week 3)

### Epic 3.1: Linking & Backlinks
**Story Points**: 5 points

#### Issue #13: Implement page linking with @ trigger
**Type**: Feature
**Priority**: High
**Estimate**: 3 points

**Description**:
Create page link creation with @ or [[ trigger and page selector.

**Tasks**:
- [ ] Detect @ or [[ input in editor
- [ ] Show page selector dropdown
- [ ] Implement fuzzy search for pages
- [ ] Create page link on selection
- [ ] Store link in backend
- [ ] Render page link block with icon

**Acceptance Criteria**:
- [ ] @ or [[ triggers page selector
- [ ] Can search and select pages
- [ ] Link created successfully
- [ ] Link displays page title and icon

---

#### Issue #14: Implement backlinks panel
**Type**: Feature
**Priority**: Medium
**Estimate**: 2 points

**Description**:
Create expandable backlinks panel showing pages/blocks linking to current page.

**Tasks**:
- [ ] Create BacklinksPanel component
- [ ] Fetch backlinks from API
- [ ] Display backlinks with context preview
- [ ] Make backlinks clickable (navigate)
- [ ] Add expand/collapse toggle

**Acceptance Criteria**:
- [ ] Backlinks panel displays correctly
- [ ] Shows all incoming links
- [ ] Context preview shown
- [ ] Clicking navigates to source

---

### Epic 3.2: Tag Management
**Story Points**: 3 points

#### Issue #15: Implement tag creation and assignment
**Type**: Feature
**Priority**: Medium
**Estimate**: 2 points

**Description**:
Create tag input with # trigger and tag management.

**Tasks**:
- [ ] Detect # input in editor
- [ ] Show tag autocomplete dropdown
- [ ] Create new tags inline
- [ ] Assign tags to blocks
- [ ] Display tags with colors
- [ ] Store tags in backend

**Acceptance Criteria**:
- [ ] # triggers tag autocomplete
- [ ] Can create new tags
- [ ] Tags assigned to blocks
- [ ] Tags display with colors

---

#### Issue #16: Implement tag filtering and management
**Type**: Feature
**Priority**: Low
**Estimate**: 1 point

**Description**:
Add tag filtering page and tag settings.

**Tasks**:
- [ ] Create tags settings page
- [ ] Allow tag color editing
- [ ] Allow tag deletion
- [ ] Show tag usage count
- [ ] Add filter by tag feature

**Acceptance Criteria**:
- [ ] Can edit tag colors
- [ ] Can delete unused tags
- [ ] Tag usage count shown

---

### Epic 3.3: Polish & Performance
**Story Points**: 8 points

#### Issue #17: Implement optimistic UI updates
**Type**: Performance
**Priority**: High
**Estimate**: 3 points

**Description**:
Add optimistic updates for instant feedback on all mutations.

**Tasks**:
- [ ] Implement optimistic create page
- [ ] Implement optimistic create block
- [ ] Implement optimistic update block
- [ ] Implement optimistic delete block
- [ ] Add rollback on error
- [ ] Show loading states

**Acceptance Criteria**:
- [ ] All create actions instant
- [ ] UI updates before API response
- [ ] Rollback on error works

---

#### Issue #18: Add loading skeletons and transitions
**Type**: UI/UX
**Priority**: Medium
**Estimate**: 2 points

**Description**:
Create loading skeletons and smooth transitions for better UX.

**Tasks**:
- [ ] Create PageSkeleton component
- [ ] Create BlockSkeleton component
- [ ] Add loading states to sidebar
- [ ] Add Framer Motion transitions
- [ ] Add toast notifications for errors

**Acceptance Criteria**:
- [ ] Skeletons show while loading
- [ ] Transitions smooth and subtle
- [ ] Errors show toast notifications

**Dependencies**:
```bash
npm install framer-motion sonner
```

---

#### Issue #19: Optimize bundle size and performance
**Type**: Performance
**Priority**: High
**Estimate**: 3 points

**Description**:
Optimize Next.js bundle for fast load times and small size.

**Tasks**:
- [ ] Implement code splitting for editor
- [ ] Lazy load heavy components
- [ ] Optimize images with next/image
- [ ] Optimize fonts with next/font
- [ ] Run Lighthouse audit
- [ ] Fix performance issues
- [ ] Achieve <100KB JS bundle

**Acceptance Criteria**:
- [ ] Initial bundle <100KB
- [ ] Lighthouse score >90
- [ ] FCP <1s
- [ ] TTI <2s

---

#### Issue #20: Implement responsive design for tablets
**Type**: UI/UX
**Priority**: Medium
**Estimate**: 2 points

**Description**:
Ensure Ocean works well on tablets (768px-1024px).

**Tasks**:
- [ ] Test on iPad (1024px width)
- [ ] Adjust sidebar for tablet
- [ ] Optimize touch targets (min 44x44px)
- [ ] Test editor on touch devices
- [ ] Fix any layout issues

**Acceptance Criteria**:
- [ ] Works on tablets (768px+)
- [ ] Touch targets appropriately sized
- [ ] Editor usable with touch

---

### Epic 3.4: Testing & Deployment
**Story Points**: 5 points

#### Issue #21: Write component tests with Vitest
**Type**: Testing
**Priority**: High
**Estimate**: 3 points

**Description**:
Create comprehensive test suite for components.

**Tasks**:
- [ ] Set up Vitest and Testing Library
- [ ] Write tests for block components
- [ ] Write tests for sidebar components
- [ ] Write tests for search components
- [ ] Achieve 70%+ test coverage

**Acceptance Criteria**:
- [ ] Test coverage >= 70%
- [ ] All tests pass
- [ ] CI runs tests on PR

**Dependencies**:
```bash
npm install -D vitest @testing-library/react @testing-library/jest-dom
```

---

#### Issue #22: Deploy to Vercel
**Type**: DevOps
**Priority**: Critical
**Estimate**: 2 points

**Description**:
Deploy Ocean frontend to Vercel with production configuration.

**Tasks**:
- [ ] Create Vercel project
- [ ] Configure environment variables
- [ ] Set up GitHub integration
- [ ] Deploy to production
- [ ] Test production deployment
- [ ] Set up custom domain (ocean.ainative.studio)

**Acceptance Criteria**:
- [ ] Deployed successfully
- [ ] All features work in production
- [ ] Custom domain configured
- [ ] HTTPS enabled

---

#### Issue #23: Accessibility audit and fixes
**Type**: Accessibility
**Priority**: High
**Estimate**: 2 points

**Description**:
Ensure WCAG 2.1 AA compliance.

**Tasks**:
- [ ] Run axe DevTools audit
- [ ] Fix keyboard navigation issues
- [ ] Add ARIA labels
- [ ] Test with screen reader
- [ ] Fix color contrast issues
- [ ] Test focus management

**Acceptance Criteria**:
- [ ] axe audit passes with 0 violations
- [ ] Keyboard navigation works everywhere
- [ ] Screen reader compatible
- [ ] Color contrast meets AA standard

---

## Summary

### Total Story Points: 44 points
- **Sprint 1** (Week 1): 13 points - Foundation & Layout
- **Sprint 2** (Week 2): 18 points - Block Editor & Search
- **Sprint 3** (Week 3): 13 points - Linking, Tags, Polish

### Team Capacity
- **2 frontend developers**: ~20-25 points/week
- **Timeline**: 2-3 weeks for MVP

### Critical Path
1. Project setup (Issues #1-2)
2. Workspace layout (Issue #3)
3. Page tree (Issue #4)
4. Block editor (Issues #7-8)
5. Search (Issue #11)
6. Testing & deployment (Issues #21-22)

---

## Issue Labels

- `setup` - Initial project setup
- `feature` - New feature implementation
- `ui` - UI component development
- `editor` - Editor-related work
- `authentication` - Auth functionality
- `testing` - Test development
- `performance` - Performance optimization
- `accessibility` - Accessibility improvements
- `devops` - Deployment & CI/CD
- `critical` - Must-have for MVP
- `high` - Important but not blocking
- `medium` - Nice to have
- `low` - Can defer to post-MVP

---

## Dependencies

```
Issue #1 → All other issues (project setup)
Issue #2 → All protected routes (authentication)
Issue #3 → Issue #4 (layout before page tree)
Issue #5 → All API calls (React Query setup)
Issue #7 → Issue #8-10 (Tiptap before blocks)
Issue #21 → Issue #22 (tests before deploy)
```

---

**Ready to create GitHub issues!**
