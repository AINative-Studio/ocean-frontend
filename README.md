# Ocean Frontend

**Block-Based Knowledge Workspace - Next.js 15 Frontend with Tiptap Editor**

Ocean is a modern block-based knowledge management workspace similar to Notion, built with Next.js 15 and TypeScript. **All data services powered by AINative ZeroDB** - our serverless NoSQL database with built-in vector search and embeddings API.

---

## 🚀 Quick Start

```bash
# Clone repository
git clone https://github.com/AINative-Studio/ocean-frontend.git
cd ocean-frontend

# Install dependencies
npm install

# Configure environment
cp .env.example .env.local
# Edit .env.local with your API credentials

# Run development server
npm run dev

# Open browser
open http://localhost:3000
```

---

## 📋 Project Overview

Ocean Frontend provides a beautiful, keyboard-first block editor for managing knowledge with pages, blocks, links, and semantic search.

### Key Features

- **Block Editor**: 6 block types with Tiptap extensible editor
- **Slash Commands**: `/` to quickly create any block type
- **Global Search**: `Cmd+K` for instant semantic search
- **Page Linking**: `@` or `[[` to link pages with automatic backlinks
- **Tag System**: `#` to create and assign colored tags
- **Real-time Updates**: Optimistic UI with automatic rollback on errors
- **Keyboard-First**: Comprehensive shortcuts for power users
- **Responsive**: Works on desktop and tablet (768px+)

### Tech Stack

- **Framework**: Next.js 15 (App Router)
- **Language**: TypeScript 5.8+ (strict mode)
- **UI Library**: shadcn/ui + Radix UI + Tailwind CSS
- **Editor**: Tiptap (extensible rich-text)
- **State Management**: TanStack Query v5 (React Query)
- **Authentication**: NextAuth.js v5
- **Deployment**: Vercel

---

## 📚 Documentation

| Document | Description |
|----------|-------------|
| [FRONTEND_BACKLOG.md](FRONTEND_BACKLOG.md) | Complete development backlog (23 issues, 44 story points) |
| [FRONTEND_PRD.md](FRONTEND_PRD.md) | Comprehensive Next.js 15 implementation spec |
| [PRD.md](PRD.md) | Product requirements document |
| [.claude/CLAUDE.md](.claude/CLAUDE.md) | Project memory and coding standards |

---

## 🗂️ Project Structure

```
ocean-frontend/
├── app/
│   ├── (auth)/
│   │   ├── login/                     # Login page
│   │   └── signup/                    # Signup page
│   ├── (workspace)/
│   │   └── [pageId]/                  # Dynamic page routes
│   ├── api/
│   │   └── auth/[...nextauth]/        # NextAuth routes
│   └── layout.tsx                     # Root layout
├── components/
│   ├── layout/
│   │   ├── WorkspaceLayout.tsx        # Main workspace
│   │   ├── Sidebar.tsx                # Collapsible sidebar
│   │   └── TopNav.tsx                 # Top navigation
│   ├── sidebar/
│   │   ├── PageTree.tsx               # Hierarchical tree
│   │   └── PageTreeItem.tsx           # Tree node
│   ├── editor/
│   │   ├── BlockEditor.tsx            # Tiptap editor
│   │   ├── SlashCommandMenu.tsx       # / command menu
│   │   └── blocks/
│   │       ├── TextBlock.tsx          # Text block
│   │       ├── HeadingBlock.tsx       # Heading block
│   │       ├── ListBlock.tsx          # List block
│   │       ├── TaskBlock.tsx          # Task/checkbox block
│   │       ├── LinkBlock.tsx          # URL link block
│   │       └── PageLinkBlock.tsx      # Page reference block
│   ├── search/
│   │   ├── GlobalSearch.tsx           # Cmd+K search modal
│   │   └── SearchFilters.tsx          # Filter UI
│   └── ui/                            # shadcn/ui components
├── hooks/
│   ├── usePages.ts                    # Page data hooks
│   ├── useBlocks.ts                   # Block data hooks
│   ├── useSearch.ts                   # Search hooks
│   └── useTags.ts                     # Tag hooks
├── lib/
│   ├── api/
│   │   └── client.ts                  # API client
│   └── utils.ts                       # Utilities
├── .claude/                           # Claude Code config
└── public/                            # Static assets
```

