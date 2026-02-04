# Jabotio – Modern E-commerce Admin Dashboard

**A clean, fast, and scalable admin panel for managing e-commerce stores**

Built with **Next.js 14** • **TypeScript** • **Tailwind CSS** • **shadcn/ui** • **REST API**

[![Next.js](https://img.shields.io/badge/Next.js-14-black?style=for-the-badge&logo=next.js&logoColor=white)](https://nextjs.org)
[![Tailwind](https://img.shields.io/badge/Tailwind_CSS-3.4-38bdf8?style=for-the-badge&logo=tailwindcss)](https://tailwindcss.com)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.x-3178c6?style=for-the-badge&logo=typescript&logoColor=white)](https://typescriptlang.org)
[![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)](https://opensource.org/licenses/MIT)

---

## 📖 Table of Contents

- [✨ Features](#-features)
- [🛠 Tech Stack](#-tech-stack)
- [🚀 Quick Start](#-quick-start)
- [📁 Project Structure](#-project-structure)
- [🔐 Authentication](#-authentication)
- [📊 API Routes](#-api-routes)
- [🌐 Environment Variables](#-environment-variables)
- [🎨 UI Components](#-ui-components)
- [📱 Pages Overview](#-pages-overview)
- [🔄 State Management](#-state-management)
- [🧪 Testing](#-testing)
- [⚡ Performance Optimization](#-performance-optimization)
- [🚀 Deployment](#-deployment)
- [🤝 Contributing](#-contributing)
- [📄 License](#-license)

---

## ✨ Features

Jabotio provides everything needed for modern e-commerce store management:

### Core Features
* **Responsive UI** – Fully optimized for Desktop, Tablet, and Mobile devices with a mobile-first approach
* **Secure Authentication** – JWT-based session management with HTTP-only cookies and refresh token rotation
* **Product Management** – Complete CRUD operations with image uploads, categories, variants, and inventory tracking
* **Order Management** – Real-time order tracking with status updates, filtering, search, and bulk actions
* **Analytics Dashboard** – Interactive charts displaying revenue trends, sales metrics, customer growth, and conversion rates
* **Customer Management** – View customer profiles, purchase history, and engagement analytics
* **Theme Support** – Seamless Dark/Light mode with system preference detection
* **Form Validation** – Robust client and server-side validation using Zod schemas
* **Search & Filter** – Advanced filtering and search capabilities across all data tables
* **Export Data** – Export orders, products, and reports to CSV/Excel formats
* **Role-Based Access** – Multi-level user permissions (Admin, Manager, Viewer)
* **Notifications** – Real-time toast notifications for all user actions
* **Internationalization** – Multi-language support ready (i18n infrastructure)
* **File Upload** – Drag-and-drop file uploads with preview and validation
* **API Documentation** – Auto-generated API docs with Swagger/OpenAPI
* **Performance Monitoring** – Built-in analytics and error tracking integration

---

## 🛠 Tech Stack

| Category | Technology | Purpose |
|:---------|:-----------|:--------|
| **Framework** | Next.js 14 (App Router) | React framework with server components |
| **Language** | TypeScript 5.x | Type-safe development |
| **Styling** | Tailwind CSS 3.4 | Utility-first CSS framework |
| **UI Components** | shadcn/ui | Accessible, customizable components |
| **State Management** | React Context + TanStack Query | Global state and server state caching |
| **Data Fetching** | TanStack Query (React Query) | Async state management with caching |
| **Forms** | React Hook Form | Performant form handling |
| **Validation** | Zod | Schema validation for forms and API |
| **Charts** | Recharts | Data visualization and analytics |
| **Icons** | Lucide React | Modern icon library |
| **Date Handling** | date-fns | Date manipulation and formatting |
| **Tables** | TanStack Table | Powerful data table solution |
| **Authentication** | JWT + HTTP-only Cookies | Secure token-based auth |
| **Database** | PostgreSQL / MongoDB | Relational or NoSQL database |
| **ORM** | Prisma / Mongoose | Database abstraction layer |

---

## 🚀 Quick Start

### Prerequisites

Ensure you have the following installed:
- Node.js 18.x or higher
- npm 9.x or yarn 1.22.x
- Git

### 1. Clone & Install
```bash
