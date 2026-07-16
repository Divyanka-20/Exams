import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.Statement;

public class CRUD {

    private static final String URL = "jdbc:mysql://localhost:3306/studentdb";
    private static final String USER = "root";
    private static final String PASSWORD = "divyanka123";

    public static void main(String[] args) {
        System.out.println("=== Starting Live CRUD Tracker ===");

        try {
            Class.forName("com.mysql.cj.jdbc.Driver");
        } catch (ClassNotFoundException e) {
            System.err.println("Error: Driver missing.");
            return;
        }

        try (Connection con = DriverManager.getConnection(URL, USER, PASSWORD);
             Statement stmt = con.createStatement()) {

            System.out.println("[CONNECTED] Successfully linked to MySQL server.");
            System.out.println("------------------------------------------------");

            // 1. CREATE (Insert)
            String insertSQL = "INSERT INTO students (name, age) VALUES ('John', 20)";
            stmt.executeUpdate(insertSQL);
            System.out.println("[CREATE] Inserted 'John' with age 20.");
            
            // READ (State After Insert)
            System.out.println("--> Table State After INSERT:");
            printCurrentRecords(stmt);

            // 2. UPDATE (Modify existing record) - This was missing!
            System.out.println("\n[UPDATE] Changing John's age to 22.");
            String updateSQL = "UPDATE students SET age = 22 WHERE name = 'John'";
            stmt.executeUpdate(updateSQL);

            // 3. READ (State After Update)
            System.out.println("--> Table State After UPDATE:");
            printCurrentRecords(stmt);

            // 4. DELETE (Remove Record)
            String deleteSQL = "DELETE FROM students WHERE name = 'John'";
            stmt.executeUpdate(deleteSQL);
            System.out.println("\n[DELETE] Purged 'John' from the database.");

            // READ (State After Delete)
            System.out.println("--> Table State After DELETE:");
            printCurrentRecords(stmt);

        } catch (Exception e) {
            System.err.println("\n[ERROR] Database execution broken:");
            e.printStackTrace();
        }

        System.out.println("\n=== Lifecycle Complete ===");
    }

    // Helper function to query and display the current records in the table
    private static void printCurrentRecords(Statement stmt) throws Exception {
        String selectSQL = "SELECT id, name, age FROM students";
        System.out.println("ID   | NAME                 | AGE");
        System.out.println("------------------------------------------------");
        
        try (ResultSet rs = stmt.executeQuery(selectSQL)) {
            boolean hasData = false;
            while (rs.next()) {
                hasData = true;
                int id = rs.getInt("id");
                String name = rs.getString("name");
                int age = rs.getInt("age");
                System.out.printf("%-4d | %-20s | %d\n", id, name, age);
            }
            if (!hasData) {
                System.out.println("      *** Table is currently empty *** ");
            }
        }
        System.out.println("------------------------------------------------");
    }
}
    
    <!DOCTYPE html>
    <html>
    <head>
    <title>Calculator</title>
    </head>
    <body>
    
    <h2>Simple Calculator</h2>
    
    <form action="CalculatorServlet" method="post">
    
    First Number:
    <input type="number" name="num1"><br><br>
    
    Second Number:
    <input type="number" name="num2"><br><br>
    
    <input type="submit" value="Add">
    
    </form>
    
    </body>
    </html>


    package com.calc;
    
    import java.io.*;
    import jakarta.servlet.*;
    import jakarta.servlet.http.*;
    
    public class CalculatorServlet extends HttpServlet{
    
        protected void doPost(HttpServletRequest request,HttpServletResponse response)
        throws ServletException,IOException{
    
            response.setContentType("text/html");
    
            PrintWriter out=response.getWriter();
    
            int a=Integer.parseInt(request.getParameter("num1"));
            int b=Integer.parseInt(request.getParameter("num2"));
    
            int sum=a+b;
    
            out.println("<h2>Result = "+sum+"</h2>");
        }
    }

    <?xml version="1.0" encoding="UTF-8"?>
    
    <web-app xmlns="https://jakarta.ee/xml/ns/jakartaee"
    version="5.0">
    
    <servlet>
    <servlet-name>CalculatorServlet</servlet-name>
    <servlet-class>com.calc.CalculatorServlet</servlet-class>
    </servlet>
    
    <servlet-mapping>
    <servlet-name>CalculatorServlet</servlet-name>
    <url-pattern>/CalculatorServlet</url-pattern>
    </servlet-mapping>
    
    </web-app>