---

## 🔑 Environment Variables

Create `.env.local`:

```bash
# Backend API
NEXT_PUBLIC_API_URL=https://api.ainative.studio

# NextAuth
NEXTAUTH_URL=http://localhost:3000
NEXTAUTH_SECRET=<generate-with-openssl-rand-base64-32>

# Optional: Analytics
NEXT_PUBLIC_ANALYTICS_ID=<your-analytics-id>
```

---

## 🎨 UI Components

### Block Types

1. **Text Block**: Rich text with formatting (`**bold**`, `*italic*`, etc.)
2. **Heading Block**: H1, H2, H3 with hierarchy
3. **List Block**: Bullet (`-`) or numbered (`1.`) lists
4. **Task Block**: Checkboxes with strike-through completion
5. **Link Block**: External URLs with preview
6. **Page Link Block**: Internal page references with icon

### Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| `Cmd+K` | Open global search |
| `/` | Show slash command menu |
| `Ctrl+B` | Bold text |
| `Ctrl+I` | Italic text |
| `Ctrl+K` | Insert link |
| `Ctrl+D` | Duplicate block |
| `Ctrl+Shift+X` | Toggle task checkbox |
| `Ctrl+Up/Down` | Move block up/down |
| `Tab` / `Shift+Tab` | Indent / Unindent |
| `Cmd+\` | Toggle sidebar |
| `@` or `[[` | Link to page |
| `#` | Add tag |
| `Ctrl+Shift+?` | Keyboard shortcuts help |

---

## 🏗️ Development Workflow

### Sprint Plan (3 sprints, 2-3 weeks)

**Sprint 1 (Week 1)**: Foundation & Layout
- Issues #1-6 (13 story points)
- Next.js setup, auth, workspace layout, page tree

**Sprint 2 (Week 2)**: Block Editor & Search
- Issues #7-12 (18 story points)
- Tiptap editor, all block types, slash commands, search

**Sprint 3 (Week 3)**: Linking, Tags & Polish
- Issues #13-23 (13 story points)
- Page linking, backlinks, tags, performance, testing, deployment

### GitHub Issues

View all issues: [https://github.com/AINative-Studio/ocean-frontend/issues](https://github.com/AINative-Studio/ocean-frontend/issues)

### Coding Standards

Ocean follows AINative core coding standards. See [.claude/CLAUDE.md](.claude/CLAUDE.md) for:

- **ZERO AI Attribution Policy**: No "Claude", "Anthropic", or AI references in commits
- **Issue Tracking**: NO code without a GitHub issue
- **TypeScript**: Strict mode, full type safety
- **Testing**: 70%+ test coverage with Vitest
- **Performance**: <100KB initial bundle, Lighthouse score >90

---

## 🧪 Testing

```bash
# Run all tests
npm test

# Run tests with coverage
npm test -- --coverage

# Run specific test file
npm test -- PageTree.test.tsx

# Run tests in watch mode
npm test -- --watch
```

**Coverage Target**: ≥70% for components

---

## 🎯 Performance Targets

- **Initial Bundle**: <100KB JavaScript
- **Lighthouse Score**: >90
- **First Contentful Paint (FCP)**: <1s
- **Time to Interactive (TTI)**: <2s
- **Largest Contentful Paint (LCP)**: <2.5s
- **Cumulative Layout Shift (CLS)**: <0.1

---

## ♿ Accessibility

Ocean meets WCAG 2.1 AA standards:

- **Keyboard Navigation**: All features accessible via keyboard
- **ARIA Labels**: Comprehensive labeling for screen readers
- **Color Contrast**: 4.5:1 minimum contrast ratio
- **Focus Management**: Clear focus indicators
- **Screen Reader**: Full compatibility with NVDA/JAWS/VoiceOver

Run accessibility audit:
```bash
npm run lighthouse
```

---

## 🚢 Deployment

### Vercel (Recommended)

```bash
# Install Vercel CLI
npm i -g vercel

# Login
vercel login

# Deploy
vercel

# Deploy to production
vercel --prod
```

### Environment Variables in Vercel

Set these in Vercel dashboard:
- `NEXT_PUBLIC_API_URL`
- `NEXTAUTH_URL`
- `NEXTAUTH_SECRET`

### Custom Domain

Configure `ocean.ainative.studio` in Vercel dashboard.

---

## 🤝 Contributing

1. **Create a GitHub issue** for your feature/bug
2. **Create a branch**: `git checkout -b feature/123-short-description`
3. **Write tests first** (TDD approach)
4. **Implement feature** with TypeScript
5. **Run tests**: `npm test`
6. **Check types**: `npm run type-check`
7. **Commit**: `git commit -m "Add feature\n\nRefs #123"`
8. **Push**: `git push origin feature/123-short-description`
9. **Create PR** linking to issue

**Important**: Read `.claude/git-rules.md` for commit message rules.

---

## 📦 Scripts

```bash
npm run dev              # Start development server
npm run build            # Build for production
npm run start            # Start production server
npm run lint             # Run ESLint
npm run type-check       # Check TypeScript types
npm test                 # Run tests
npm run lighthouse       # Run Lighthouse audit
```

---

## 🎨 Design System

Ocean uses shadcn/ui + Tailwind CSS for consistent design:

```bash
# Add new shadcn component
npx shadcn@latest add button
npx shadcn@latest add dialog
npx shadcn@latest add dropdown-menu

# See available components
npx shadcn@latest add
```

### Theme Configuration

Edit `tailwind.config.ts` for custom colors, spacing, typography.

---

## 🐛 Troubleshooting

### Issue: API requests fail with CORS error
**Solution**: Check `NEXT_PUBLIC_API_URL` is correct and backend CORS is configured

### Issue: Authentication not working
**Solution**: Verify `NEXTAUTH_SECRET` is set and backend JWT is compatible

### Issue: Build fails with type errors
**Solution**: Run `npm run type-check` to identify type issues

### Issue: Page not found on refresh
**Solution**: Next.js App Router handles this automatically; check deployment config

---

## 📖 ZeroDB Integration

Ocean Frontend connects to Ocean Backend which is powered by ZeroDB:

- **Semantic Search**: Uses ZeroDB Embeddings API (BAAI/bge-base-en-v1.5, 768 dims)
- **Real-time Updates**: Optimistic UI with TanStack Query
- **Vector Search**: Results ranked by semantic similarity
- **Cost**: FREE (no external API costs)

---

## 📝 License

Proprietary - AINative Studio

---

## 🔗 Links

- **Backend Repo**: https://github.com/AINative-Studio/ocean-backend
- **AINative Platform**: https://www.ainative.studio
- **ZeroDB Docs**: https://www.ainative.studio/zerodb
- **API Documentation**: https://api.ainative.studio/docs

---

## 💡 Architecture Highlights

### State Management

Uses TanStack Query v5 for:
- **Server State**: Automatic caching and revalidation
- **Optimistic Updates**: Instant UI feedback
- **Error Handling**: Automatic rollback on failures
- **Background Sync**: Keep data fresh without user intervention

### Editor Architecture

Tiptap provides:
- **Extensibility**: Custom nodes for all block types
- **Collaborative**: Ready for real-time collaboration (future)
- **Markdown**: Shortcuts like `**bold**`, `*italic*`, `#` heading
- **Accessibility**: Built-in keyboard navigation

### Component Composition

- **Radix UI**: Accessible component primitives
- **Tailwind CSS**: Utility-first styling
- **shadcn/ui**: Pre-built component patterns
- **Framer Motion**: Smooth transitions and animations

---

## 🎯 Roadmap

See [FRONTEND_BACKLOG.md](FRONTEND_BACKLOG.md) for complete roadmap.

**MVP (Weeks 1-3)**:
- ✅ Setup & Authentication
- ✅ Workspace Layout
- ✅ Page Tree
- ✅ Block Editor (6 types)
- ✅ Global Search
- ✅ Page Linking & Backlinks
- ✅ Tag Management
- ✅ Deployment

**Post-MVP**:
- 📱 Mobile app (React Native)
- 🤝 Real-time collaboration
- 📊 Advanced analytics
- 🎨 Custom themes
- 🔌 API integrations
- 📁 File uploads

---

**Ready to build the future of knowledge management!** 🚀

For questions, see documentation or contact the team via GitHub issues.
