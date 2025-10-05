# React Flow Org Chart - AI Coding Instructions

This is a React organizational chart visualization app using React Flow, Dagre layouts, and Faker.js for generated data.

## Architecture Overview

**Core Flow**: `App.jsx` → `generateTeamNodesAndEdges()` → `getLayoutedElements()` → React Flow render
- **Nodes**: Custom `PersonNode` components with person data (name, role, image, manager status)
- **Edges**: Hierarchical connections from manager to direct reports
- **Layouts**: Two directions supported via `LayoutDirection` type: `'LR'` (horizontal) and `'TB'` (vertical)

## Key Patterns

### Node Generation Algorithm (`src/utils/generateTeamNodesAndEdges.ts`)
- Creates hierarchical org structure: CEO → Managers (≤3 levels) → Individual Contributors
- Each manager gets 1-7 random direct reports using `Math.floor(Math.random() * 7) + 1`
- Faker.js generates realistic person data: `faker.person.fullName()`, `faker.person.jobTitle()`
- Manager detection: `isManager: levels.length <= maxManagerLevel` (maxManagerLevel = 2)

### Custom Hook Pattern (`src/hooks/useRedraw.ts`)
- Encapsulates redraw logic with direction switching
- Returns callback that regenerates entire chart: `(direction: LayoutDirection) => void`
- Automatically handles React Flow state updates via `setNodes` and `setEdges`

### React Flow Integration
- Custom node type registration: `const nodeTypes = { personNode: PersonNode }`
- Handle positioning depends on direction: `Position.Top/Bottom` for TB, `Position.Left/Right` for LR
- Fixed node width: `const nodeWidth = 300` (consistent across all person nodes)

## Development Workflow

### Setup & Build Commands
```bash
npm install                    # Install dependencies
npm run dev                   # Start Vite dev server
npm run build                 # Production build
npm run lint                  # ESLint check
```

### CSS Build Process
Tailwind requires separate watch process:
```bash
npx tailwindcss -i ./src/input.css -o ./public/output.css --watch
```

## Component Architecture

### PersonNode Structure
- **Props**: `{ data, isConnectable }` where `data: NodeData`
- **Styling**: Tailwind classes with consistent shadow pattern: `shadow-md shadow-gray-600`
- **Handles**: Dynamic positioning based on `data.direction` prop
- **Image Source**: Faker Lorem Flickr API: `faker.image.urlLoremFlickr({ width: 200, height: 200, category: 'people' })`

### Control Panel Pattern
- Panel component from React Flow: `<Panel position="top-right">`
- Number input for employee count with `parseInt(e.target.value) || 0` fallback
- Direction buttons trigger `redraw('TB')` or `redraw('LR')`

## TypeScript Conventions

### Type Definitions (`src/utils/types.ts`)
- `CustomNode`: Extends base node with person data and fixed width
- `NodeData`: Person info + hierarchical metadata (level, isManager, direction)
- `LayoutDirection`: String union `'LR' | 'TB'` for layout orientation

### File Extensions
- `.tsx` for TypeScript React components with JSX
- `.ts` for pure TypeScript utilities and types
- `.jsx` for JavaScript React components (App.jsx, PersonNode.jsx)

## External Dependencies

### Critical Libraries
- `@xyflow/react`: React Flow v12+ (note: newer package name, not `reactflow`)
- `@dagrejs/dagre`: Auto-layout algorithm (handles `getLayoutedElements` logic)
- `@faker-js/faker`: Data generation (person names, job titles, images)

### Layout Engine
- Dagre handles automatic positioning in `src/utils/getLayoutedElements.ts`
- Direction parameter controls tree orientation: `'LR'` = left-to-right, `'TB'` = top-to-bottom
- Snap to grid enabled: `snapToGrid={true}` with `snapGrid={[15, 15]}`