<br>

    import java.sql.*;
    
    public class CRUD {
    
        public static void main(String args[]) {
    
            String url="jdbc:mysql://localhost:3306/studentdb";
            String user="root";
            String password="root";
    
            try{
    
                Class.forName("com.mysql.cj.jdbc.Driver");
    
                Connection con=DriverManager.getConnection(url,user,password);
    
                Statement stmt=con.createStatement();
    
                stmt.executeUpdate("INSERT INTO students(name,age) VALUES('John',20)");
                System.out.println("Inserted");
    
                ResultSet rs=stmt.executeQuery("SELECT * FROM students");
    
                while(rs.next()){
                    System.out.println(rs.getInt("id")+" "
                    +rs.getString("name")+" "
                    +rs.getInt("age"));
                }
    
                stmt.executeUpdate("UPDATE students SET age=22 WHERE name='John'");
                System.out.println("Updated");
    
                stmt.executeUpdate("DELETE FROM students WHERE name='John'");
                System.out.println("Deleted");
    
                con.close();
    
            }
    
            catch(Exception e){
                System.out.println(e);
            }
    
        }
    }

    CREATE DATABASE studentdb;

    USE studentdb;
    
    CREATE TABLE students(
    
    id INT AUTO_INCREMENT PRIMARY KEY,
    
    name VARCHAR(50),
    
    age INT
    
    );


            <!DOCTYPE html>
        <html>
        <head>
        
        <title>Student Registration Form</title>
        
        <style>
        body{
            font-family: Arial;
            margin: 30px;
        }
        
        input, select{
            margin: 5px;
            padding: 5px;
        }
        
        button{
            padding: 5px 10px;
        }
        
        #result{
            margin-top: 20px;
            border: 1px solid black;
            padding: 10px;
        }
        </style>
        
        <script>
        
        function validateForm(){
        
            var name=document.getElementById("name").value.trim();
            var roll=document.getElementById("roll").value.trim();
            var dept=document.getElementById("dept").value;
            var email=document.getElementById("email").value.trim();
        
            if(name==""){
                alert("Please enter Name");
                return false;
            }
        
            if(roll==""){
                alert("Please enter Roll Number");
                return false;
            }
        
            if(dept==""){
                alert("Please select Department");
                return false;
            }
        
            if(email==""){
                alert("Please enter Email");
                return false;
            }
        
            document.getElementById("result").innerHTML=
            "<h3>Entered Details</h3>"+
            "<b>Name :</b> "+name+"<br><br>"+
            "<b>Roll Number :</b> "+roll+"<br><br>"+
            "<b>Department :</b> "+dept+"<br><br>"+
            "<b>Email :</b> "+email;
        
            return false;
        
        }
        
        </script>
        
        </head>
        
        <body>
        
        <div class="container">
        
        <h2>Student Registration Form</h2>
        
        <form onsubmit="return validateForm()">
        
        <label>Name</label>
        <input type="text" id="name">
        
        <label>Roll Number</label>
        <input type="text" id="roll">
        
        <label>Department</label>
        
        <select id="dept">
        <option value="">--Select Department--</option>
        <option>BCA</option>
        <option>BBA</option>
        <option>B.Tech</option>
        <option>MCA</option>
        </select>
        
        <label>Email</label>
        <input type="email" id="email">
        
        <button type="submit">Submit</button>
        
        </form>
        
        <div id="result"></div>
        
        </div>
        
        </body>
        </html>
1.JDBC Connection
  
    package com.example;
    import java.sql.*;
    public class DBConnectionTest {
        public static void main(String[] args) {
            String url = "jdbc:mysql://localhost:3306/studentdb";
            String user = "root";
            String password = "root";
            try {
                Connection con = DriverManager.getConnection(url, user, password);
                System.out.println("Connected! to the DataBase");
                con.close();
            } catch (Exception e) {
                System.out.println(e);
            }
        }
    }

