# Library Management System

A modern library management application built with Next.js, React, TypeScript, and Tailwind CSS using shadcn/ui components.

## Starting the Project

Students should first follow the experiment guide to proceed with the project

- [Experiment 3 Guide](https://github.com/cu-fs1#experiment-3)

## Installation

```bash
# Install dependencies
pnpm install

# Add shadcn components (if needed)
pnpm dlx shadcn@latest add button input card
```

## Overview

This application allows users to manage a collection of books with features including:

- **Search**: Filter books by title or author
- **Add**: Add new books with title and author
- **Edit**: Modify existing book information
- **Remove**: Delete books from the collection

## Getting Started

First, run the development server:

```bash
pnpm dev
```

Open [http://localhost:3000](http://localhost:3000) with your browser to see the application.

## Project Structure

```text
.
├── app/
│   ├── favicon.ico
│   ├── globals.css
│   ├── layout.tsx
│   └── page.tsx
├── components/
│   ├── ui/
│   │   ├── button.tsx
│   │   ├── card.tsx
│   │   └── input.tsx
│   └── library-button.tsx
├── lib/
│   └── utils.ts
├── public/
│   ├── file.svg
│   ├── globe.svg
│   ├── next.svg
│   ├── vercel.svg
│   └── window.svg
├── components.json
├── eslint.config.mjs
├── next.config.ts
├── package.json
├── pnpm-lock.yaml
├── pnpm-workspace.yaml
├── postcss.config.mjs
├── README.md
└── tsconfig.json
```

### File: `app/page.tsx`

This is the main page component that manages the entire application state and UI.

#### Key Components:

**State Management:**

- `query`: Stores the search input value
- `title` & `author`: Temporary states for the "Add Book" form
- `books`: Array of all books in the library
- `editingId`: Tracks which book is currently being edited (null if none)
- `editTitle` & `editAuthor`: Stores the edited values temporarily

**Data Structure:**

```typescript
type Book = {
  id: number; // Unique numeric ID using Date.now() (millisecond timestamp)
  title: string; // Book title
  author: string; // Author name
};
```

#### Key Functions:

**1. `filteredBooks`**

- Computed value that filters books based on search query
- Searches both title and author fields (case-insensitive)
- Returns all books if search query is empty
- Recalculates on every render when `query` or `books` change

**2. `handleAdd()`**

- Validates that both title and author are not empty
- Uses `Date.now()` to generate a unique numeric ID based on the current timestamp in milliseconds
- Prepends new book to the books array
- Clears the input fields after adding

**3. `handleRemove(id)`**

- Filters out the book with matching numeric ID
- Updates the books array

**4. `handleEdit(book)`**

- Sets the book ID as currently editing
- Populates edit form fields with current book data

**5. `handleSaveEdit(id)`**

- Validates edited title and author are not empty
- Updates the specific book in the array with new values using the numeric ID
- Clears editing state and form fields

**6. `handleCancelEdit()`**

- Exits edit mode without saving changes
- Clears all edit-related state

#### UI Structure:

1. **Header**: Displays the application title
2. **Input Section**:
   - Search bar for filtering books
   - Form with title and author inputs
   - Add Book button (blue)
3. **Books Display**:
   - Shows filtered books in cards
   - Each card displays book title and author
   - Edit and Remove buttons (amber and red respectively)
   - Edit mode: Shows input fields with Save/Cancel buttons
   - Empty state: Shows message when no books match search

### File: `components/library-button.tsx`

A reusable button component that applies consistent styling based on the button type.

#### Props:

```typescript
type LibraryButtonProps = {
  onClick: () => void; // Callback function when button is clicked
  variant: "add" | "remove" | "edit"; // Button type (determines color)
  children: React.ReactNode; // Button label/content
};
```

#### Variants:

1. **`add` (Blue)**:
   - Background: `bg-blue-600`
   - Hover: `hover:bg-blue-700`
   - Used for: Add Book, Save buttons

2. **`remove` (Red)**:
   - Background: `bg-red-600`
   - Hover: `hover:bg-red-700`
   - Used for: Remove, Cancel buttons

3. **`edit` (Amber)**:
   - Background: `bg-amber-600`
   - Hover: `hover:bg-amber-700`
   - Used for: Edit button

#### Features:

- Uses `cn()` utility from shadcn to conditionally apply styles
- Consistent white text color across all variants
- Cursor pointer on hover for better UX
- Simplified button creation throughout the app

## Technologies Used

- **Next.js 16+**: React framework
- **React 19+**: UI library
- **TypeScript**: Type safety
- **Tailwind CSS**: Utility-first CSS framework
- **shadcn/ui**: Component library (Button, Card, Input)
- **pnpm**: Package manager

## Components Used

- **Button**: Base button component from shadcn/ui
- **Card**: Container component from shadcn/ui
- **Input**: Text input field from shadcn/ui
- **LibraryButton**: Custom button wrapper with variant support

## How It Works

### Adding a Book:

1. User enters title and author in the input fields
2. Clicks "Add Book" button
3. `handleAdd()` validates and creates new book entry
4. Book is prepended to the list

### Searching Books:

1. User types in the search field
2. `filteredBooks` automatically updates based on query
3. List re-renders showing only matching books

### Editing a Book:

1. User clicks "Edit" button on a book card
2. Card switches to edit mode with input fields pre-filled
3. User modifies title and/or author
4. Clicks "Save" to confirm or "Cancel" to discard changes

### Removing a Book:

1. User clicks "Remove" button
2. `handleRemove()` filters out the book
3. List updates immediately

## Development

The app uses React hooks for state management:

- `useState`: For local state (input values, editing mode)

The component is marked as `"use client"` to enable React hooks in Next.js App Router.
