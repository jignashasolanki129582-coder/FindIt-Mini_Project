# FindIt – Campus Lost & Found Portal

## Stack
ASP.NET MVC 5, C#, .NET Framework 4.8, SQL Server LocalDB, ADO.NET (`System.Data.SqlClient`), Razor, Bootstrap 5.

## Prerequisites
- Windows 10/11
- Visual Studio 2022 with **ASP.NET and web development** workload and .NET Framework 4.8 targeting pack
- SQL Server Express LocalDB; SSMS recommended

## Setup
1. Extract ZIP and open `FindIt.sln` in Visual Studio 2022.
2. Restore NuGet packages (MVC 5.2.9, Razor/WebPages 3.2.9). If package restore fails, right-click solution → Restore NuGet Packages.
3. In SSMS connect to `(localdb)\MSSQLLocalDB` using Windows Authentication.
4. Open and execute `Database/FindItDB.sql`. It creates `findit_db` and schema.
5. Confirm `Web.config` connection string: `Data Source=(LocalDB)\MSSQLLocalDB;Initial Catalog=findit_db;Integrated Security=True;Connect Timeout=30`.
6. Build → Build Solution, then run with IIS Express.
7. Register a normal account in the portal. To make the first admin, run in SSMS after registration (substitute your email): `UPDATE dbo.Users SET Role='Admin' WHERE Email='your-admin-email@example.edu';` Sign out and sign in again.
8. Students can register, browse, report lost/found items, upload images, and submit claims. Admin can manage users, reports, and claims.

## Security notes
Passwords use PBKDF2 with per-password random salt (150,000 iterations); no plaintext stored. SQL is parameterized. Uploads are restricted by extension, size, and basic file signature; generated names are used. Student/admin checks are server-side session checks. Approval runs within a transaction and marks competing pending claims rejected.

## Known limitations / testing disclosure
This source package was generated in a non-Windows environment. Visual Studio compilation, IIS Express execution, and SQL LocalDB script execution could not be run here. Review and test these on Windows before submission. Image signature checks are intentionally conservative but WEBP signature validation should be reviewed (RIFF/WEBP structure). MVC NuGet restore and project-file compatibility should be confirmed in VS2022. This is not certified error-free.
