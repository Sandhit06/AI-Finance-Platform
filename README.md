# AI Finance Platform

A full-stack AI-powered finance management platform built with **Next.js**, **Supabase**, **Prisma**, **Tailwind CSS**, **Shadcn UI**, **Clerk**, **Inngest**, **ArcJet**, and **Resend**.

The app is designed to help users **manage accounts, track income and expenses, scan receipts, handle recurring transactions, and visualize financial activity** in a clean, modern interface.

<img width="1470" alt="Screenshot 2024-12-10 at 9 45 45 AM" src="https://github.com/user-attachments/assets/1bc50b85-b421-4122-8ba4-ae68b2b61432">

---

## Overview

**AI Finance Platform** is a personal finance SaaS application that combines traditional financial tracking with AI-assisted workflows.  
It allows users to create accounts, add transactions, categorize spending, and analyze their money flow from a centralized dashboard.

The platform focuses on:

- **Ease of financial tracking**
- **Automation through AI**
- **Secure authenticated workflows**
- **Clean and scalable full-stack architecture**

---

## Key Features

### 1. User Authentication
- Secure sign-in and sign-up flows powered by **Clerk**
- Protected routes for authenticated users
- User-specific dashboards and actions
- Seamless user session handling

### 2. Account Management
- Create and manage multiple financial accounts
- Support for account types like **Current** and **Savings**
- Set a default account for faster transaction entry
- Track balances per account

### 3. Transaction Management
- Add **income** and **expense** transactions
- Edit existing transactions
- Link transactions to specific accounts
- Categorize spending for better budgeting
- Support for recurring transactions
- Date-based transaction entry and updates

### 4. AI-Assisted Receipt Scanning
- Scan receipts to auto-fill transaction data
- Reduce manual entry for amounts, descriptions, dates, and categories
- Improve transaction capture speed and accuracy

### 5. Dashboard & Financial Overview
- Central dashboard for viewing financial data
- Account-level and transaction-level insights
- Visual structure ready for charts and analytics
- Designed for quick money management at a glance

### 6. Notifications & Email
- Transactional email support using **Resend**
- Useful for onboarding, alerts, and user communication
- Server-side email action for secure delivery

### 7. Background Workflows
- Async task orchestration using **Inngest**
- Built-in retry strategy for reliability
- Suitable for workflows like notifications, processing, and automation

### 8. Security & Protection
- **ArcJet** for request protection and abuse prevention
- Rate limiting and safety measures for a finance-oriented app

---

## Architecture

                      ┌──────────────────────┐
                      │      Clerk Auth      │
                      │    Arcjet Security   │
                      └──────────┬───────────┘
                                 │
                                 ▼
                      ┌──────────────────────┐
                      │     Next.js 15       │
                      │     App Router       │
                      │                      │
                      │ React / Shadcn UI    │
                      │ React Hook Form      │
                      │ Zod Validation       │
                      └──────────┬───────────┘
                                 │
             ┌───────────────────┼───────────────────┐
             │                   │                   │
             ▼                   ▼                   ▼
   ┌──────────────────┐ ┌────────────────┐ ┌──────────────────┐
   │  Server Actions  │ │ Inngest Jobs   │ │  Google Gemini   │
   │                  │ │                │ │                  │
   │ Accounts         │ │ Recurring Txns │ │ Receipt Scanning │
   │ Transactions     │ │ Budget Alerts  │ │ AI Insights      │
   │ Budgets          │ │ Monthly Report │ │                  │
   └────────┬─────────┘ └───────┬────────┘ └──────────────────┘
            │                   │
            │                   └──────────────┐
            │                                  │
            ▼                                  ▼
   ┌──────────────────┐               ┌─────────────────┐
   │     Prisma       │               │     Resend      │
   │       ORM        │               │  Email Service  │
   └────────┬─────────┘               └─────────────────┘
            │
            ▼
   ┌──────────────────┐
   │    PostgreSQL    │
   │     Supabase     │
   └──────────────────┘

## Tech Stack

