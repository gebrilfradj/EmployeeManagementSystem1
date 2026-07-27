# Employee Management System

A full-stack Blazor Server application for tracking employee and intern records, built with ASP.NET Core and Entity Framework Core.

Originally built during downtime while interning at UPS, to give my supervisor a way to track the interns rotating through the team. It was handed over to my supervisors in my final week and has been in use since.

## Features

- **CRUD operations** — create, read, update, and delete employee records.
- **Audit logging** — every change to an employee record is written to an audit log, viewable in-app at `/auditlogs`.
- **Authentication and authorization** — ASP.NET Core Identity with role support, so only authorized staff can make changes.
- **Responsive UI** — Blazor Server components that work across desktop and mobile.
- **Seed data** — Bogus is used to generate realistic sample employees for local development.

## Technology stack

| Layer    | Technology                          |
| -------- | ----------------------------------- |
| UI       | Blazor Server (.NET 6)              |
| Backend  | ASP.NET Core 6                      |
| Auth     | ASP.NET Core Identity (with roles)  |
| ORM      | Entity Framework Core 6             |
| Database | Microsoft SQL Server                |

## Getting started

### Prerequisites

- [.NET 6 SDK](https://dotnet.microsoft.com/download/dotnet/6.0)
- SQL Server (LocalDB, Express, or a full instance)

### Setup

1. **Clone the repository**

   ```bash
   git clone https://github.com/gebrilfradj/employee-management-system.git
   cd employee-management-system
   ```

2. **Point the app at your SQL Server instance**

   Edit `EmployeeManagementSystem1/appsettings.json` and replace the `DefaultConnection` string with your own server:

   ```json
   "ConnectionStrings": {
     "DefaultConnection": "Server=(localdb)\\MSSQLLocalDB;Initial Catalog=EmployeeManagementSysDb;Integrated Security=True;TrustServerCertificate=True;"
   }
   ```

   > The database schema is created automatically on first run via `Database.EnsureCreated()` — there are no EF migrations to apply.

3. **Restore and run**

   ```bash
   dotnet restore
   dotnet run --project EmployeeManagementSystem1
   ```

4. **Open the app**

   Browse to the HTTPS URL printed in the console (typically `https://localhost:7xxx`). This is a single Blazor Server app — it hosts both the UI and the server-side logic, so there is no separate API to start.

## Project structure

```
EmployeeManagementSystem1/
├── Pages/         # Blazor pages: AddEmployee, EmployeesTable, EmployeeDetail, AuditLogs
├── Components/    # Reusable Blazor components
├── Services/      # EmployeeService — CRUD + audit log writes
├── Data/          # DataContext (EF Core DbContext)
├── Models/        # Employee and audit log entities
├── Areas/         # Identity UI
└── Shared/        # Layout and navigation
```

## Notes

- Identity password requirements are intentionally relaxed for internal use (minimum 5 characters, no complexity rules). Tighten these in `Program.cs` before any public deployment.
- `appsettings.json` is committed with a local development connection string; use user secrets or environment variables for real credentials.

## License

No license has been specified yet. Consider adding one (MIT is a common choice) if you want others to be able to reuse this code.
