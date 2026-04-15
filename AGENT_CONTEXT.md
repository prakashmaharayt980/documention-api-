# Agent Memory Context

This document serves as a context memory for the AI agent working on the **Fatafatsewa** project. It outlines the project structure, design system, responsive guidelines, and data conventions to ensure smooth development.

## 1. Paths & Project Structure

*   **Root Directory**: `/home/kalihouse/Desktop/FatProj/Fatafatsewa`
*   **Source Code**: `src/`
    *   **App Router**: `src/app/` (Next.js 16+ App Router)
    *   **Components**: `src/components/` (Reusable UI components)
    *   **UI Primitives**: `src/components/ui/` (likely Shadcn/Radix primitives)
    *   **Hooks**: `src/hooks/`
    *   **Utilities**: `src/lib/` (contains `utils.ts` with `cn` helper)
    *   **API Routes**: `src/app/api/`
    *   **Mock Data**: `src/apijsonexample/`
*   **Public Assets**: `public/` (Images, SVGs, Favicons)
*   **Configuration**:
    *   `next.config.ts`
    *   `package.json`
    *   `src/app/globals.css` (Tailwind & Theme definition)

## 2. Networking & Context ("Nowinking")

*   **Framework**: Next.js 16.1.3
*   **HTTP Client**: `axios` (v1.10.0) is installed. `swr` is also available for data fetching.
*   **API Response Structure**:
    Standard response format based on mock data:
    ```json
    {
        "success": true,
        "message": "Success",
        "data": { ... }
    }
    ```
*   **Authentication**: `next-auth` is not explicitly seen, but `@react-oauth/google` and `@greatsumini/react-facebook-login` are present.

## 3. Colour Theme & Design System

Defined in `src/app/globals.css` using CSS variables and Tailwind v4 `@theme`.

### Primary Colors
*   **Blue (Brand)**: `#1f67b7` (`--colour-bg1`, `--colour-fsP2`)
*   **Dark Blue**: `#0474BA` (`--colour-btn1`, `--colour-text1`)
*   **Yellow/Orange (Accent)**: `#FF9107` (`--colour-yellow`, `--colour-btn2`)
*   **Green**: `#0F6600` (`--colour-bg3`)

### Premium Design System
*   **Blue**: `#007BFF` (`--premium-blue`)
*   **Slate**: `#2C3E50` (`--premium-slate`)
*   **Glassmorphism**:
    *   `--glass-bg`: `rgba(255, 255, 255, 0.8)`
    *   `--glass-border`: `rgba(255, 255, 255, 0.18)`
    *   Utility class: `.glass`, `.glass-premium`

### Fonts
*   `--font-heading`: `'Inter', sans-serif` (Default body font)
*   `--font-dm-sans`: "DM Sans"
*   `--font-poppins`: "Poppins"

## 4. Responsiveness

*   **Breakpoints**: Standard Tailwind (`sm`, `md`, `lg`, `xl`, `2xl`).
*   **Custom Utilities** (using `clamp()` for fluid sizing):
    *   `.text-responsive`: Font size `0.875rem` to `1rem`.
    *   `.text-responsive-lg`: Font size `1.125rem` to `1.5rem`.
    *   `.space-responsive`: Gap `0.5rem` to `1rem`.
    *   `.container-responsive`: Fluid padding.
*   **Visibility Classes**:
    *   `.mobile-hidden` (Hidden on max-width 640px)
    *   `.tablet-hidden` (Hidden between 641px and 1024px)
    *   `.desktop-hidden` (Hidden on min-width 1025px)

## 5. Images (Img)

*   **Location**: `public/` folder.
*   **Subdirectories**: `public/imgfile/`, `public/svgfile/`.
*   **Usage**: Use absolute paths starting with `/`. E.g., `/imgfile/banner.jpg`.
*   **Component**: Prefer `next/image` for optimization.

## 6. Mock Data Record

*   **Purpose**: Temporary data for development, to be removed later.
*   **Location**: `src/apijsonexample/`
*   **Files**:
    *   `productDetails.json`: Detailed single product view.
    *   `productserach.json`: Search results.
    *   `productbyCategory.json`: Category listing.
*   **Example Structure** (`productDetails.json`):
    ```json
    {
      "success": true,
      "message": "Success",
      "data": {
        "id": 4785,
        "name": "OnePlus 15...",
        "price": 169999,
        "discounted_price": 159999,
        "image": {
            "full": "https://fatafatsewa.com/storage/media/...",
            "thumb": "..."
        },
        "attributes": { ... }
      }
    }
    ```

---
*Created by Agent Antigravity on 2026-02-10.*
