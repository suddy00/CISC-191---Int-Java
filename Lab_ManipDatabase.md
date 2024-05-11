## Challenges:
-Overall getting familiar with SQL language

## Output:
![Screenshot (62)](https://github.com/suddy00/CISC_191_Int_Java/assets/17439019/4444f4b8-f66a-4a9e-b604-fb5654eaee85)

## Code: 
```java
import java.sql.*;
public class Main {
    public static void main(String[] args)
            throws SQLException, ClassNotFoundException {
        // Load the JDBC driver
        Class.forName("com.mysql.cj.jdbc.Driver");
        System.out.println("Driver loaded");

        // Establish a connection
        // Assuming the database name is 'testdb', user is 'testuser'
        // and password is 'Pa$$word'
        Connection connection = DriverManager.getConnection
                ("jdbc:mysql://localhost/miramar","testuser","Pa$$word");
        System.out.println("Database connected");

        // Create a statement
        Statement statement = connection.createStatement();

        statement.executeUpdate("insert into Student (ssn,firstname,mi,lastname,birthDate,street,phone,zipCode,deptId)" +
                "values ('111222333','Philip','D','Collins','1951-01-30','NA','NA','NA',1234)\n" +
                ";");

        statement.executeUpdate("update Student " +
                "set zipcode = '92126' " +
                "where ssn = '111222333'");

        // Execute a statement
        ResultSet resultSet = statement.executeQuery
                ("select * from Student;");

        // Iterate through the result and print the student names
        while (resultSet.next())
            System.out.println(resultSet.getString(1) + "\t" +
                    resultSet.getString(2) + "\t" + resultSet.getString(3) + "\t" +
                    resultSet.getString(4) + "\t" + resultSet.getString(5));

        // Close the connection
        connection.close();
    }
}
```
