# Sliding Grid Game - Product Specification

[Reference Link](https://play.google.com/store/apps/details?id=com.dopuz.klotski.riddle&hl=en_IN&pli=1)



https://github.com/user-attachments/assets/869930cf-3375-41bb-a705-8ef20833a481



## Overview
A web-based sliding puzzle implementation where elements can only move into a single empty cell position. Movement direction is determined by the position of the empty cell relative to each element. The application consists of a dashboard for puzzle creation and a client interface for puzzle solving.

## Core Components

### 1. Dashboard (/dashboard)

#### Grid Creation Module
- Input fields for grid dimensions (M rows, N columns)
- Validation to ensure dimensions are positive integers
- Grid size limits: Min 2x2, Max 10x10
- Cell dimension controls:
  - Width input (pixels)
  - Height input (pixels)
  - Preview updates dynamically with dimension changes

#### Element Population Module
- Manual number entry per cell
- One cell must always remain empty
- Element constraints:
  - Only positive integers allowed
  - Each number must be unique within the grid
  - Exactly one empty cell in the grid

#### Evaluation Configuration
- Text area for evaluation function input
- Function receives current grid state
- Returns boolean (true/false)
- Example:
  ```javascript
  function evaluate(grid) {
    const flatGrid = grid.flat().filter(x => x !== null);
    return flatGrid.every((num, i) => i === 0 || num > flatGrid[i - 1]);
  }
  ```

#### Storage
- Save configurations to local storage
- Generate unique puzzle ID
- List of saved puzzles with links

### 2. Client Interface (/puzzle/:id)

#### Grid Display
- Renders grid with specified cell dimensions
- Elements sized according to dashboard configuration
- Clear visual distinction of the empty cell

#### Movement System
- Drag and drop functionality
- Movement rules:
  - Elements can only move into the empty cell position
  - Only elements adjacent to empty cell can be moved
  - Movement is automatically determined by empty cell position:
    - If empty cell is above/below: Vertical movement only
    - If empty cell is left/right: Horizontal movement only
  - Invalid movements prevented by drag constraints
- Smooth animation for successful moves

#### Game State
- Submit button to check solution
- Clear success/failure message
- Reset puzzle option

## User Stories

### Dashboard
1. Admin can create grid with custom cell dimensions
2. Admin can input numbers, ensuring one empty cell
3. Admin can input evaluation function
4. Admin can save and manage puzzles

### Client
1. User can load puzzles by ID
2. User can drag elements into empty cell position
3. User can submit solution for verification
4. User can reset puzzle
