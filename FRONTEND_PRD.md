# Ocean Frontend - Product Requirements Document

**Project**: Ocean Frontend (Next.js 15 + TypeScript + shadcn/ui)
**Repository**: `ainative-studio/ocean-frontend`
**Version**: 1.0 (MVP)
**Last Updated**: December 23, 2025

---

## 1. Overview

Ocean Frontend is a **modern, block-based workspace interface** built with Next.js 15, providing an intuitive UI for creating, organizing, and searching knowledge using a Notion-like editor experience.

### Tech Stack
- **Framework**: Next.js 15 (App Router, React Server Components)
- **Language**: TypeScript 5.8+
- **UI Library**: shadcn/ui + Radix UI + Tailwind CSS
- **Editor**: Tiptap (extensible rich-text editor)
- **State Management**: TanStack Query (React Query v5)
- **Authentication**: NextAuth.js v5 (JWT integration with AINative backend)
- **Deployment**: Vercel (SSG + ISR)

---

## 2. Design Principles

1. **Keyboard-First**: Every action accessible via keyboard shortcuts
2. **Instant Feedback**: Optimistic UI updates, real-time feel
3. **Progressive Enhancement**: Works without JS, enhanced with JS
4. **Accessible by Default**: WCAG 2.1 AA compliance
5. **Mobile-Responsive**: Desktop-first, but works on tablets
6. **Fast & Lightweight**: <100KB initial JS bundle

---

## 3. User Interface Structure

### 3.1 Layout

```
┌─────────────────────────────────────────────────────┐
│                    Top Navigation                    │
│  [Logo] [Search] [Create Page]      [User] [Settings]│
├───────────────┬──────────────────────────────────────┤
│               │                                       │
│   Sidebar     │         Main Content Area            │
│               │                                       │
│ • All Pages   │    ┌──────────────────────────┐     │
│ • Favorites   │    │   Page Title (editable)  │     │
│ • Recent      │    ├──────────────────────────┤     │
│ • Archived    │    │                          │     │
│               │    │   Block 1 (text)        │     │
│ • Page Tree   │    │   Block 2 (heading)     │     │
│   ├─ Project  │    │   Block 3 (task)        │     │
│   └─ Notes    │    │   Block 4 (list)        │     │
│               │    │   ...                    │     │
│               │    └──────────────────────────┘     │
│               │                                       │
└───────────────┴──────────────────────────────────────┘
```

### 3.2 Sidebar Components

**Persistent Sections**:
- **All Pages**: Flat list of all user pages
- **Favorites**: Starred pages for quick access
- **Recent**: Last 10 visited pages
- **Archived**: Soft-deleted pages (trash)

**Page Tree**:
- Collapsible hierarchy
- Drag-and-drop to reorganize
- Hover actions: favorite, archive, more options
- Inline rename (click to edit)

### 3.3 Main Editor Area

**Page Header**:
```
┌────────────────────────────────────────┐
│  📄 [Page Title - Click to Edit]      │
│  Path: Home > Projects > Ocean MVP     │
│  Last edited: 2 hours ago by You       │
│                                         │
│  [Add Icon] [Add Cover] [Share] [•••]  │
└────────────────────────────────────────┘
```

**Block Editor**:
- Each block has:
  - **Drag Handle** (⋮⋮) - For reordering
  - **Block Type Icon** - Visual indicator
  - **Content Area** - Inline editing
  - **Block Menu** (⋯) - Delete, duplicate, convert

**Slash Commands** (`/`):
```
/text      → Plain text block
/h1        → Heading 1
/h2        → Heading 2
/h3        → Heading 3
/list      → Bullet list
/task      → Todo checkbox
/link      → External link
/page      → Link to another page
```

---

## 4. Core Features (MVP)

### 4.1 Page Management

**Create Page**:
- Click "New Page" in sidebar
- Opens blank page with title prompt
- Auto-focuses on title input
- Creates first block automatically

**Edit Page**:
- Click page title to edit inline
- Auto-save on blur (debounced 500ms)
- Show "Saving..." indicator

**Delete Page** (Soft Delete):
- Right-click page → Archive
- Moves to "Archived" section
- Can restore from archived

**Move Page** (Reparent):
- Drag page in sidebar to new parent
- Updates page tree hierarchy
- Shows breadcrumb path

### 4.2 Block Editor

**Block Types** (6 types in MVP):

1. **Text Block**
   - Markdown formatting: **bold**, *italic*, `code`
   - Inline links: [link text](url)
   - Auto-convert: -- → — (em dash)