2.CRUD Operations

    package com.example;
    import java.sql.*;
    public class JDBCExample {
        public static void main(String[] args) {
            String url = "jdbc:mysql://localhost:3306/studentdb";
            String user = "root";
            String password = "root";
            try {
                Class.forName("com.mysql.cj.jdbc.Driver");
                Connection con = DriverManager.getConnection(url, user, password);
                System.out.println("Connected to Database!");
                Statement stmt = con.createStatement();
                // 1. CREATE (INSERT)
                String insertQuery ="INSERT INTO students(name, age) VALUES('John',20)";
                stmt.executeUpdate(insertQuery);
                System.out.println("Record Inserted!");
                // 2. READ (SELECT)
                String selectQuery = "SELECT * FROM students";
                ResultSet rs = stmt.executeQuery(selectQuery);
                System.out.println("\nStudent Records:");
                while (rs.next()) {
                    System.out.println(
                            rs.getInt("id") + " "
                            + rs.getString("name") + " "
                            + rs.getInt("age"));
                }
                // 3. UPDATE
                String updateQuery = "UPDATE students SET age=22 WHERE name='John'";
                stmt.executeUpdate(updateQuery);
                System.out.println("\nRecord Updated!");
                // 4. READ AFTER UPDATE
                rs = stmt.executeQuery("SELECT * FROM students");
                System.out.println("\nAfter Update:");
                while (rs.next()) {
                    System.out.println(
                            rs.getInt("id") + " "
                            + rs.getString("name") + " "
                            + rs.getInt("age"));
                }
                // 5. DELETE
                String deleteQuery = "DELETE FROM students WHERE name='John'";
                stmt.executeUpdate(deleteQuery);
                System.out.println("\nRecord Deleted!");
                // Close
                rs.close();
                stmt.close();
                con.close();
    
            } catch (Exception e) {
                e.printStackTrace();
            }
        }
    }

3.Clock Servlet <br>
  3.1.Servlet
  
    package com.clock;
    import java.io.IOException;
    import java.io.PrintWriter;
    import java.time.LocalDateTime;
    import java.time.format.DateTimeFormatter;  
    import jakarta.servlet.ServletException;
    import jakarta.servlet.http.HttpServlet;
    import jakarta.servlet.http.HttpServletRequest;
    import jakarta.servlet.http.HttpServletResponse;    
    public class ClockServlet extends HttpServlet {   
        protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
            response.setContentType("text/html");
            PrintWriter out = response.getWriter();
            LocalDateTime now = LocalDateTime.now();
            DateTimeFormatter format = DateTimeFormatter.ofPattern("dd-MM-yyyy HH:mm:ss");
            String currentDateTime = now.format(format);
            out.println("<html>");
            out.println("<head>");
            out.println("<title>Digital Clock</title>");
            out.println("</head>");
            out.println("<body style='text-align:center; font-family:Arial;'>");
            out.println("<h1>Current Date and Time</h1>");
            out.println("<h2>" + currentDateTime + "</h2>");
            out.println("</body>");
            out.println("</html>");
        }
    }

 3.2.XML

    <?xml version="1.0" encoding="UTF-8"?>   
    <web-app xmlns="https://jakarta.ee/xml/ns/jakartaee"
             xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
             xsi:schemaLocation="https://jakarta.ee/xml/ns/jakartaee https://jakarta.ee/xml/ns/jakartaee/web-app_5_0.xsd"
             version="5.0">
        <servlet>
            <servlet-name>ClockServlet</servlet-name>
            <servlet-class>com.clock.ClockServlet</servlet-class>
        </servlet>
        <servlet-mapping>
            <servlet-name>ClockServlet</servlet-name>
            <url-pattern>/</url-pattern>
        </servlet-mapping>
    </web-app>

4.Login using Servlet+JDBC
4.1HTML

    <!DOCTYPE html>
    <html>
    <head>
    <title>Login Form</title>
    </head>
    <body>
    <h2>Login Form</h2>
    <form action="LoginServlet" method="post">
    Username:<input type="text" name="username"><br><br>
    Password:<input type="password" name="password"><br><br>
    <input type="submit" value="Login">
    </form>
    </body>
    </html>

