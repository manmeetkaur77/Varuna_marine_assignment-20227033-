#  AI Agent Workflow Log  

##  Agents Used  

During the development of the **FuelEU Maritime Compliance Dashboard**, I worked with several AI tools to streamline both frontend and backend development:  

- **ChatGPT (GPT-5)** – My primary debugging and explanation assistant. I used it to identify and resolve frontend errors, backend route mismatches, and Prisma integration bugs.  
- **Claude Code (Sonnet 4.5)** – Used mainly for reviewing and refining generated code. It helped simplify logic, clean up TypeScript syntax, and validate ChatGPT’s responses.  
- **GitHub Copilot** – Provided quick inline code completions while writing repetitive React components or Express controller logic.  
- **Cursor Agent** – Useful for quickly scaffolding new files such as repositories, controller layers, and hook structures, saving significant setup time.  

---

##  Prompts & Outputs  

### Example 1 – Frontend Import Error  

**Prompt:**  
> “Uncaught SyntaxError: The requested module '/src/adapters/infrastructure/apiClient.ts' does not provide an export named 'API'. Can you fix this?”  

**ChatGPT’s Output:**  
```ts
// src/adapters/infrastructure/apiClient.ts
const API_BASE = "http://localhost:3000/api";

async function getRoutes() {
  const res = await fetch(`${API_BASE}/routes`);
  if (!res.ok) throw new Error("Failed to fetch routes");
  return res.json();
}

export const API = { getRoutes };
```

**Result:**  
After updating the file as suggested, the error disappeared, and the frontend successfully fetched route data from the backend.  

---

###  Example 2 – Blank Frontend Screen  

**Prompt:**  
> “My frontend shows a blank page after running. Can you help me debug it?”  

**ChatGPT’s Process:**  
- Checked for missing hook files (`useBanking`, `useCompare`, `usePooling`) and guided me to create them.  
- Suggested adding a default redirect route to App.tsx:  
  ```tsx
  <Route path="/" element={<Navigate to="/routes" replace />} />
  ```  
- Identified and corrected UTF-8 encoding issues (✅ instead of âœ…, 🚢 instead of ðŸš¢).  

**Claude Code’s Review:**  
Claude optimized the same code by improving type safety and cleaning up unnecessary `as any` usage.  

✅ **Result:**  
The app rendered correctly after implementing these changes.  

---

### Example 3 – Backend 404 Error  

**Prompt:**  
> “Getting 404 when calling /api/routes. Can you help me trace the issue?”  

**ChatGPT’s Suggestion:**  
Found that the routes were not prefixed with `/api` in the Express app.  
```js
app.use("/api/routes", routesRouter);
```

**Result:**  
After adding the prefix, testing with Postman confirmed that the routes responded correctly.  

---

## Validation & Corrections  

Each AI-generated output was verified through:  
- **Postman API Testing** – checked GET and POST endpoints manually.  
- **React Developer Tools** – verified rendering and state updates.  
- **psql CLI** – confirmed database writes using direct SQL queries.  
- **Cross-checking AI responses** – compared ChatGPT and Claude suggestions before final implementation.  

I always reviewed the generated code before committing to avoid introducing logical errors.  

---

## 🔍 Observations  

###  Where AI Helped  
- Reduced setup time for repetitive files (controllers, repositories).  
- Helped catch missing or mismatched imports.  
- Simplified debugging with clear step-by-step guidance.  
- Made TypeScript and Prisma usage cleaner and more consistent.  

### Where AI Struggled  
- Sometimes suggested incorrect file paths or outdated syntax.  
- Added redundant CORS and middleware configurations.  
- Mixed frontend and backend logic in a few explanations.  

### How I Combined Tools  
- **ChatGPT** → architecture, debugging, documentation.  
- **Claude Code** → refining and reviewing generated logic.  
- **Cursor** → scaffolding new code modules quickly.  
- **Copilot** → generating boilerplate and inline JSX/Express handlers.  

Together, they created an efficient, complementary workflow.  

---

## Best Practices Followed  

- Used **Cursor’s `tasks.md`** to plan and track prompt tasks.  
- Verified every AI output manually before merging.  
- Limited Copilot’s use to small, predictable completions.  
- Avoided copy-pasting large blocks of code without review.  
- Maintained consistent code formatting and TypeScript conventions.  

---

## Summary  

Using AI coding assistants significantly accelerated the project’s development while maintaining code quality.  
Each agent had a defined purpose — **ChatGPT for debugging**, **Claude for refinement**, **Copilot for boilerplate**, and **Cursor for setup**.  

The key success factor was maintaining **human control** over the workflow: validating every suggestion, testing APIs manually, and combining insights from multiple tools.  
This approach ensured the final product was accurate, maintainable, and aligned with project goals.  