2. **Heading Block** (H1, H2, H3)
   - Auto-generates anchor IDs
   - Appears in table of contents (future)
   - Keyboard: Ctrl+Alt+1/2/3

3. **List Block**
   - Bullet list (•) and numbered (1, 2, 3)
   - Tab/Shift+Tab for nesting
   - Enter to create new item
   - Backspace on empty item to delete

4. **Task Block**
   - Checkbox + text
   - Click checkbox to toggle
   - Strikethrough when checked
   - Keyboard: Ctrl+Shift+T

5. **Link Block**
   - External URL + display text
   - Auto-fetch title from URL (if accessible)
   - Show favicon preview

6. **Page Link Block**
   - Links to another Ocean page
   - Shows page icon + title
   - Click to navigate
   - Keyboard: @ or [[ to trigger page search

**Block Actions**:
- **Create**: Press Enter to create block below
- **Delete**: Backspace on empty block
- **Move**: Drag handle (⋮⋮) to reorder
- **Convert**: Click block menu → Convert to...
- **Duplicate**: Click block menu → Duplicate

**Keyboard Shortcuts**:
```
Enter              → Create new block below
Shift+Enter        → Newline within block
Backspace (empty)  → Delete current block
Ctrl+D             → Duplicate block
Ctrl+/             → Show slash command menu
Ctrl+K             → Create link
Ctrl+B             → Bold
Ctrl+I             → Italic
Ctrl+Shift+X       → Toggle task checkbox
Tab                → Indent block
Shift+Tab          → Unindent block
Ctrl+Up/Down       → Move block up/down
Ctrl+Z             → Undo
Ctrl+Shift+Z       → Redo
```

### 4.3 Search

**Global Search** (Cmd+K):
```
┌──────────────────────────────────────┐
│  🔍  Search pages and blocks...      │
├──────────────────────────────────────┤
│  Recent:                             │
│  • Project Planning                  │
│  • Meeting Notes                     │
│                                      │
│  Suggestions:                        │
│  • Create new page                   │
└──────────────────────────────────────┘
```

**Search Features**:
- **As-you-type search** (debounced 300ms)
- **Semantic search** using ZeroDB embeddings
- **Filter by block type**: text, task, etc.
- **Filter by tags**: #important, #work
- **Results ranked by relevance**
- **Highlight matching text**

**Search Results**:
```
┌────────────────────────────────────────┐
│  📄 Project Planning                   │
│  ...found "machine learning" in:       │
│  "We need to implement ML features..." │
│  ───────────────────────────────────── │
│  ☑ Task: Complete ML integration       │
│  "Integrate ML model with backend API" │
└────────────────────────────────────────┘
```

### 4.4 Linking & Backlinks

**Create Link**:
- Type `[[` or `@` to trigger page search
- Select page from dropdown
- Creates page_link block

**Backlinks Panel** (Expandable):
```
┌────────────────────────────────────────┐
│  🔗 Linked to this page (3)            │
├────────────────────────────────────────┤
│  📄 Meeting Notes                      │
│  "Discuss Ocean MVP progress..."       │
│  ───────────────────────────────────── │
│  📄 Roadmap                            │
│  "Ocean launch planned for Jan 2026"   │
└────────────────────────────────────────┘
```

### 4.5 Tags

**Add Tag**:
- Type `#` followed by tag name
- Auto-complete from existing tags
- Creates tag if new

**Tag Management**:
- Click tag to view all tagged blocks
- Edit tag color in settings
- Delete unused tags

**Tag Display**:
```
Block content here #important #work
                   └─ Blue    └─ Red
```

### 4.6 Collaboration (Future - Not MVP)

**Not included in MVP**:
- Real-time multiplayer editing
- Comments and threads
- Mentions (@username)
- Sharing and permissions

---

## 5. Technical Architecture

### 5.1 Next.js App Router Structure

```
app/
├── (auth)/
│   ├── login/
│   │   └── page.tsx          # Login page
│   └── signup/
│       └── page.tsx          # Signup page
├── (workspace)/
│   ├── layout.tsx            # Workspace layout (sidebar + nav)
│   ├── page.tsx              # Workspace home
│   ├── [page_id]/
│   │   └── page.tsx          # Page viewer/editor
│   └── search/
│       └── page.tsx          # Search results page
├── api/
│   └── auth/
│       └── [...nextauth]/
│           └── route.ts      # NextAuth.js configuration
└── layout.tsx                # Root layout
```

### 5.2 Component Structure

```
components/
├── editor/
│   ├── BlockEditor.tsx           # Main block editor
│   ├── blocks/
│   │   ├── TextBlock.tsx         # Text block component
│   │   ├── HeadingBlock.tsx      # Heading block component
│   │   ├── ListBlock.tsx         # List block component
│   │   ├── TaskBlock.tsx         # Task block component
│   │   ├── LinkBlock.tsx         # Link block component
│   │   └── PageLinkBlock.tsx     # Page link block component
│   ├── SlashCommandMenu.tsx      # Slash command popup
│   └── BlockMenu.tsx             # Block actions menu (⋯)
├── sidebar/
│   ├── Sidebar.tsx               # Main sidebar container
│   ├── PageTree.tsx              # Hierarchical page tree
│   ├── PageTreeItem.tsx          # Single page in tree
│   └── SidebarSearch.tsx         # Quick search in sidebar
├── search/
│   ├── GlobalSearch.tsx          # Cmd+K search modal
│   ├── SearchResults.tsx         # Search results list
│   └── SearchResult.tsx          # Single search result
├── page/
│   ├── PageHeader.tsx            # Page title + metadata
│   ├── PageBreadcrumb.tsx        # Breadcrumb navigation
│   └── BacklinksPanel.tsx        # Backlinks expandable panel
├── ui/
│   └── ...                       # shadcn/ui components
└── layout/
    ├── TopNav.tsx                # Top navigation bar
    └── WorkspaceLayout.tsx       # Workspace wrapper
```

### 5.3 State Management

**TanStack Query** (React Query v5):

```typescript
// hooks/usePages.ts
export function usePages() {
  return useQuery({
    queryKey: ['pages'],
    queryFn: async () => {
      const response = await fetch('/api/v1/ocean/pages');
      return response.json();
    }
  });
}

// hooks/useCreatePage.ts
export function useCreatePage() {
  const queryClient = useQueryClient();

  return useMutation({
    mutationFn: async (pageData) => {
      const response = await fetch('/api/v1/ocean/pages', {
        method: 'POST',
        body: JSON.stringify(pageData)
      });
      return response.json();
    },
    onSuccess: () => {
      queryClient.invalidateQueries({ queryKey: ['pages'] });
    }
  });
}
```

**Optimistic Updates**:
```typescript
// Instant UI feedback before API response
const mutation = useMutation({
  mutationFn: updateBlock,
  onMutate: async (newData) => {
    // Cancel outgoing queries
    await queryClient.cancelQueries({ queryKey: ['blocks'] });

    // Snapshot previous value
    const previous = queryClient.getQueryData(['blocks']);

    // Optimistically update
    queryClient.setQueryData(['blocks'], (old) => ({
      ...old,
      ...newData
    }));

    return { previous };
  },
  onError: (err, variables, context) => {
    // Rollback on error
    queryClient.setQueryData(['blocks'], context.previous);
  }
});
```

### 5.4 Editor Implementation (Tiptap)

**Why Tiptap?**
- Built on ProseMirror (battle-tested)
- React components for blocks
- Extensible with custom nodes
- Collaborative editing ready (future)
- Markdown shortcuts built-in

**Custom Tiptap Nodes**:
```typescript
// extensions/TaskNode.ts
export const TaskNode = Node.create({
  name: 'task',
  content: 'text*',
  marks: '_',
  group: 'block',

  addAttributes() {
    return {
      checked: {
        default: false,
        parseHTML: element => element.getAttribute('data-checked') === 'true',
        renderHTML: attributes => ({
          'data-checked': attributes.checked,
        }),
      },
    };
  },

  parseHTML() {
    return [{ tag: 'div[data-type="task"]' }];
  },

  renderHTML({ HTMLAttributes }) {
    return ['div', { 'data-type': 'task', ...HTMLAttributes }, 0];
  },

  addNodeView() {
    return ReactNodeViewRenderer(TaskBlockComponent);
  },
});
```

### 5.5 API Integration

**API Client**:
```typescript
// lib/api/client.ts
import { getSession } from 'next-auth/react';

class OceanAPIClient {
  private baseURL = process.env.NEXT_PUBLIC_API_URL;

  async request(endpoint: string, options?: RequestInit) {
    const session = await getSession();

    const response = await fetch(`${this.baseURL}${endpoint}`, {
      ...options,
      headers: {
        'Content-Type': 'application/json',
        'Authorization': `Bearer ${session?.accessToken}`,
        ...options?.headers,
      },
    });

    if (!response.ok) {
      throw new Error(`API Error: ${response.statusText}`);
    }

    return response.json();
  }

  // Pages
  async getPages() {
    return this.request('/v1/ocean/pages');
  }

  async createPage(data: CreatePageData) {
    return this.request('/v1/ocean/pages', {
      method: 'POST',
      body: JSON.stringify(data),
    });
  }

  // Blocks
  async createBlock(data: CreateBlockData) {
    return this.request('/v1/ocean/blocks', {
      method: 'POST',
      body: JSON.stringify(data),
    });
  }

  // Search
  async search(query: string, filters?: SearchFilters) {
    const params = new URLSearchParams({ q: query, ...filters });
    return this.request(`/v1/ocean/search?${params}`);
  }
}

export const apiClient = new OceanAPIClient();
```

### 5.6 Authentication (NextAuth.js v5)

```typescript
// app/api/auth/[...nextauth]/route.ts
import NextAuth from 'next-auth';
import CredentialsProvider from 'next-auth/providers/credentials';

export const { handlers, auth, signIn, signOut } = NextAuth({
  providers: [
    CredentialsProvider({
      async authorize(credentials) {
        // Call AINative backend /v1/auth/login
        const response = await fetch(`${process.env.API_URL}/v1/auth/login`, {
          method: 'POST',
          body: JSON.stringify(credentials),
        });

        if (!response.ok) return null;

        const user = await response.json();
        return user;
      },
    }),
  ],
  callbacks: {
    async jwt({ token, user }) {
      if (user) {
        token.accessToken = user.accessToken;
        token.organizationId = user.organizationId;
      }
      return token;
    },
    async session({ session, token }) {
      session.accessToken = token.accessToken;
      session.user.organizationId = token.organizationId;
      return session;
    },
  },
});
```

---

## 6. Design System

### 6.1 Colors (Dark Mode Default)

```css
/* Base colors */
--background: 0 0% 0%;        /* #000000 */
--foreground: 0 0% 100%;      /* #FFFFFF */

/* Muted colors */
--muted: 0 0% 15%;            /* #262626 */
--muted-foreground: 0 0% 70%; /* #B3B3B3 */

/* Accent colors */
--accent: 220 100% 50%;       /* #0066FF */
--accent-foreground: 0 0% 100%;

/* Destructive */
--destructive: 0 84% 60%;     /* #EF4444 */

/* Border */
--border: 0 0% 20%;           /* #333333 */
```

### 6.2 Typography

```css
/* Font families */
--font-sans: 'Inter', system-ui, sans-serif;
--font-mono: 'JetBrains Mono', monospace;

/* Font sizes */
--text-xs: 0.75rem;   /* 12px */
--text-sm: 0.875rem;  /* 14px */
--text-base: 1rem;    /* 16px */
--text-lg: 1.125rem;  /* 18px */
--text-xl: 1.25rem;   /* 20px */
--text-2xl: 1.5rem;   /* 24px */
--text-3xl: 1.875rem; /* 30px */
```

### 6.3 Spacing

```css
--spacing-1: 0.25rem;  /* 4px */
--spacing-2: 0.5rem;   /* 8px */
--spacing-3: 0.75rem;  /* 12px */
--spacing-4: 1rem;     /* 16px */
--spacing-6: 1.5rem;   /* 24px */
--spacing-8: 2rem;     /* 32px */
--spacing-12: 3rem;    /* 48px */
```

### 6.4 Component Styling

**Block Styles**:
```css
.ocean-block {
  padding: 4px 8px;
  border-radius: 4px;
  transition: background 0.2s;
}

.ocean-block:hover {
  background: var(--muted);
}

.ocean-block-drag-handle {
  opacity: 0;
  cursor: grab;
}

.ocean-block:hover .ocean-block-drag-handle {
  opacity: 0.5;
}
```

---

## 7. Performance Targets

### 7.1 Metrics

| Metric | Target | Rationale |
|--------|--------|-----------|
| **First Contentful Paint** | <1s | Fast initial load |
| **Time to Interactive** | <2s | Quick interaction readiness |
| **Bundle Size (JS)** | <100KB | Fast downloads |
| **Bundle Size (CSS)** | <30KB | Minimal styles |
| **Lighthouse Score** | >90 | Overall performance |

### 7.2 Optimization Strategies

**Code Splitting**:
```typescript
// Lazy load editor (heavy component)
const BlockEditor = dynamic(() => import('@/components/editor/BlockEditor'), {
  ssr: false,
  loading: () => <EditorSkeleton />
});
```

**Image Optimization**:
```typescript
import Image from 'next/image';

<Image
  src="/icon.png"
  width={24}
  height={24}
  alt="Page icon"
  priority={false}
/>
```

**Font Optimization**:
```typescript
// app/layout.tsx
import { Inter } from 'next/font/google';

const inter = Inter({
  subsets: ['latin'],
  display: 'swap',
  variable: '--font-sans',
});
```

---

## 8. Accessibility (WCAG 2.1 AA)

### 8.1 Requirements

- **Keyboard Navigation**: All features accessible via keyboard
- **Screen Reader Support**: ARIA labels on all interactive elements
- **Focus Management**: Visible focus indicators, logical tab order
- **Color Contrast**: Minimum 4.5:1 for text, 3:1 for UI components
- **Semantic HTML**: Use proper heading hierarchy, landmarks

### 8.2 Implementation

**Keyboard Navigation**:
```typescript
// components/editor/BlockEditor.tsx
<div
  role="textbox"
  aria-label="Block content"
  tabIndex={0}
  onKeyDown={handleKeyDown}
>
  {content}
</div>
```

**ARIA Labels**:
```typescript
<button
  aria-label="Delete block"
  onClick={handleDelete}
>
  <TrashIcon />
</button>
```

**Focus Management**:
```typescript
useEffect(() => {
  if (isOpen) {
    // Focus first input when modal opens
    inputRef.current?.focus();
  }
}, [isOpen]);
```

---

## 9. Deployment & DevOps

### 9.1 Vercel Configuration

```json
// vercel.json
{
  "buildCommand": "npm run build",
  "outputDirectory": ".next",
  "framework": "nextjs",
  "regions": ["iad1"],
  "env": {
    "NEXT_PUBLIC_API_URL": "https://api.ainative.studio",
    "NEXTAUTH_URL": "https://ocean.ainative.studio",
    "NEXTAUTH_SECRET": "@nextauth-secret"
  }
}
```

### 9.2 Environment Variables

```bash
# .env.local
NEXT_PUBLIC_API_URL=http://localhost:8000
NEXTAUTH_URL=http://localhost:3000
NEXTAUTH_SECRET=your-secret-here
DATABASE_URL=postgresql://...
```

---

## 10. Success Criteria

### 10.1 MVP Launch Criteria

- [ ] User can create, edit, delete pages
- [ ] User can create all 6 block types
- [ ] User can search pages and blocks semantically
- [ ] User can link pages together
- [ ] Backlinks display correctly
- [ ] Keyboard shortcuts work
- [ ] Mobile responsive (tablet and above)
- [ ] Lighthouse score >90
- [ ] WCAG 2.1 AA compliant
- [ ] Zero critical bugs

### 10.2 User Experience Metrics

- **Page Load Time**: <2s (p95)
- **Search Response Time**: <300ms (p95)
- **Block Creation Time**: <100ms (p95)
- **Keyboard Shortcut Coverage**: 100% of actions
- **Mobile Usability Score**: >85 (Google)

---

## 11. Future Enhancements (Post-MVP)

### Phase 2: Collaboration
- Real-time multiplayer editing (Yjs or Liveblocks)
- Comments and threads
- Mentions (@username)
- Sharing and permissions

### Phase 3: Advanced Features
- Templates and snippets
- Databases (tables, kanban, gallery)
- Embeds (YouTube, Twitter, etc.)
- Export (Markdown, PDF, HTML)
- Import (Notion, Google Docs)

### Phase 4: AI Features
- AI writing assistant
- Smart suggestions
- Auto-tagging
- Content summarization

---

## 12. Appendix

### 12.1 Browser Support

- Chrome/Edge: Latest 2 versions
- Firefox: Latest 2 versions
- Safari: Latest 2 versions
- Mobile Safari: iOS 15+
- Mobile Chrome: Android 10+

### 12.2 Third-Party Dependencies

```json
{
  "next": "^15.0.0",
  "react": "^19.0.0",
  "typescript": "^5.8.0",
  "@tanstack/react-query": "^5.0.0",
  "next-auth": "^5.0.0",
  "@tiptap/react": "^2.8.0",
  "@tiptap/starter-kit": "^2.8.0",
  "@radix-ui/react-dropdown-menu": "^2.0.0",
  "tailwindcss": "^3.4.0",
  "cmdk": "^1.0.0"
}
```

---

**Document Version**: 1.0
**Last Updated**: December 23, 2025
**Status**: Ready for Implementation
