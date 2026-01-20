# 🎯 Interview Q&A - Complete Reference Guide

**Frontend:**
- Virtual DOM, React rendering, reconciliation, diffing
- Redux, state management, store, actions, reducers, NOT API calls
- Server Components, Client Components, use client, Next.js
- Axios, HTTP client, API calls, fetch, interceptors
- TanStack Query, React Query, useQuery, useMutation, server state, caching

**Backend:**
- .NET, .NET Framework, .NET Core, difference, cross-platform
- CQRS, Commands, Queries, MediatR, mediator pattern
- Entity Framework, EF Core, ORM, migrations, idempotent
- SQL optimization, indexes, query performance, execution plan, table scan
- SignalR, real-time, WebSockets, hubs, backplane, scaling

---

## 🎤 QUICK ANSWERS (30-second versions)

### Virtual DOM
**Q: What is Virtual DOM?**  
**A:** JavaScript representation of the real DOM. React uses it to optimize rendering by comparing changes and updating only what's different. Faster than direct DOM manipulation.

**Keywords:** Virtual DOM, reconciliation, diffing, performance

---

### Redux
**Q: What is Redux?**  
**A:** Client-side state management library. Centralized store with actions and reducers. **Important:** Redux does NOT make API calls - that's Axios or TanStack Query.

**Keywords:** Redux, state management, store, actions, reducers, NOT API calls

**Q: Redux vs API calls?**  
**A:** Redux = state management. API calls = Axios/fetch/TanStack Query. They're different things.

**Keywords:** Redux vs Axios, state vs API

---

### Server vs Client Components
**Q: Server Components vs Client Components?**  
**A:** Server Components render on server (no JS to client). Client Components render in browser (can use hooks, browser APIs). In Vite/SPA, all components are client-side.

**Keywords:** Server Components, Client Components, use client, Next.js

---

### Axios
**Q: What is Axios?**  
**A:** HTTP client library for making API requests. Better than fetch: automatic JSON parsing, interceptors, better error handling. We wrap it in an 'api' utility.

**Keywords:** Axios, HTTP client, API requests, fetch alternative

**Q: Axios vs fetch?**  
**A:** Axios has interceptors, auto JSON parsing, better errors. Fetch is native but more manual. We use Axios.

**Keywords:** Axios vs fetch, interceptors

---

### TanStack Query
**Q: What is TanStack Query?**  
**A:** Data-fetching library for server state. Automatic caching, loading states, refetching. For API data. Redux is for client state - they're different.

**Keywords:** TanStack Query, React Query, server state, caching, useQuery

**Q: useQuery vs useMutation?**  
**A:** useQuery = read data (GET), runs automatically, caches. useMutation = write data (POST/PUT/DELETE), must call mutate(), no caching.

**Keywords:** useQuery, useMutation, read vs write

---

### .NET Platform
**Q: .NET vs .NET Framework vs .NET Core?**  
**A:** .NET = current cross-platform platform. .NET Framework = legacy Windows-only. .NET Core = discontinued (merged into .NET). Use .NET 8 for new projects.

**Keywords:** .NET, .NET Framework, .NET Core, difference, cross-platform

---

### MediatR
**Q: What is MediatR?**  
**A:** Mediator pattern library. Decouples controllers from handlers. Implements CQRS: Commands (write) and Queries (read).

**Keywords:** MediatR, mediator pattern, CQRS, commands, queries

**Q: Commands vs Queries?**  
**A:** Commands = write operations (Create/Update/Delete), change state, return ID. Queries = read operations (Get/List), don't change state, return data.

**Keywords:** Commands, Queries, CQRS, write vs read

---

### SQL Optimization
**Q: How to optimize SQL?**  
**A:** Use indexes, efficient WHERE clauses, select only needed columns, avoid N+1 queries, use pagination, check execution plans for table scans.

**Keywords:** SQL optimization, indexes, query performance, execution plan

**Q: Index trade-offs?**  
**A:** Benefits: faster reads, faster joins. Costs: slower writes, storage space, maintenance. Create on frequently queried columns, foreign keys.

**Keywords:** Index, trade-offs, faster reads, slower writes

---

### SignalR
**Q: What is SignalR?**  
**A:** Real-time communication library. Server-to-client push notifications. Uses WebSockets (best), falls back to SSE or Long Polling. Uses Hubs for communication.

**Keywords:** SignalR, real-time, WebSockets, hubs, push notifications

---

## 📖 DETAILED ANSWERS

## Frontend Questions

### Virtual DOM

#### Q: What is the Virtual DOM?
**SPEAKABLE ANSWER:**  
"The Virtual DOM is a JavaScript representation of the real DOM. React creates a lightweight copy in memory, and when state changes, React compares the new Virtual DOM with the previous one. It then updates only the changed parts in the real DOM. This is much faster than directly manipulating the DOM because DOM operations are expensive."

**Key points:**
- **In-memory representation** of the real DOM
- **JavaScript object** that mirrors the DOM structure
- **Faster than direct DOM manipulation**
- React uses it to calculate the most efficient way to update the real DOM

**How it works:**
1. React creates a Virtual DOM representation of your UI
2. When state changes, React creates a new Virtual DOM tree
3. React compares (diffs) the new Virtual DOM with the previous one
4. React updates only the changed parts in the real DOM (reconciliation)

**Example:**
```javascript
// Virtual DOM (JavaScript object)
{
  type: 'div',
  props: { className: 'container' },
  children: [
    { type: 'h1', props: {}, children: ['Hello'] }
  ]
}

// React converts this to real DOM elements
```

**Benefits:**
- **Performance**: Batch updates, minimize DOM operations
- **Predictable**: React handles the diffing algorithm
- **Cross-platform**: Same Virtual DOM can render to web, mobile (React Native)

**Why not update DOM directly?**
- DOM manipulation is slow and expensive
- Virtual DOM batches changes and updates efficiently
- Prevents unnecessary re-renders

**Keywords:** Virtual DOM, reconciliation, diffing algorithm, performance

---

#### Q: How does React's Virtual DOM differ from other frameworks?
**A:** 

**React:**
- Uses Virtual DOM with reconciliation algorithm
- Compares entire tree, updates only differences
- Declarative approach

**Vue:**
- Also uses Virtual DOM
- More template-based
- Similar reconciliation process

**Angular:**
- Uses change detection instead of Virtual DOM
- Zone.js for change detection
- Different approach, similar goal

**Svelte:**
- Compile-time optimization
- No Virtual DOM at runtime
- Converts components to efficient JavaScript

**Keywords:** Virtual DOM, React vs Vue vs Angular, reconciliation

---

### Redux

#### Q: What is Redux and what is it used for?
**SPEAKABLE ANSWER:**  
"Redux is a client-side state management library. It provides a centralized store to manage application state. It uses actions to describe what happened, and reducers to update state. **Important:** Redux does NOT make API calls - that's what Axios or TanStack Query do. Redux is purely for managing client-side state like user data, UI preferences, or app-wide state."

**Key concepts:**
- **Store**: Single source of truth for application state
- **Actions**: Plain objects describing what happened
- **Reducers**: Pure functions that update state based on actions
- **Dispatch**: Method to trigger actions

**Purpose:**
- Manage **global client-side state** (user data, UI preferences, app-wide state)
- **Predictable state updates** through reducers
- **Time-travel debugging** with Redux DevTools
- **State persistence** and hydration

**CRITICAL DISTINCTION:**
- ❌ Redux does **NOT** make API calls
- ✅ Redux is for **client-side state management**
- ✅ API calls are done with HTTP clients (Axios, fetch) or data-fetching libraries (TanStack Query)

**Example:**
```typescript
// Redux Store
const store = {
  user: { name: 'John', email: 'john@example.com' },
  theme: 'dark',
  entities: []
};

// Action
{ type: 'SET_USER', payload: { name: 'Jane' } }

// Reducer
function userReducer(state = initialState, action) {
  switch (action.type) {
    case 'SET_USER':
      return { ...state, user: action.payload };
    default:
      return state;
  }
}
```

