# SRP (Single Responsibility Principle)
Single responsibility state that a class should have one, and only one, reason to change.

     namespace SRP
     {
         public class Employee
         {
             public int Employee_Id { get; set; }
             public string Employee_Name { get; set; }

             /// <summary>
             /// This method used to insert into employee table
             /// </summary>
             /// <param name="em">Employee object</param>
             /// <returns>Successfully inserted or not</returns>
             public bool InsertIntoEmployeeTable(Employee em)
             {
                 // Insert into employee table.
                 return true;
             }
             /// <summary>
             /// Method to generate report
             /// </summary>
             /// <param name="em"></param>
             public void GenerateReport(Employee em)
             {
                 // Report generation with employee data using crystal report.
             }
         }
     }
     
     
Solution# 


     public class ReportGeneration
     {
          /// <summary>
          /// Method to generate report
          /// </summary>
          /// <param name="em"></param>
          public void GenerateReport(Employee em)
          {
              // Report reneration with employee data.
          }
     }  

     
# OCP (Open-Closed Principle)
Open close principle state that a software module/class is open for extension and closed for modification

     public class ReportGeneration
     {
         /// <summary>
         /// Report type
         /// </summary>
         public string ReportType { get; set; }

         /// <summary>
         /// Method to generate report
         /// </summary>
         /// <param name="em"></param>
         public void GenerateReport(Employee em)
         {
             if (ReportType == "CRS")
             {
                  // Report generation with employee data in Crystal Report.
             }
             if (ReportType == "PDF")
             {
                 // Report generation with employee data in PDF.
             }
          }
      }
     
 Solution
 
         public class IReportGeneration
         {
             /// <summary>
             /// Method to generate report
             /// </summary>
             /// <param name="em"></param>
             public virtual void GenerateReport(Employee em)
             {
                 // From base
             }
         }
         /// <summary>
         /// Class to generate Crystal report
         /// </summary>
         public class CrystalReportGeneraion : IReportGeneration
         {
             public override void GenerateReport(Employee em)
             {
                 // Generate crystal report.
             }
         }
         /// <summary>
         /// Class to generate PDF report
         /// </summary>
         public class PDFReportGeneraion : IReportGeneration
         {
             public override void GenerateReport(Employee em)
             {
                 // Generate PDF report.
             }
         }
    
          
# LSP (Liskov's Substitution Principle)
The Liskov Substitution Principle (LSP) states that "you should be able to use any derived class instead of a parent class and have it 
behave in the same manner without modification". It ensures that a derived class does not affect the behavior of the parent class, 
in other words that a derived class must be substitutable for its base class

Problem

     public abstract class Employee
     {
         public virtual string GetProjectDetails(int employeeId)
         {
             return "Base Project";
         }
         public virtual string GetEmployeeDetails(int employeeId)
         {
             return "Base Employee";
         }
     }
     public class CasualEmployee : Employee
     {
         public override string GetProjectDetails(int employeeId)
         {
             return "Child Project";
         }
         // May be for contractual employee we do not need to store the details into database.
         public override string GetEmployeeDetails(int employeeId)
         {
             return "Child Employee";
         }
     }
     public class ContractualEmployee : Employee
     {
         public override string GetProjectDetails(int employeeId)
         {
             return "Child Project";
         }
         // May be for contractual employee we do not need to store the details into database.
         public override string GetEmployeeDetails(int employeeId)
         {
             throw new NotImplementedException();
         }
     }
     
     List<Employee> employeeList = new List<Employee>();
     employeeList.Add(new ContractualEmployee());
     employeeList.Add(new CasualEmployee());
     foreach (Employee e in employeeList)
     {
         e.GetEmployeeDetails(1245);
     }
     
     
Solutions

     public interface IEmployee
     {
         string GetEmployeeDetails(int employeeId);
     }

     public interface IProject
     {
         string GetProjectDetails(int employeeId);
     }




# ISP (Interface Segregation Principle)
Clients should not be forced to implement interfaces they don't use. Instead of one fat interface many small interfaces are preferred 
based on groups of methods, each one serving one sub module.

# DIP (Dependency Injection/Inversion)
High-level modules/classes should not depend upon low-level modules/classes. Both should depend upon abstractions. Secondly, 
abstractions should not depend upon details. Details should depend upon abstractions.