### Frontend
- **Next.js** — App Router-based full-stack React framework
- **React** — UI component model
- **Tailwind CSS** — Utility-first styling
- **Shadcn UI** — Reusable, accessible UI components
- **Lucide React** — Icon library

### Backend / Data
- **Supabase** — Backend infrastructure and PostgreSQL database
- **Prisma** — Type-safe database ORM
- **Next.js Server Actions** — Secure server-side mutations
- **Inngest** — Event-driven background jobs

### Authentication / Security
- **Clerk** — Authentication and user management
- **ArcJet** — Security, protection, and rate limiting

### Forms / Validation
- **React Hook Form** — Form handling
- **Zod** — Schema validation
- **@hookform/resolvers** — Resolver integration

### Notifications / Email
- **Resend** — Email delivery

### Utilities
- **date-fns** — Date formatting and manipulation
- **sonner** — Toast notifications

---

## Architecture Highlights

### Next.js App Router
The project uses the modern **App Router** structure, which enables:
- Server Components
- Client Components
- Route groups
- Nested layouts
- Server Actions

This creates a cleaner separation between rendering logic and mutation logic.

### Server and Client Component Split
The repo uses:
- **Server components** for authenticated and data-driven pages
- **Client components** for interactive forms, drawers, and UI controls

This improves performance while keeping the UI interactive where needed.

### Server Actions
Critical actions like:
- creating transactions
- updating transactions
- creating accounts
- sending emails

are handled on the server for security and reliability.

### Form Validation
Forms are built using:
- **React Hook Form** for state management
- **Zod** for schema validation

This gives strong runtime validation and a better developer experience.

### Background Processing
**Inngest** is used for asynchronous, event-driven workflows with retry support.  
This is useful for jobs that should not block the main request-response cycle.

### Theming and Design System
The app uses:
- Tailwind CSS
- CSS variables
- Dark mode support
- Shadcn UI primitives

This makes the UI consistent, themeable, and maintainable.

---

## Project Structure

A simplified view of the repository structure:

```bash
app/
  ├── (main)/
  │   ├── transaction/
  │   │   └── _components/
  │   │       └── transaction-form.jsx
  │   └── ...
  ├── globals.css
  ├── page.js
  └── ...
actions/
  └── send-email.js
components/
  ├── header.jsx
  ├── create-account-drawer.jsx
  └── ...
lib/
  └── inngest/
      └── client.js
tailwind.config.js
components.json
```

### Notable folders
- **`app/`** — application routes and pages
- **`components/`** — reusable UI components
- **`actions/`** — server actions for business logic
- **`lib/`** — shared utilities and integrations
- **`hooks/`** — reusable client hooks
- **`app/lib/`** — schemas and app-specific utilities

---

## Environment Variables

Create a `.env` file in the project root with the following variables:

```env
DATABASE_URL=
DIRECT_URL=

NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY=
CLERK_SECRET_KEY=
NEXT_PUBLIC_CLERK_SIGN_IN_URL=/sign-in
NEXT_PUBLIC_CLERK_SIGN_UP_URL=/sign-up
NEXT_PUBLIC_CLERK_AFTER_SIGN_IN_URL=/onboarding
NEXT_PUBLIC_CLERK_AFTER_SIGN_UP_URL=/onboarding

GEMINI_API_KEY=

RESEND_API_KEY=

ARCJET_KEY=
```

### Environment variable purpose

- **`DATABASE_URL`** — Main database connection string
- **`DIRECT_URL`** — Direct database connection for Prisma
- **`NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY`** — Clerk frontend auth key
- **`CLERK_SECRET_KEY`** — Clerk backend auth key
- **`NEXT_PUBLIC_CLERK_SIGN_IN_URL`** — Sign-in page route
- **`NEXT_PUBLIC_CLERK_SIGN_UP_URL`** — Sign-up page route
- **`NEXT_PUBLIC_CLERK_AFTER_SIGN_IN_URL`** — Redirect after sign-in
- **`NEXT_PUBLIC_CLERK_AFTER_SIGN_UP_URL`** — Redirect after sign-up
- **`GEMINI_API_KEY`** — AI integration key for smart features
- **`RESEND_API_KEY`** — Email delivery service key
- **`ARCJET_KEY`** — Security/protection key