**When to use Redux:**
- Complex global state shared across many components
- Need for time-travel debugging
- Large applications with complex state logic
- Team needs strict state update patterns

**When NOT to use Redux:**
- Simple local component state (use `useState`)
- Server data (use TanStack Query)
- Simple global state (use Zustand or Context API)

**Keywords:** Redux, state management, store, actions, reducers, NOT API calls

---

#### Q: What is Redux Toolkit and how does it differ from Redux?
**A:** **Redux Toolkit (RTK)** is the **official, recommended way** to write Redux logic. It simplifies Redux usage and reduces boilerplate.

**Differences:**

**Traditional Redux:**
- Lots of boilerplate (actions, action creators, reducers)
- Manual immutability handling
- Complex setup

**Redux Toolkit:**
- Less boilerplate with `createSlice`
- Automatic immutability with Immer
- Built-in best practices
- Includes Redux Thunk by default

**Example:**
```typescript
// Redux Toolkit (simpler)
import { createSlice } from '@reduxjs/toolkit';

const entitiesSlice = createSlice({
  name: 'entities',
  initialState: { items: [] },
  reducers: {
    addEntity: (state, action) => {
      state.items.push(action.payload); // Immer handles immutability
    },
  },
});

// vs Traditional Redux (more boilerplate)
// Actions, action creators, reducers, etc.
```

**RTK Query:**
- Built-in data fetching solution
- Similar to TanStack Query
- Integrated with Redux store

**Keywords:** Redux Toolkit, RTK, createSlice, Immer, RTK Query

---

#### Q: What is the difference between Redux and Context API?
**A:**

| Redux | Context API |
|-------|-------------|
| External library | Built into React |
| More boilerplate | Less boilerplate |
| Better for complex state | Better for simple state |
| Time-travel debugging | No debugging tools |
| Middleware support | No middleware |
| Optimized re-renders | Can cause unnecessary re-renders |

**When to use Context API:**
- Simple global state (theme, user, language)
- Small to medium applications
- Don't need Redux features

**When to use Redux:**
- Complex state logic
- Need middleware (logging, async)
- Large applications
- Need debugging tools

**Keywords:** Redux vs Context API, comparison, when to use

---

### Server Components and Client Components

#### Q: What are React Server Components?
**SPEAKABLE ANSWER:**  
"Server Components render on the server, not in the browser. They can access databases directly, use async/await, and zero JavaScript is sent to the client. But they can't use hooks like useState, or browser APIs like localStorage. They're part of React 19 and Next.js 13+. In our Vite SPA setup, we don't use them - all components are client-side."

**Characteristics:**
- **Run only on server** (Node.js environment)
- **Zero JavaScript sent to client** (reduces bundle size)
- **Can use async/await** directly
- **Can access databases, file system, APIs** directly
- **Cannot use hooks** (useState, useEffect, etc.)
- **Cannot use browser APIs** (localStorage, window, etc.)
- **Cannot handle user interactions** (onClick, onChange, etc.)

**Example:**
```typescript
// Server Component (Next.js)
// No 'use client' directive = Server Component
async function EntityList() {
  // Direct database access on server
  const entities = await db.entities.findMany();
  
  return (
    <div>
      {entities.map(entity => (
        <EntityCard key={entity.id} entity={entity} />
      ))}
    </div>
  );
}
```

**Benefits:**
- **Smaller bundle size** - No JavaScript sent to client
- **Faster initial load** - Server-rendered HTML
- **Direct data access** - No API layer needed
- **Better SEO** - Server-rendered content

**Keywords:** Server Components, server-side rendering, Next.js, no hooks

---

#### Q: What are Client Components?
**SPEAKABLE ANSWER:**  
"Client Components are traditional React components that render in the browser. They can use hooks, browser APIs, handle user interactions. In Next.js, you need 'use client' directive. In Vite/SPA, all components are client-side by default."

**Characteristics:**
- **Run in browser** (JavaScript environment)
- **JavaScript sent to client** (included in bundle)
- **Can use React hooks** (useState, useEffect, useCallback, etc.)
- **Can use browser APIs** (localStorage, window, fetch, etc.)
- **Can handle user interactions** (onClick, onChange, etc.)
- **Can use Context API, Redux, etc.**

**Example:**
```typescript
// Client Component
'use client'; // Required directive in Next.js

import { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);
  
  return (
    <button onClick={() => setCount(count + 1)}>
      Count: {count}
    </button>
  );
}
```

**When to use Client Components:**
- User interactions (buttons, forms, inputs)
- Browser APIs (localStorage, geolocation)
- React hooks (useState, useEffect)
- Context providers
- Third-party libraries that need browser APIs

**Keywords:** Client Components, use client, browser, hooks, interactions

---

#### Q: When should you use Server Components vs Client Components?
**SPEAKABLE ANSWER:**  
"Use Server Components for static data, no interactivity, heavy dependencies you don't want in bundle. Use Client Components for user interactions, browser APIs, hooks. Simple rule: need interactivity or browser APIs? Use Client Component. Otherwise, can be Server Component."

