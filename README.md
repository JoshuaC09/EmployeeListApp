follow this step by step to fully understand and run the application

To Start use this repository clone it first after you clone open the "Employee.List.App.Client" folder find and open  "EmployeeListApp.Client.sln" solution
after opening to the visual studion code  at the top of the buttons fine "Tools" find " Nuget Package Manager" under that button find and click Package Manager solution

Change first the default project to "EmployeeListApp.DataAccess"
before running this command

" Add-Migration <NameOfMigration> "
Update-Database

Or run this if cannot find change project default.
"Add-Migration <NameOfMigration> -Project EmployeeListApp.DataAccess"

Note change the <NameOfMigration> with your desired migration name 

after migration open SQl Server Management Studion  run this sql script " CREATE PROCEDURE dbo.sp_SearchEmployees
    @searchPattern NVARCHAR(100)
AS
BEGIN
    SET NOCOUNT ON;

    SELECT 
        EmployeeId,
        FirstName,
        LastName,
        MiddleName,
        Email,
        Address,
        PhoneNumber,
        Salary,
        Status,
        Gender
    FROM 
        dbo.Employees
    WHERE 
        LOWER(CONCAT(
            COALESCE(FirstName, ''),
            COALESCE(LastName, ''),
            COALESCE(MiddleName, ''),
            COALESCE(Email, ''),
            COALESCE(Address, ''),
            COALESCE(PhoneNumber, '')
        )) LIKE '%' + LOWER(@searchPattern) + '%'
    ORDER BY 
        LastName, FirstName;
END
" to create stored procedure

You may now run the  "EmployeeListApp.Client" project 


Now for the front end or UI open the "employee-list-app.UI folder" click the location path and open in cmd and type "ng serve" and access its local host or url to "" if open in vs code at the top button click "Terminal" and click "New Terminal" type "ng serve" and access its url to .

make sure to run first the web api or "EmployeeListApp.Client". and thats it you may now use the application
