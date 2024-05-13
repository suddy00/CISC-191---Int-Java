## Challenges:
  -Input data type as INT for Cylinders and Horsepower but because they had periods following received a data mismatch error.
    Tried: 
      Altered table properties. (Year is definitely NOT a double) bad solution
      Creating "." delimeter. Prevous double values include "." so caused other mismatches 
      returned to all doubles ...
  - Recieved input SQL syntax error at statement.executeUpdate line
    Triple checked syntax
    Altered all fields to varchar
    Changed all input to string, setting delimeter to a space
    removed all variable data types, using input.next()
    removed all varibales, reverted all Auto fields, imported .txt data via SQL ...
- Received --secure-file-priv error
    Tried:
      load data local -- Loading local data is disabled error
      exact location path
      turned off (and on) local_infile
  - Took a Break - Restarted. Set attributes to String, removed "'" in record, deleted 1 duplicate record. Altered name of a LOT of records. Upload successful.

## Process:
Create Database (Auto) and Table based on values given:

create table AutoData (
  mpg DOUBLE(3, 1), 
  cylinders INT(2), 
  displacement DOUBLE(4,1), 
  horsepower INT(4), 
  weight DOUBLE(4,0),  
  acceleration DOUBLE(3,1),  
  year YEAR,
  origin VARCHAR(2),
  name VARCHAR(255),  
  primary key (name)
); 
later altered to:
  mpg VARCHAR(4), 
  cylinders VARCHAR(3), 
  displacement VARCHAR(5), 
  horsepower VARCHAR(5), 
  weight VARCHAR(6),  
  acceleration VARCHAR(6),  
  year VARCHAR(4),
  origin VARCHAR(3),
  name VARCHAR(255),  
  primary key (name)


![AutoData](https://github.com/suddy00/CISC_191_Int_Java/assets/17439019/fbeafa97-a6c7-4343-8204-cbf797264a04)


### Program to input records into SQL database:

```java
import java.io.FileNotFoundException;
import java.sql.*;
import java.util.Scanner;
import java.io.FileInputStream;
import java.io.IOException;

public class Main {
    public static void main(String[] args)
            throws SQLException, ClassNotFoundException, IOException {
        // Load the JDBC driver
        Class.forName("com.mysql.cj.jdbc.Driver");
        System.out.println("Driver loaded");

        FileInputStream inputData;
        try {
            inputData = new FileInputStream("src/Auto_MPG_Data.txt");
        } catch (FileNotFoundException e) {
            throw new RuntimeException(e);
        }
        Scanner input = new Scanner(inputData);

        // Establish a connection
        // Assuming the database name is 'Auto', user is 'testuser'
        // and password is 'Pa$$word'
        Connection connection = DriverManager.getConnection
                ("jdbc:mysql://localhost/Auto", "testuser", "Pa$$word");
        System.out.println("Database connected");

        // Create a statement
        Statement statement = connection.createStatement();

        while (input.hasNextLine()) {
            String mpg = input.next();
            System.out.print(mpg + " ");
            String cylinders = input.next();
            System.out.print(cylinders + " ");
            String displacement = input.next();
            System.out.print(displacement + " ");
            String horsepower = input.next();
            System.out.print(horsepower + " ");
            String weight = input.next();
            System.out.print(weight + " ");
            String acceleration = input.next();
            System.out.print(acceleration + " ");
            String year = input.next();
            System.out.print(year + " ");
            String origin = input.next();
            System.out.print(origin + " ");
            String name = input.nextLine();
            System.out.println(name);

            //Input record via SQL
            statement.executeUpdate("insert into AutoData (mpg,cylinders,displacement,horsepower,weight,acceleration,year,origin,name)" +
            "values ('"+mpg+"','"+cylinders+"','"+displacement+"','"+horsepower+"','"+weight+"','"+acceleration+"','"+year+"','"+origin+"','"+name+"' )");
        }

        // Close the connection
        connection.close();
        inputData.close();
    }
}
```