**Use Server Components when:**
- ✅ Static or server-fetched data
- ✅ No interactivity needed
- ✅ Heavy dependencies (don't want in client bundle)
- ✅ SEO-critical content
- ✅ Direct database access

**Use Client Components when:**
- ✅ User interactions (clicks, form inputs)
- ✅ Browser APIs (localStorage, window)
- ✅ React hooks (useState, useEffect)
- ✅ Event handlers (onClick, onChange)
- ✅ Context providers
- ✅ Third-party libraries requiring browser

**Decision Tree:**
```
Do you need interactivity or browser APIs?
├─ YES → Client Component ('use client')
└─ NO → Can be Server Component (default in Next.js)
```

**Important:**
- In **Vite/SPA** (like your current setup), all components are client-side
- Server Components require **Next.js, Remix, or similar framework**
- Server Components can import Client Components
- Client Components **cannot** import Server Components directly

**Keywords:** Server vs Client, when to use, decision tree

---

#### Q: How do Server Components work with Client Components?
**A:** Server Components can render Client Components, but not vice versa.

**Pattern:**
```typescript
// Server Component
async function EntityPage() {
  const entity = await fetchEntity(); // Server-side fetch
  
  return (
    <div>
      <h1>{entity.name}</h1>
      {/* Client Component for interactivity */}
      <EntityForm entity={entity} />
    </div>
  );
}

// Client Component
'use client';
function EntityForm({ entity }) {
  const [name, setName] = useState(entity.name);
  // Interactive form logic
}
```

**Boundary:**
- Server Components can pass data to Client Components
- Client Components receive props from Server Components
- Once you use 'use client', everything below is client-side

**Keywords:** Server Components, Client Components, boundary, props

---

### Axios

#### Q: What is Axios?
**SPEAKABLE ANSWER:**  
"Axios is an HTTP client library for making API requests. It's better than fetch because it has automatic JSON parsing, request/response interceptors for things like auth headers, and better error handling. In our codebase, we wrap Axios in an 'api' utility that handles authentication and error handling."

**Key features:**
- **Promise-based** API
- **Request/response interceptors** (auth headers, error handling)
- **Automatic JSON transformation**
- **Request/response transformation**
- **Cancel requests** (AbortController support)
- **Better error handling** than fetch

**Purpose:**
- Make HTTP requests (GET, POST, PUT, DELETE, PATCH)
- Handle API communication
- Manage request/response lifecycle

**Example:**
```typescript
import axios from 'axios';

// GET request
const response = await axios.get('/api/entities/1');

// POST request
const result = await axios.post('/api/entities', {
  name: 'New Entity',
  vatNumber: 'PT123456789'
});

// With interceptors
axios.interceptors.request.use(config => {
  config.headers.Authorization = `Bearer ${token}`;
  return config;
});
```

**In our codebase:**
```typescript
// We wrap Axios in an 'api' utility
import { api } from '@myskypro/shared-utils';

// GET request
const data = await api.get<EntityDto>('/api/entities/1');

// POST request
const result = await api.post<CreateResponse>('/api/entities', payload);
```

**Keywords:** Axios, HTTP client, API requests, interceptors

---

#### Q: What's the difference between Axios and fetch?
**SPEAKABLE ANSWER:**  
"Axios is an external library with more features. It has automatic JSON parsing, interceptors for auth headers, better error handling, and works in Node.js. Fetch is native but requires manual JSON parsing, no interceptors, and only works in browsers. We use Axios because it's more convenient."

| Axios | fetch |
|-------|-------|
| External library | Native browser API |
| Automatic JSON parsing | Manual JSON parsing |
| Request/response interceptors | No interceptors |
| Better error handling | Errors only on network failure |
| Cancel requests easily | Requires AbortController |
| Works in Node.js | Browser only (needs polyfill for Node) |
| Timeout support | No built-in timeout |

**Example comparison:**
```typescript
// Axios
const response = await axios.get('/api/data');
const data = response.data; // Already parsed

// fetch
const response = await fetch('/api/data');
const data = await response.json(); // Manual parsing
if (!response.ok) {
  throw new Error('Request failed'); // Manual error handling
}
```

**When to use Axios:**
- Need interceptors (auth, error handling)
- Want automatic JSON parsing
- Need better error handling
- Working in Node.js environment

**When to use fetch:**
- Want to avoid external dependencies
- Simple requests
- Modern browser support only

**Keywords:** Axios vs fetch, comparison, interceptors

---

#### Q: How do you handle errors with Axios?
**A:** Multiple approaches:

**1. Try/catch:**
```typescript
try {
  const response = await axios.get('/api/data');
} catch (error) {
  if (axios.isAxiosError(error)) {
    console.error('API Error:', error.response?.data);
    console.error('Status:', error.response?.status);
  }
}
```

**2. Interceptors:**
```typescript
// Response interceptor for global error handling
axios.interceptors.response.use(
  response => response,
  error => {
    if (error.response?.status === 401) {
      // Handle unauthorized
      redirectToLogin();
    }
    return Promise.reject(error);
  }
);
```

**3. With TanStack Query:**
```typescript
// TanStack Query handles errors automatically
const { data, error, isError } = useQuery({
  queryKey: ['entities'],
  queryFn: () => api.get('/api/entities'),
  onError: (error) => {
    toast.error('Failed to load entities');
  }
});
```

**Keywords:** Axios error handling, interceptors, try catch

---

### TanStack Query (React Query)

#### Q: What is TanStack Query and what is it used for?
**SPEAKABLE ANSWER:**  
"TanStack Query is a data-fetching library for managing server state. It automatically caches API responses, provides loading and error states, and refetches data when needed. It's specifically for server state - data from APIs. Redux is for client state - they're different things."

**Purpose:**
- Fetch data from APIs
- Manage **server state** (data from backend)
- Automatic caching and synchronization
- Loading and error states
- Automatic refetching

**Key features:**
- **Automatic caching** - Reduces unnecessary API calls
- **Background refetching** - Keeps data fresh
- **Request deduplication** - Multiple components requesting same data = one request
- **Optimistic updates** - Update UI before server confirms
- **Pagination and infinite queries** - Built-in support

**Important distinction:**
- TanStack Query is for **server state** (API data)
- Redux/Zustand are for **client state** (UI state, user preferences)
- They solve different problems and can work together

**Keywords:** TanStack Query, React Query, server state, caching, useQuery

---

#### Q: How does TanStack Query work?
**SPEAKABLE ANSWER:**  
"You define a query with a unique key and a function that fetches data. TanStack Query automatically caches the result, provides loading states, handles errors, and refetches when data becomes stale. Multiple components requesting the same data share the cache - only one request is made."

**Pattern:**
```typescript
import { useQuery } from '@tanstack/react-query';

// 1. Define query
const { data, isLoading, error } = useQuery({
  queryKey: ['entities', entityId], // Unique key for caching
  queryFn: ({ signal }) => api.get(`/api/entities/${entityId}`, { signal }), // Function that fetches data
  staleTime: 5 * 60 * 1000, // Data is fresh for 5 minutes
});

// 2. TanStack Query automatically:
// - Caches the result
// - Provides loading state
// - Handles errors
// - Refetches when needed
```

**Query lifecycle:**
1. Component mounts → Query runs
2. Data fetched → Cached with query key
3. Other components with same key → Get cached data
4. Data becomes stale → Refetches in background
5. Component unmounts → Data stays in cache

**Keywords:** useQuery, queryKey, queryFn, caching, lifecycle

---

#### Q: What's the difference between useQuery and useMutation?
**SPEAKABLE ANSWER:**  
"useQuery is for reading data - GET requests. It runs automatically when component mounts, caches the result, and refetches automatically. useMutation is for writing data - POST, PUT, DELETE. It doesn't run automatically, you must call mutate(), and it doesn't cache. After a mutation, you typically invalidate queries to refetch fresh data."

**useQuery** - For **reading** data (GET requests):
```typescript
// Automatically runs on mount
// Caches the result
// Refetches automatically
const { data, isLoading } = useQuery({
  queryKey: ['entities'],
  queryFn: () => api.get('/api/entities'),
});
```

**useMutation** - For **writing** data (POST, PUT, DELETE):
```typescript
// Doesn't run automatically
// Must call mutate() to trigger
// No caching
const mutation = useMutation({
  mutationFn: (payload) => api.post('/api/entities', payload),
  onSuccess: () => {
    // Invalidate queries to refetch
    queryClient.invalidateQueries({ queryKey: ['entities'] });
  },
});

// Usage
mutation.mutate({ name: 'New Entity' });
```

**When to use:**
- **useQuery**: Fetching/reading data
- **useMutation**: Creating/updating/deleting data

**Keywords:** useQuery, useMutation, read vs write, GET vs POST

---

#### Q: How does TanStack Query compare to Redux for data fetching?
**SPEAKABLE ANSWER:**  
"They solve different problems. Redux is for client-side state - things like user preferences, UI state. TanStack Query is for server state - data from APIs. Redux manages state in your app. TanStack Query fetches and caches data from your backend. They can work together - TanStack Query fetches data, you can store it in Redux if needed globally."

| TanStack Query | Redux (with Thunk/Saga) |
|----------------|-------------------------|
| **Purpose**: Server state | **Purpose**: Client state |
| Automatic caching | Manual caching |
| Built-in loading/error states | Manual state management |
| Automatic refetching | Manual refetching |
| Less boilerplate | More boilerplate |
| Optimized for API data | Optimized for app state |

**Best practice:**
- **TanStack Query** for server state (API data)
- **Redux/Zustand** for client state (UI, user preferences)
- They can work together:
  ```typescript
  // TanStack Query fetches data
  const { data } = useQuery({ ... });
  
  // Store in Redux if needed globally
  dispatch(setEntities(data));
  ```

**Keywords:** TanStack Query vs Redux, server state vs client state

---

#### Q: What is query invalidation in TanStack Query?
**A:** **Query invalidation** marks cached data as stale, triggering a refetch.

**Use case:**
After creating/updating data, invalidate related queries to refetch fresh data.

**Example:**
```typescript
const createMutation = useMutation({
  mutationFn: (payload) => api.post('/api/entities', payload),
  onSuccess: () => {
    // Invalidate all entity queries
    queryClient.invalidateQueries({ queryKey: ['entities'] });
    
    // Or invalidate specific query
    queryClient.invalidateQueries({ 
      queryKey: ['entities', entityId] 
    });
  },
});
```

**What happens:**
1. Mutation succeeds
2. Queries with matching key are marked stale
3. TanStack Query refetches in background
4. Components automatically update with new data

**Keywords:** query invalidation, invalidateQueries, stale data

---

## Backend Questions

### .NET vs .NET Framework vs .NET Core

#### Q: What is .NET?
**SPEAKABLE ANSWER:**  
".NET is a free, open-source, cross-platform development platform created by Microsoft. It's the unified platform that replaced both .NET Framework and .NET Core. It's actively developed, supports Windows, Linux, and macOS, and is the current standard for new projects."

**Current state (2024):**
- **.NET** (version 5+) is the current platform
- **.NET Framework** is legacy (Windows only, no longer actively developed)
- **.NET Core** was the cross-platform predecessor (now merged into .NET)

**Key characteristics:**
- **Cross-platform** (Windows, Linux, macOS)
- **Open source**
- **Modern** (async/await, performance, cloud-native)
- **Unified** (one platform for all scenarios)

**Keywords:** .NET, unified platform, cross-platform, open source

---

#### Q: What is .NET Framework?
**A:** **.NET Framework** is the **original, Windows-only** .NET platform released in 2002.

**Characteristics:**
- **Windows only** - Cannot run on Linux/macOS
- **Proprietary** (though some parts open-sourced)
- **Mature and stable** - 20+ years of development
- **Legacy platform** - No new features, security updates only
- **Tightly integrated with Windows** - Uses Windows-specific APIs

**When to use:**
- Maintaining existing .NET Framework applications
- Windows-only enterprise applications
- Legacy system integration
- **Not recommended for new projects**

**Versions:**
- .NET Framework 4.8 is the final version
- No .NET Framework 5, 6, 7, etc. (that's .NET)

**Keywords:** .NET Framework, Windows only, legacy, 4.8 final

---

#### Q: What is .NET Core?
**A:** **.NET Core** was Microsoft's **cross-platform, open-source** rewrite of .NET Framework (2016-2020).

**Characteristics:**
- **Cross-platform** (Windows, Linux, macOS)
- **Open source**
- **Modular** - Install only what you need
- **High performance**
- **Cloud-native** - Designed for microservices, containers

**History:**
- .NET Core 1.0 (2016) - Initial release
- .NET Core 2.0, 2.1, 2.2
- .NET Core 3.0, 3.1
- **Merged into .NET 5** (2020) - No more .NET Core

**Important:**
- .NET Core is **no longer developed**
- Replaced by **.NET 5+** (now just called ".NET")
- If you see ".NET Core" in documentation, it's likely outdated

**Keywords:** .NET Core, discontinued, merged into .NET 5

---

#### Q: What's the difference between .NET Framework, .NET Core, and .NET?
**SPEAKABLE ANSWER:**  
".NET is the current unified platform - cross-platform, open source, actively developed. .NET Framework is the legacy Windows-only platform from 2002 - no new features, just security updates. .NET Core was the cross-platform rewrite from 2016-2020, but it's been merged into .NET 5+. For new projects, use .NET 8."

| Feature | .NET Framework | .NET Core | .NET (5+) |
|---------|----------------|-----------|-----------|
| **Platform** | Windows only | Cross-platform | Cross-platform |
| **Open source** | Partial | Yes | Yes |
| **Status** | Legacy (maintenance) | Discontinued | Active development |
| **Performance** | Good | Better | Best |
| **Cloud-native** | No | Yes | Yes |
| **Container support** | Limited | Excellent | Excellent |
| **Latest version** | 4.8 (final) | 3.1 (final) | 8.0+ (current) |

**Timeline:**
```
2002: .NET Framework 1.0 (Windows only)
2016: .NET Core 1.0 (Cross-platform)
2020: .NET 5 (Unified platform, .NET Core merged in)
2021: .NET 6 (LTS)
2022: .NET 7
2023: .NET 8 (LTS)
```

**For new projects:**
- ✅ Use **.NET 8** (or latest)
- ❌ Don't use .NET Framework (legacy)
- ❌ Don't use .NET Core (discontinued)

**Keywords:** .NET, .NET Framework, .NET Core, difference, timeline

---

#### Q: Can .NET Framework code run on .NET?
**A:** **Partially**. There's **compatibility** but not 100% portability.

**Compatibility:**
- Most .NET Framework code can run on .NET with **minimal changes**
- Some APIs are **not available** in .NET
- Some Windows-specific APIs don't work on Linux

**Migration path:**
1. **Analyze** - Use .NET Portability Analyzer
2. **Update** - Replace incompatible APIs
3. **Test** - Thoroughly test on .NET
4. **Deploy** - Run on .NET

**Common issues:**
- Windows-specific APIs (WPF, Windows Forms)
- Removed APIs (some older APIs removed)
- Package references (different package ecosystem)

**Best practice:**
- For new projects: Start with .NET
- For existing projects: Plan migration to .NET
- For Windows-only apps: Consider staying on .NET Framework if migration is too complex

**Keywords:** .NET Framework migration, compatibility, portability

---

#### Q: What version of .NET should I use for new projects?
**A:** Use **.NET 8** (or the latest LTS version).

**Recommendations:**
- **.NET 8** - Current LTS (Long Term Support) until 2026
- **.NET 9** - Latest version (when available)
- **LTS versions** - .NET 6, .NET 8 (supported for 3 years)

**Why .NET 8?**
- Latest features and performance improvements
- Long-term support (LTS)
- Best performance
- Modern C# features
- Cloud-native support

**In your codebase:**
- You're using **.NET 7** (based on your rules)
- Consider upgrading to **.NET 8** for LTS support

**Keywords:** .NET 8, LTS, Long Term Support, version recommendation

---

### .NET Architecture & Patterns

#### Q: What is CQRS and when do you use it?
**A:** **CQRS (Command Query Responsibility Segregation)** separates read and write operations.

**Pattern:**
- **Commands** - Write operations (Create, Update, Delete)
- **Queries** - Read operations (Get, List, Search)

**Benefits:**
- **Optimize separately** - Different models for read/write
- **Scale independently** - Read and write databases can be different
- **Clear separation** - Commands change state, queries don't

**When to use:**
- Complex domain models
- High read/write ratio differences
- Need for different data models
- Event sourcing scenarios

**When NOT to use:**
- Simple CRUD applications
- Small applications
- Over-engineering risk

**Example:**
```csharp
// Command (write)
public class CreateEntityCommand : IRequest<Guid>
{
    public string Name { get; set; }
    public string VatNumber { get; set; }
}

// Query (read)
public class GetEntityQuery : IRequest<EntityDto>
{
    public Guid Id { get; set; }
}
```

**Keywords:** CQRS, Command Query Responsibility Segregation, commands, queries

---

#### Q: What is MediatR and why use it?
**SPEAKABLE ANSWER:**  
"MediatR implements the Mediator pattern in .NET. It decouples controllers from business logic handlers. Controllers send requests through MediatR, and handlers process them. This makes code more testable and follows single responsibility. It's commonly used with CQRS pattern - separating Commands (writes) and Queries (reads)."

**Purpose:**
- **Decouple** components
- **Request/response** handling
- **Pipeline behaviors** (validation, logging)
- **CQRS** implementation

**Benefits:**
- **Loose coupling** - Controllers don't know about handlers
- **Single Responsibility** - Each handler does one thing
- **Testability** - Easy to test handlers in isolation
- **Pipeline behaviors** - Cross-cutting concerns

**Example:**
```csharp
// Controller
[HttpPost]
public async Task<IActionResult> Create(CreateEntityRequest request)
{
    var command = new CreateEntityCommand { Name = request.Name };
    var result = await _mediator.Send(command);
    return Ok(result);
}

// Handler
public class CreateEntityHandler : IRequestHandler<CreateEntityCommand, Guid>
{
    public async Task<Guid> Handle(CreateEntityCommand request, CancellationToken cancellationToken)
    {
        // Business logic
        return entityId;
    }
}
```

**In your codebase:**
- You use MediatR in **Core Service** (complex business logic)
- You use **service pattern** in **BFFs** (simpler aggregation)

**Keywords:** MediatR, mediator pattern, CQRS, decoupling, handlers

---

#### Q: What are Commands and Queries in MediatR?
**SPEAKABLE ANSWER:**  
"In CQRS with MediatR, Commands are write operations - they change state. They usually return an ID or void. Queries are read operations - they retrieve data and don't change state. Commands end with 'Command', Queries end with 'Query'. This separation allows you to optimize reads and writes separately."

**Commands** - Write operations (change state):
- **Purpose**: Modify data, perform actions
- **Returns**: Usually an ID or success indicator
- **Side effects**: Changes application state
- **Examples**: Create, Update, Delete operations

**Queries** - Read operations (don't change state):
- **Purpose**: Retrieve data
- **Returns**: Data (DTOs, entities)
- **No side effects**: Does not modify state
- **Examples**: Get, List, Search operations

**Key distinction:**
- **Commands** = `IRequest<T>` (usually returns ID or void)
- **Queries** = `IRequest<T>` (returns data)
- Convention: Commands end with "Command", Queries end with "Query"

**Example:**
```csharp
// COMMAND - Changes state
public class CreateEntityCommand : IRequest<Guid>
{
    public string Name { get; set; }
    public string VatNumber { get; set; }
}

public class CreateEntityHandler : IRequestHandler<CreateEntityCommand, Guid>
{
    public async Task<Guid> Handle(CreateEntityCommand request, CancellationToken ct)
    {
        var entity = new Entity { Name = request.Name, VatNumber = request.VatNumber };
        _context.Entities.Add(entity);
        await _context.SaveChangesAsync(ct);
        return entity.Id; // Returns ID of created entity
    }
}

// QUERY - Reads data (no state change)
public class GetEntityQuery : IRequest<EntityDto>
{
    public Guid Id { get; set; }
}

public class GetEntityHandler : IRequestHandler<GetEntityQuery, EntityDto>
{
    public async Task<EntityDto> Handle(GetEntityQuery request, CancellationToken ct)
    {
        var entity = await _context.Entities
            .Where(e => e.Id == request.Id)
            .Select(e => new EntityDto { Id = e.Id, Name = e.Name })
            .FirstOrDefaultAsync(ct);
        return entity; // Returns data, no state change
    }
}

// Usage in controller
[HttpPost]
public async Task<IActionResult> Create(CreateEntityRequest request)
{
    var command = new CreateEntityCommand { Name = request.Name };
    var entityId = await _mediator.Send(command); // Command
    return Ok(new { entityId });
}

[HttpGet("{id}")]
public async Task<IActionResult> Get(Guid id)
{
    var query = new GetEntityQuery { Id = id };
    var entity = await _mediator.Send(query); // Query
    return Ok(entity);
}
```

**Benefits of separation:**
- **Clear intent** - Commands modify, queries read
- **Optimization** - Can optimize reads and writes separately
- **Security** - Different permissions for commands vs queries
- **Scalability** - Can scale read/write databases independently

**Keywords:** Commands, Queries, CQRS, write vs read, MediatR, IRequest

---

#### Q: What is Entity Framework Core?
**A:** **Entity Framework Core (EF Core)** is Microsoft's **ORM (Object-Relational Mapping)** for .NET.

**Purpose:**
- **Map** database tables to C# classes
- **Query** databases using LINQ
- **Manage** database schema (migrations)
- **Track changes** and save to database

**Benefits:**
- **Type-safe** queries (LINQ)
- **Migrations** - Version control for database
- **Change tracking** - Automatic update detection
- **Cross-platform** - Works with SQL Server, PostgreSQL, MySQL, etc.

**Example:**
```csharp
// DbContext
public class AppDbContext : DbContext
{
    public DbSet<Entity> Entities { get; set; }
}

// Query
var entities = await context.Entities
    .Where(e => e.Status == "Active")
    .ToListAsync();

// Create
var entity = new Entity { Name = "New Entity" };
context.Entities.Add(entity);
await context.SaveChangesAsync();
```

**Keywords:** Entity Framework Core, EF Core, ORM, LINQ, DbContext

---

#### Q: What are Entity Framework Migrations?
**A:** **Migrations** are version-controlled changes to your database schema.

**Purpose:**
- **Track** database schema changes
- **Apply** changes consistently across environments
- **Rollback** if needed
- **Version control** for database structure

**Commands:**
```bash
# Create migration
dotnet ef migrations add AddEntityTable

# Apply migration
dotnet ef database update

# Remove last migration
dotnet ef migrations remove
```

**In your codebase:**
- Migrations in `apps/core-service/Migrations/`
- Must be **idempotent** (can run multiple times safely)
- Use `IDENTITY_INSERT` for specific IDs when needed

**Keywords:** Migrations, EF Core migrations, idempotent, database schema

---

### Database Questions

#### Q: What is a relational database?
**A:** A **relational database** stores data in **tables** with **relationships** between them.

**Key concepts:**
- **Tables** - Rows and columns
- **Relationships** - Foreign keys, one-to-many, many-to-many
- **ACID** - Atomicity, Consistency, Isolation, Durability
- **SQL** - Structured Query Language

**Examples:**
- SQL Server
- PostgreSQL
- MySQL
- SQLite

**Benefits:**
- **Data integrity** - Foreign keys, constraints
- **Normalization** - Reduce data duplication
- **ACID transactions** - Reliable data operations
- **Mature** - Well-established patterns

**Keywords:** Relational database, tables, relationships, ACID, SQL

---

#### Q: What is database normalization?
**A:** **Normalization** is organizing database tables to reduce redundancy and improve data integrity.

**Normal forms:**
- **1NF** - Each column contains atomic values
- **2NF** - No partial dependencies
- **3NF** - No transitive dependencies

**Example:**
```sql
-- Denormalized (bad)
Users (id, name, email, order_id, order_date, product_name)

-- Normalized (good)
Users (id, name, email)
Orders (id, user_id, date)
OrderItems (id, order_id, product_id)
Products (id, name)
```

**Benefits:**
- **Reduce redundancy** - Data stored once
- **Data integrity** - Easier to maintain
- **Flexibility** - Easier to modify

**Trade-offs:**
- More joins required
- Can impact performance (denormalization sometimes needed)

**Keywords:** Normalization, 1NF, 2NF, 3NF, redundancy

---

#### Q: What is a database index?
**SPEAKABLE ANSWER:**  
"An index is a data structure that improves query performance by creating a quick lookup path. It's like a book index - instead of scanning every page, you can jump directly to the right page. Indexes speed up WHERE clauses, JOINs, and ORDER BY operations. But they slow down writes because every INSERT, UPDATE, DELETE must update the index."

**How it works:**
- Creates a **separate structure** pointing to table rows
- Similar to a book index
- Speeds up **WHERE**, **JOIN**, **ORDER BY** clauses
- Database uses index to find rows quickly instead of scanning entire table

**Types:**
- **Clustered** - Physical order of data (usually primary key)
  - Only one per table
  - Determines physical storage order
- **Non-clustered** - Separate structure (can have multiple)
  - Points to data rows
  - Can have many per table

**Example:**
```sql
-- Create index
CREATE INDEX IX_Entities_VatNumber ON Entities(VatNumber);

-- Query uses index automatically
SELECT * FROM Entities WHERE VatNumber = 'PT123456789';
```

**Trade-offs of using indexes:**

**Benefits:**
- ✅ **Faster reads** - Queries are significantly faster
- ✅ **Faster joins** - Foreign key indexes speed up JOINs
- ✅ **Faster sorting** - ORDER BY uses indexes
- ✅ **Unique constraints** - Enforce uniqueness efficiently

**Costs:**
- ❌ **Slower writes** - INSERT/UPDATE/DELETE must update index
- ❌ **Storage space** - Indexes consume disk space
- ❌ **Maintenance overhead** - Indexes need to be maintained
- ❌ **Too many indexes** - Can slow down writes significantly

**When to create an index:**
- ✅ Frequently queried columns (WHERE clauses)
- ✅ Foreign keys (speeds up JOINs)
- ✅ Columns used in ORDER BY
- ✅ Columns used in GROUP BY
- ✅ Columns with high selectivity (many unique values)
- ✅ Columns used in JOIN conditions

**When NOT to create an index:**
- ❌ Rarely queried columns
- ❌ Columns with low selectivity (few unique values, like boolean)
- ❌ Small tables (table scan might be faster)
- ❌ Write-heavy tables (too many indexes slow writes)
- ❌ Columns frequently updated (index maintenance cost)

**Keywords:** Index, clustered index, non-clustered index, trade-offs, performance

---

#### Q: How to identify the need for optimization/indexes?
**SPEAKABLE ANSWER:**  
"Monitor slow queries - anything over 1 second. Check execution plans - look for table scans instead of index seeks. Monitor index usage - find unused indexes. Watch performance metrics - high CPU, slow page loads, timeout errors. Common scenarios: missing index causing table scan, inefficient index on wrong columns, too many indexes slowing writes, fragmented indexes needing maintenance."

**1. Monitor slow queries:**
```sql
-- SQL Server: Find slow queries
SELECT TOP 10
    qs.execution_count,
    qs.total_elapsed_time / qs.execution_count AS avg_elapsed_time,
    SUBSTRING(qt.text, (qs.statement_start_offset/2)+1,
        ((CASE qs.statement_end_offset
            WHEN -1 THEN DATALENGTH(qt.text)
            ELSE qs.statement_end_offset
        END - qs.statement_start_offset)/2)+1) AS query_text
FROM sys.dm_exec_query_stats qs
CROSS APPLY sys.dm_exec_sql_text(qs.sql_handle) qt
ORDER BY qs.total_elapsed_time / qs.execution_count DESC;
```

**2. Check execution plans:**
- Look for **Table Scan** or **Index Scan** (bad)
- Prefer **Index Seek** (good)
- Missing index warnings in execution plan

**3. Monitor index usage:**
```sql
-- SQL Server: Find unused indexes
SELECT 
    OBJECT_NAME(i.object_id) AS TableName,
    i.name AS IndexName,
    s.user_seeks,
    s.user_scans,
    s.user_lookups,
    s.user_updates
FROM sys.indexes i
LEFT JOIN sys.dm_db_index_usage_stats s ON i.object_id = s.object_id AND i.index_id = s.index_id
WHERE OBJECTPROPERTY(i.object_id, 'IsUserTable') = 1
    AND s.database_id = DB_ID()
    AND (s.user_seeks = 0 AND s.user_scans = 0 AND s.user_lookups = 0)
    AND i.name IS NOT NULL;
```

**4. Performance metrics to watch:**
- Query execution time > 1 second
- High CPU usage on database server
- Slow page load times
- Timeout errors
- High I/O operations

**5. Common optimization scenarios:**
- **Missing index**: Query scans entire table
- **Inefficient index**: Wrong columns indexed
- **Too many indexes**: Slowing down writes
- **Fragmented indexes**: Need maintenance (REBUILD/REORGANIZE)

**Index maintenance:**
```sql
-- Rebuild index (removes fragmentation)
ALTER INDEX IX_Entities_VatNumber ON Entities REBUILD;

-- Reorganize index (lighter maintenance)
ALTER INDEX IX_Entities_VatNumber ON Entities REORGANIZE;

-- Update statistics (helps query optimizer)
UPDATE STATISTICS Entities;
```

**Keywords:** SQL optimization, identify, slow queries, execution plan, table scan, index seek

---

#### Q: How do you optimize SQL queries?
**SPEAKABLE ANSWER:**  
"First, use indexes on frequently queried columns and foreign keys. Write efficient WHERE clauses - avoid functions on columns that prevent index use. Select only needed columns, not SELECT *. Use JOINs efficiently - INNER JOIN when relationship is required. Avoid N+1 queries - use Include in EF Core. Use pagination. Check execution plans for table scans - prefer index seeks."

**1. Use indexes effectively:**
```sql
-- Create indexes on frequently queried columns
CREATE INDEX IX_Entities_VatNumber ON Entities(VatNumber);
CREATE INDEX IX_Entities_Status ON Entities(Status);

-- Composite index for multiple columns
CREATE INDEX IX_Entities_Status_Created ON Entities(Status, CreatedOnUtc);
```

**2. Write efficient WHERE clauses:**
```sql
-- ❌ BAD: Function on column prevents index use
SELECT * FROM Entities WHERE YEAR(CreatedOnUtc) = 2024;

-- ✅ GOOD: Index can be used
SELECT * FROM Entities WHERE CreatedOnUtc >= '2024-01-01' AND CreatedOnUtc < '2025-01-01';

-- ❌ BAD: LIKE with leading wildcard
SELECT * FROM Entities WHERE Name LIKE '%Skypro%';

-- ✅ GOOD: LIKE without leading wildcard (if possible)
SELECT * FROM Entities WHERE Name LIKE 'Skypro%';
```

**3. Select only needed columns:**
```sql
-- ❌ BAD: Selects all columns
SELECT * FROM Entities;

-- ✅ GOOD: Select only what you need
SELECT Id, Name, VatNumber FROM Entities;
```

**4. Use JOINs efficiently:**
```sql
-- ✅ GOOD: Use INNER JOIN for required relationships
SELECT e.Name, a.City
FROM Entities e
INNER JOIN Addresses a ON e.Id = a.EntityId;

-- ✅ GOOD: Use LEFT JOIN only when needed
SELECT e.Name, a.City
FROM Entities e
LEFT JOIN Addresses a ON e.Id = a.EntityId
WHERE a.City IS NOT NULL; -- Filter after JOIN if needed
```

**5. Avoid N+1 queries:**
```csharp
// ❌ BAD: N+1 queries
var entities = await context.Entities.ToListAsync();
foreach (var entity in entities)
{
    var addresses = await context.Addresses
        .Where(a => a.EntityId == entity.Id)
        .ToListAsync(); // One query per entity!
}

// ✅ GOOD: Single query with Include
var entities = await context.Entities
    .Include(e => e.Addresses)
    .ToListAsync();
```

**6. Use pagination:**
```sql
-- ✅ GOOD: Pagination
SELECT * FROM Entities
ORDER BY CreatedOnUtc DESC
OFFSET 0 ROWS FETCH NEXT 20 ROWS ONLY;

-- ❌ BAD: Loading all records
SELECT * FROM Entities;
```

**7. Use EXISTS instead of COUNT when checking existence:**
```sql
-- ❌ BAD: Counts all rows
IF (SELECT COUNT(*) FROM Entities WHERE Status = 'Active') > 0
BEGIN
    -- Do something
END

-- ✅ GOOD: Stops at first match
IF EXISTS (SELECT 1 FROM Entities WHERE Status = 'Active')
BEGIN
    -- Do something
END
```

**8. Avoid unnecessary subqueries:**
```sql
-- ❌ BAD: Correlated subquery
SELECT e.Name,
    (SELECT COUNT(*) FROM Addresses WHERE EntityId = e.Id) AS AddressCount
FROM Entities e;

-- ✅ GOOD: Use JOIN with GROUP BY
SELECT e.Name, COUNT(a.Id) AS AddressCount
FROM Entities e
LEFT JOIN Addresses a ON e.Id = a.EntityId
GROUP BY e.Id, e.Name;
```

**9. Use parameterized queries (prevent SQL injection + better caching):**
```csharp
// ✅ GOOD: Parameterized
var entities = await context.Entities
    .Where(e => e.VatNumber == vatNumber)
    .ToListAsync();

// ❌ BAD: String concatenation (SQL injection risk)
var query = $"SELECT * FROM Entities WHERE VatNumber = '{vatNumber}'";
```

**10. Monitor and analyze execution plans:**
- Use SQL Server Management Studio (SSMS) "Include Actual Execution Plan"
- Look for:
  - **Table Scans** (bad - no index used)
  - **Index Seeks** (good - index used efficiently)
  - **Key Lookups** (might need covering index)
  - **Sort operations** (might need index on ORDER BY columns)

**11. Update statistics regularly:**
```sql
-- Update statistics so query optimizer makes good decisions
UPDATE STATISTICS Entities;
```

**12. Consider covering indexes:**
```sql
-- Covering index includes all columns needed by query
CREATE INDEX IX_Entities_Covering ON Entities(VatNumber)
INCLUDE (Name, Status, CreatedOnUtc);

-- Query can be satisfied entirely from index (no key lookup needed)
SELECT VatNumber, Name, Status FROM Entities WHERE VatNumber = 'PT123456789';
```

**Performance testing:**
```sql
-- Enable statistics
SET STATISTICS IO ON;
SET STATISTICS TIME ON;

-- Run query and check:
-- - Logical reads (lower is better)
-- - Execution time (lower is better)
```

**Keywords:** SQL optimization, indexes, WHERE clauses, JOINs, N+1 queries, pagination, execution plan

---

### SignalR

#### Q: What is SignalR?
**SPEAKABLE ANSWER:**  
"SignalR is a library for real-time communication in .NET. It enables server-to-client push notifications. It uses WebSockets when available, which is the best option - full-duplex, low latency. If WebSockets aren't available, it falls back to Server-Sent Events or Long Polling. SignalR automatically selects the best transport. It uses Hubs for communication - clients connect to hubs, and servers can send messages to connected clients."

**Purpose:**
- **Real-time communication** - Push updates from server to clients
- **Bidirectional communication** - Server can send to clients, clients can send to server
- **Automatic connection management** - Handles reconnection, connection groups
- **Multiple transport protocols** - WebSockets, Server-Sent Events, Long Polling

**Use cases:**
- **Live notifications** - Real-time alerts, updates
- **Chat applications** - Instant messaging
- **Live dashboards** - Real-time data updates
- **Collaborative editing** - Multiple users editing simultaneously
- **Live monitoring** - Real-time system status
- **Gaming** - Real-time game state updates

**How it works:**
1. Client establishes connection to SignalR hub
2. Server can send messages to connected clients
3. Clients can send messages to server
4. SignalR automatically handles connection/disconnection

**Keywords:** SignalR, real-time, WebSockets, push notifications, hubs

---

#### Q: How does SignalR work?
**SPEAKABLE ANSWER:**  
"SignalR uses Hubs for communication. On the server, you create a Hub class with methods clients can call. Clients connect to the hub and can invoke server methods. The server can send messages to all clients, specific clients, or groups. SignalR automatically handles connection/disconnection and reconnection. For scaling across multiple servers, you need sticky sessions or a backplane like Redis."

**Server-side (Hub):**
```csharp
// Hub class
public class NotificationHub : Hub
{
    // Client calls this method
    public async Task SendMessage(string user, string message)
    {
        // Broadcast to all clients
        await Clients.All.SendAsync("ReceiveMessage", user, message);
        
        // Or send to specific client
        await Clients.Client(Context.ConnectionId).SendAsync("ReceiveMessage", user, message);
        
        // Or send to group
        await Clients.Group("Admins").SendAsync("ReceiveMessage", user, message);
    }
    
    // Called when client connects
    public override async Task OnConnectedAsync()
    {
        await Groups.AddToGroupAsync(Context.ConnectionId, "Admins");
        await base.OnConnectedAsync();
    }
    
    // Called when client disconnects
    public override async Task OnDisconnectedAsync(Exception exception)
    {
        await Groups.RemoveFromGroupAsync(Context.ConnectionId, "Admins");
        await base.OnDisconnectedAsync(exception);
    }
}

// Register in Program.cs
builder.Services.AddSignalR();
app.MapHub<NotificationHub>("/notificationHub");
```

**Client-side (JavaScript/TypeScript):**
```typescript
// Create connection
const connection = new signalR.HubConnectionBuilder()
    .withUrl("/notificationHub")
    .build();

// Start connection
connection.start()
    .then(() => console.log("Connected"))
    .catch(err => console.error(err));

// Listen for messages from server
connection.on("ReceiveMessage", (user, message) => {
    console.log(`${user}: ${message}`);
});

// Send message to server
connection.invoke("SendMessage", "John", "Hello");
```

**Client-side (.NET):**
```csharp
var connection = new HubConnectionBuilder()
    .WithUrl("https://localhost:5001/notificationHub")
    .Build();

await connection.StartAsync();

connection.On<string, string>("ReceiveMessage", (user, message) =>
{
    Console.WriteLine($"{user}: {message}");
});

await connection.InvokeAsync("SendMessage", "John", "Hello");
```

**Keywords:** SignalR hubs, connection, Clients.All, Clients.Client, Clients.Group

---

#### Q: What are SignalR connection groups?
**A:** **Groups** allow you to organize connections and send messages to specific subsets of clients.

**Use cases:**
- **Role-based notifications** - Send to "Admins" group
- **Room-based chat** - Send to "Room1" group
- **User-specific** - Send to user's connection group

**Example:**
```csharp
public class ChatHub : Hub
{
    // Join a room
    public async Task JoinRoom(string roomName)
    {
        await Groups.AddToGroupAsync(Context.ConnectionId, roomName);
        await Clients.Group(roomName).SendAsync("UserJoined", Context.UserIdentifier);
    }
    
    // Leave a room
    public async Task LeaveRoom(string roomName)
    {
        await Groups.RemoveFromGroupAsync(Context.ConnectionId, roomName);
        await Clients.Group(roomName).SendAsync("UserLeft", Context.UserIdentifier);
    }
    
    // Send message to room
    public async Task SendToRoom(string roomName, string message)
    {
        await Clients.Group(roomName).SendAsync("ReceiveMessage", message);
    }
}
```

**Keywords:** SignalR groups, Groups.AddToGroupAsync, role-based, room-based

---

#### Q: What transport methods does SignalR use?
**A:** SignalR automatically selects the best available transport:

**1. WebSockets** (best):
- Full-duplex communication
- Low latency
- Most efficient
- Requires WebSocket support

**2. Server-Sent Events (SSE)**:
- Server-to-client only
- Good fallback if WebSockets unavailable
- One-way communication

**3. Long Polling** (fallback):
- Works everywhere
- Less efficient
- Higher latency
- Used when WebSockets/SSE unavailable

**SignalR automatically:**
- Tries WebSockets first
- Falls back to SSE if WebSockets fail
- Falls back to Long Polling if SSE fails
- Upgrades to better transport when available

**Keywords:** SignalR transport, WebSockets, SSE, Long Polling, fallback

---

#### Q: How do you scale SignalR applications?
**A:** SignalR requires **sticky sessions** or **backplane** for scaling across multiple servers.

**Problem:**
- Multiple servers = multiple SignalR instances
- Client connects to Server A
- Server B can't send to that client

**Solutions:**

**1. Sticky Sessions (Session Affinity):**
- Route same client to same server
- Use load balancer with session affinity
- Simple but less flexible

**2. Backplane (Redis/SQL Server):**
- All servers connect to shared backplane
- Messages broadcast through backplane
- All servers can send to all clients

**Example with Redis:**
```csharp
// Program.cs
builder.Services.AddSignalR()
    .AddStackExchangeRedis("localhost:6379", options =>
    {
        options.Configuration.ChannelPrefix = "MyApp";
    });
```

**3. Azure SignalR Service:**
- Managed service
- Handles scaling automatically
- No backplane setup needed

**Keywords:** SignalR scaling, sticky sessions, backplane, Redis, Azure SignalR

---

#### Q: How do you handle authentication with SignalR?
**A:** SignalR integrates with ASP.NET Core authentication.

**Server-side:**
```csharp
// Require authentication
[Authorize]
public class NotificationHub : Hub
{
    // Access authenticated user
    public override async Task OnConnectedAsync()
    {
        var userId = Context.UserIdentifier; // From claims
        var userName = Context.User?.Identity?.Name;
        await base.OnConnectedAsync();
    }
}

// Register with authentication
app.MapHub<NotificationHub>("/notificationHub")
    .RequireAuthorization();
```

**Client-side:**
```typescript
// Include auth token
const connection = new signalR.HubConnectionBuilder()
    .withUrl("/notificationHub", {
        accessTokenFactory: () => {
            return getAuthToken(); // Your auth token
        }
    })
    .build();
```

**Keywords:** SignalR authentication, Authorize, Context.UserIdentifier, accessTokenFactory

---

## 🎯 COMMON INTERVIEW QUESTIONS

### Frontend

**Q: "Explain how React works"**  
**A:** "React uses a Virtual DOM - a JavaScript representation of the real DOM. When state changes, React creates a new Virtual DOM tree, compares it with the previous one, and updates only the changed parts in the real DOM. This is called reconciliation and makes React fast."

**Q: "How do you fetch data in React?"**  
**A:** "We use TanStack Query with Axios. TanStack Query handles caching, loading states, and refetching. Axios is the HTTP client that makes the actual API calls. We create client functions that use Axios, then React Query hooks that use those functions."

**Q: "What's the difference between Redux and TanStack Query?"**  
**A:** "Redux is for client-side state - things like user preferences, UI state. TanStack Query is for server state - data from APIs. Redux manages state in your app. TanStack Query fetches and caches data from your backend."

**Q: "When do you use Server Components?"**  
**A:** "Server Components render on the server and send zero JavaScript to the client. Use them for static data, no interactivity needed, heavy dependencies. But they require Next.js - in our Vite SPA, all components are client-side."

**Q: "What is Redux used for?"**  
**A:** "Redux is for client-side state management - things like user data, UI preferences, app-wide state. Important: Redux does NOT make API calls. API calls are done with Axios or TanStack Query."

---

### Backend

**Q: "What's the difference between .NET Framework and .NET?"**  
**A:** ".NET Framework is the legacy Windows-only platform from 2002. .NET is the current cross-platform platform that replaced it. .NET Framework is no longer actively developed - just security updates. For new projects, use .NET 8."

**Q: "What is CQRS?"**  
**A:** "CQRS separates read and write operations. Commands are writes - they change state, return IDs. Queries are reads - they retrieve data, don't change state. This allows optimizing reads and writes separately and scaling them independently."

**Q: "How do you optimize a slow SQL query?"**  
**A:** "First, check the execution plan for table scans - that means no index is being used. Create indexes on frequently queried columns and foreign keys. Make sure WHERE clauses don't use functions on columns. Select only needed columns. Use pagination. Check for N+1 queries and use Include() in EF Core."

**Q: "What is SignalR used for?"**  
**A:** "SignalR enables real-time communication - server can push updates to clients. It uses WebSockets when available, falls back to SSE or Long Polling. Common uses: live notifications, chat applications, live dashboards. It uses Hubs for communication."

**Q: "What are Commands and Queries in MediatR?"**  
**A:** "Commands are write operations - they change state and usually return an ID. Queries are read operations - they retrieve data and don't change state. This separation allows optimizing reads and writes separately."

**Q: "What are index trade-offs?"**  
**A:** "Indexes make reads much faster - queries can find rows quickly instead of scanning the table. But they slow down writes because every INSERT, UPDATE, DELETE must update the index. They also take storage space. Create indexes on frequently queried columns and foreign keys, but don't create too many."

---

## ⚠️ MISTAKES TO AVOID

**❌ "Redux is used to call APIs"**  
✅ **Correct:** "Redux is for state management. API calls use Axios or TanStack Query."

**❌ ".NET Framework is the latest version"**  
✅ **Correct:** ".NET Framework is legacy. .NET 8 is current."

**❌ "Server Components work in Vite"**  
✅ **Correct:** "Server Components require Next.js. In Vite, all components are client-side."

**❌ "Indexes always improve performance"**  
✅ **Correct:** "Indexes speed up reads but slow down writes. Balance is important."

**❌ "Virtual DOM is the real DOM"**  
✅ **Correct:** "Virtual DOM is a JavaScript representation. React uses it to optimize updates to the real DOM."

**❌ ".NET Core is still being developed"**  
✅ **Correct:** ".NET Core was merged into .NET 5+. Use .NET 8 now."

**❌ "CQRS is always needed"**  
✅ **Correct:** "CQRS is for complex scenarios. Simple CRUD apps don't need it."

---

## 📝 QUICK REFERENCE

### State Management Decision Tree
```
Need to store data?
├─ Server data (API) → TanStack Query
├─ Global client state → Zustand/Redux
└─ Local component state → useState
```

### Data Fetching Stack
```
Component
  ↓
useQuery/useMutation (TanStack Query)
  ↓
Client Function (entitiesClient)
  ↓
api.get/post (Axios)
  ↓
Backend API
```

### .NET Platform Timeline
```
2002: .NET Framework (Windows)
2016: .NET Core (Cross-platform)
2020: .NET 5 (Unified)
2023: .NET 8 (Current LTS)
```

### SQL Optimization Checklist
- [ ] Check execution plan (table scan = bad)
- [ ] Create indexes on frequently queried columns
- [ ] Index foreign keys
- [ ] Avoid functions in WHERE clauses
- [ ] Select only needed columns
- [ ] Use pagination
- [ ] Avoid N+1 queries (use Include)
- [ ] Update statistics regularly
- [ ] Monitor slow queries
- [ ] Check for unused indexes

### MediatR Pattern
```
Controller
  ↓ Send(command/query)
MediatR
  ↓ Routes to handler
Handler
  ↓ Processes request
Returns result
```

### SignalR Transport Priority
```
1. WebSockets (best)
2. Server-Sent Events (SSE)
3. Long Polling (fallback)
```

---

## 🎤 SPEAKING TIPS

1. **Start with the core concept** - "Redux is a state management library..."
2. **Mention what it's NOT** - "...but it doesn't make API calls"
3. **Give a simple example** - "Like storing user preferences..."
4. **Compare when relevant** - "Unlike TanStack Query which is for server state..."
5. **Be concise** - Aim for 30-60 second answers
6. **If you forget a name** - "The HTTP client library" instead of "Axios"
7. **Use keywords** - Helps interviewer understand you know the terminology
8. **Admit uncertainty** - "I'm not 100% sure, but I believe..." shows honesty

---

## 🔍 QUICK SEARCH GUIDE

**During interview, Ctrl+F for:**
- Topic name (e.g., "Redux", ".NET", "SignalR")
- Key concept (e.g., "state management", "API calls", "real-time")
- Comparison (e.g., "vs", "difference", "compare")
- Problem (e.g., "optimize", "slow", "performance")

**Common search terms:**
- "Redux" → State management, NOT API calls
- "Axios" → HTTP client, API requests
- "TanStack Query" → Server state, data fetching
- ".NET" → Current platform, cross-platform
- ".NET Framework" → Legacy, Windows only
- "MediatR" → Mediator pattern, CQRS
- "Commands" → Write operations, change state
- "Queries" → Read operations, retrieve data
- "Index" → Database performance, trade-offs
- "SignalR" → Real-time, WebSockets, hubs
- "Server Components" → Next.js, server-side rendering
- "Client Components" → Browser, hooks, interactions

---

**Last updated:** 2024  
**Use Ctrl+F to search for keywords during interviews!**  
**All answers are formatted for easy speaking - use as guide, not script!**
