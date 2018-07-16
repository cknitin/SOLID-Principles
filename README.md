# SRP (Single Responsibility Principle)
Single responsibility state that a class should have one, and only one, reason to change.

     public class UserService  
     {  
        public void Register(string email, string password)  
        {  
           if (!ValidateEmail(email))  
              throw new ValidationException("Email is not an email");  
              var user = new User(email, password);  

              SendEmail(new MailMessage("mysite@nowhere.com", email) { Subject="HEllo foo" });  
        }
        public virtual bool ValidateEmail(string email)  
        {  
          return email.Contains("@");  
        }  
        public bool SendEmail(MailMessage message)  
        {  
          _smtpClient.Send(message);  
        }  
     }
     
     
Looks fine, but it is not following SRP. The SendEmail and ValidateEmail methods have nothing to do within the UserService class. Let's refract it.  


     public class UserService  
     {  
        EmailService _emailService;  
        DbContext _dbContext;  
        public UserService(EmailService aEmailService, DbContext aDbContext)  
        {  
           _emailService = aEmailService;  
           _dbContext = aDbContext;  
        }  
        public void Register(string email, string password)  
        {  
           if (!_emailService.ValidateEmail(email))  
              throw new ValidationException("Email is not an email");  
              var user = new User(email, password);  
              _dbContext.Save(user);  
              emailService.SendEmail(new MailMessage("myname@mydomain.com", email) {Subject="Hi. How are you!"});  

           }  
        }  
        public class EmailService  
        {  
           SmtpClient _smtpClient;  
        public EmailService(SmtpClient aSmtpClient)  
        {  
           _smtpClient = aSmtpClient;  
        }  
        public bool virtual ValidateEmail(string email)  
        {  
           return email.Contains("@");  
        }  
        public bool SendEmail(MailMessage message)  
        {  
           _smtpClient.Send(message);  
        }  
     }  

     
# OCP (Open-Closed Principle)
Open close principle state that a software module/class is open for extension and closed for modification
      
# LSP (Liskov's Substitution Principle)
The Liskov Substitution Principle (LSP) states that "you should be able to use any derived class instead of a parent class and have it 
behave in the same manner without modification". It ensures that a derived class does not affect the behavior of the parent class, 
in other words that a derived class must be substitutable for its base class

# ISP (Interface Segregation Principle)
Clients should not be forced to implement interfaces they don't use. Instead of one fat interface many small interfaces are preferred 
based on groups of methods, each one serving one sub module.

# DIP (Dependency Injection/Inversion)
High-level modules/classes should not depend upon low-level modules/classes. Both should depend upon abstractions. Secondly, 
abstractions should not depend upon details. Details should depend upon abstractions.