---

## Getting Started

### 1. Clone the repository
```bash
git clone https://github.com/Sandhit06/AI-Finance-Platform.git
cd AI-Finance-Platform
```

### 2. Install dependencies
```bash
npm install
# or
yarn install
# or
pnpm install
```

### 3. Configure environment variables
Create a `.env` file and add the required values listed above.

### 4. Set up the database
Make sure your Supabase/PostgreSQL database is available and Prisma is configured correctly.

Run Prisma commands as needed:

```bash
npx prisma generate
npx prisma migrate dev
```

### 5. Start the development server
```bash
npm run dev
```

Open the app in your browser:

```bash
http://localhost:3000
```

---

## How It Works

1. A user signs in using Clerk
2. The user creates or selects a financial account
3. The user adds income or expense transactions
4. Receipt scanning can auto-fill transaction fields
5. Data is saved through server actions and Prisma
6. The dashboard reflects updated financial information
7. Background tasks can run through Inngest
8. Emails can be sent using Resend

---

## Design Principles

This project is built around a few key engineering ideas:

- **User-first UX** — minimize friction when tracking money
- **Secure-by-default** — protect user data and routes
- **Modular architecture** — separate UI, actions, schemas, and integrations
- **Scalability** — use background jobs and server actions for clean growth
- **Modern frontend patterns** — App Router, Server Components, and composable UI

---

## Interview Highlights

If you’re presenting this project in an interview, these are the strongest points to mention:

- Built a **full-stack SaaS-style finance application**
- Integrated **authentication, database, server actions, and background jobs**
- Implemented **AI-assisted receipt scanning** to reduce manual data entry
- Designed a **scalable architecture** with Next.js App Router and server/client component separation
- Used **Prisma + Supabase** for a type-safe and scalable data layer
- Added **transactional emails** and **security protections** for production readiness
- Focused on **UX, reliability, and maintainability**

### Example interview summary
> “I built a full-stack AI finance platform that helps users manage accounts and transactions, scan receipts, and analyze spending. The app uses Next.js, Clerk, Prisma, Supabase, Inngest, ArcJet, and Resend, with a UI built in Tailwind and Shadcn. It combines secure authentication, server actions, background workflows, and AI-assisted data entry into a production-style personal finance product.”

---

## Future Improvements

Potential next enhancements could include:
- Budget planning and spending goals
- Advanced charts and analytics
- Export to CSV/PDF
- Automated recurring bill detection
- Multi-currency support
- Investment tracking
- Push notifications
- More AI-driven financial insights

---

## License

This project does not currently include a license file.  
Add one if you plan to open source or distribute the project publicly.

---

## Acknowledgements

Built as a modern full-stack finance platform using the following ecosystem:
- Next.js
- Supabase
- Prisma
- Clerk
- Inngest
- ArcJet
- Tailwind CSS
- Shadcn UI
- Resend
- Gemini AI

## Developer
<table>
    <tr align="center">
        <td>
        Sandhit Karmakar
        <p align="center">
            <img src = "https://avatars.githubusercontent.com/u/90787826?v=4" width="150" height="150" alt="Dhruv Shah">
        </p>
            <p align="center">
                <a href="https://github.com/Sandhit06">
                    <img src="https://api.iconify.design/mdi:github.svg?color=%230088cc" width="36" height="36" alt="GitHub"/>
                </a>
                <a href="https://www.linkedin.com/in/sandhit-karmakar/" target="_blank">
                    <img src="https://api.iconify.design/mdi:linkedin.svg?color=%230088cc" width="36" height="36" alt="LinkedIn"/>
                </a>
                <a href="mailto:sandhitkarmakar@gmail.com" target="_blank">
                    <img src="https://api.iconify.design/mdi:email.svg?color=%230088cc" width="36" height="36" alt="Email"/>
                </a>
            </p>
        </td>
    </tr>
</table>

<p align="center">
    Made with ❤️ by <a href="https://github.com/Sandhit06">Sandhit Karmakar</a>
</p>