4.2Servlet

    package com.login;
    import java.io.IOException;
    import java.io.PrintWriter;
    import java.sql.*;
    import jakarta.servlet.ServletException;
    import jakarta.servlet.http.*;
    import jakarta.servlet.annotation.WebServlet;
    @WebServlet("/LoginServlet")
    public class LoginServlet extends HttpServlet {
        protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
            response.setContentType("text/html");
            PrintWriter out = response.getWriter();
            String username = request.getParameter("username");
            String password = request.getParameter("password");
            String url = "jdbc:mysql://localhost:3306/studentdb";
            String user = "root";
            String pass = "root";
            try {
                Class.forName("com.mysql.cj.jdbc.Driver");
                Connection con = DriverManager.getConnection(url, user, pass);
                PreparedStatement ps = con.prepareStatement("SELECT * FROM users WHERE username=? AND password=?");
                ps.setString(1, username);
                ps.setString(2, password);
                ResultSet rs = ps.executeQuery();
                if (rs.next()) {
                    out.println("<h2>Login Successful</h2>");
                } else {
                    out.println("<h2>Invalid Username or Password</h2>");
                }
                rs.close();
                ps.close();
                con.close();
            } catch (Exception e) {
                out.println(e);
            }
        }
    }

5.Register

    <!DOCTYPE html>
    <html>
    <head>
        <title>Registration Form</title>
    </head>
    <body>
    <h2>Student Registration Form</h2>
    <form action="RegisterServlet" method="post">
        Name:
        <input type="text" name="name" required><br><br>
        Email:
        <input type="email" name="email" required><br><br>
        Username:
        <input type="text" name="username" required><br><br>
        Password:
        <input type="password" name="password" required><br><br>
        Age:
        <input type="number" name="age"><br><br>
        Gender:
        <input type="radio" name="gender" value="Male">Male
        <input type="radio" name="gender" value="Female">Female
        <br><br>
        Course:
        <select name="course">
            <option>BCA</option>
            <option>BBA</option>
            <option>B.Sc</option>
            <option>MCA</option>
        </select>
        <br><br>
        <input type="submit" value="Register">
        <input type="reset" value="Clear">
    </form>
    </body>
    </html>

    package com.register;
    
    import java.io.IOException;
    import java.io.PrintWriter;
    import java.sql.Connection;
    import java.sql.DriverManager;
    import java.sql.PreparedStatement;
    
    import jakarta.servlet.ServletException;
    import jakarta.servlet.annotation.WebServlet;
    import jakarta.servlet.http.HttpServlet;
    import jakarta.servlet.http.HttpServletRequest;
    import jakarta.servlet.http.HttpServletResponse;
    
    @WebServlet("/RegisterServlet")
    public class RegisterServlet extends HttpServlet {
    
        protected void doPost(HttpServletRequest request,
                              HttpServletResponse response)
                throws ServletException, IOException {
    
            response.setContentType("text/html");
            PrintWriter out = response.getWriter();
    
            String name = request.getParameter("name");
            String email = request.getParameter("email");
            String username = request.getParameter("username");
            String password = request.getParameter("password");
            String age = request.getParameter("age");
            String gender = request.getParameter("gender");
            String course = request.getParameter("course");
    
            String url = "jdbc:mysql://localhost:3306/studentdb";
            String user = "root";
            String pass = "root";
    
            try {
    
                Class.forName("com.mysql.cj.jdbc.Driver");
    
                Connection con = DriverManager.getConnection(url, user, pass);
    
                String sql = "INSERT INTO students(name,email,username,password,age,gender,course) VALUES(?,?,?,?,?,?,?)";
    
                PreparedStatement ps = con.prepareStatement(sql);
    
                ps.setString(1, name);
                ps.setString(2, email);
                ps.setString(3, username);
                ps.setString(4, password);
                ps.setInt(5, Integer.parseInt(age));
                ps.setString(6, gender);
                ps.setString(7, course);
    
                int i = ps.executeUpdate();
    
                if (i > 0) {
                    out.println("<h2>Registration Successful!</h2>");
                } else {
                    out.println("<h2>Registration Failed!</h2>");
                }
    
                ps.close();
                con.close();
    
            } catch (Exception e) {
                out.println(e);
            }
        }
    }


    <?xml version="1.0" encoding="UTF-8"?>
    
    <web-app xmlns="https://jakarta.ee/xml/ns/jakartaee"
             xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
             xsi:schemaLocation="https://jakarta.ee/xml/ns/jakartaee
             https://jakarta.ee/xml/ns/jakartaee/web-app_5_0.xsd"
             version="5.0">
    
        <welcome-file-list>
            <welcome-file>registration.html</welcome-file>
        </welcome-file-list>
    
    </web-app>
