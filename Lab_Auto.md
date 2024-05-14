   
### Program to input records into SQL database (Part 1):

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

### GUI with user input (Part 2)
![2024-05-13](https://github.com/suddy00/CISC_191_Int_Java/assets/17439019/f8c6fb49-02f9-48dd-ae0f-94d569a87634)

### Code:
```java
import java.awt.GridBagConstraints;
import java.awt.GridBagLayout;
import java.awt.Insets;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import javax.swing.JButton;
import javax.swing.JFormattedTextField;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JScrollPane;
import javax.swing.JTextArea;
import java.sql.*;

public class AutoFrame extends JFrame implements ActionListener {
    private JTextArea outputArea;                       // Displays Database info
    private JButton refreshButton;                      // Triggers query
    private JFormattedTextField inputField;             // Input

    /* Constructor creates GUI components and adds GUI components
       using a GridBagLayout. */
    AutoFrame() {
        GridBagConstraints layoutConst = null; // Used to specify GUI component layout
        JScrollPane scrollPane = null;         // Container that adds a scroll bar
        JLabel inputLabel = null;               // Label for input field
        JLabel outputLabel = null;             // Label output


        // Set frame's title
        setTitle("Auto Program");

        // Create labels
        inputLabel = new JLabel("User Input:");
        outputLabel = new JLabel("Auto Info:");

        // Create output area and add it to scroll pane
        outputArea = new JTextArea(10, 52);
        scrollPane = new JScrollPane(outputArea);
        outputArea.setEditable(false);

        refreshButton = new JButton("Refresh");
        refreshButton.addActionListener(this);

        // Create savings field and specify the currency format
        inputField = new JFormattedTextField();
        inputField.setEditable(true);
        inputField.setColumns(10); // Initial width of 10 units
        inputField.setValue("All");
        inputField.addActionListener(this);

        // Use a GridBagLayout
        setLayout(new GridBagLayout());

        layoutConst = new GridBagConstraints();
        layoutConst.insets = new Insets(10, 10, 5, 1);
        layoutConst.anchor = GridBagConstraints.LINE_END;
        layoutConst.gridx = 0;
        layoutConst.gridy = 0;
        add(inputLabel, layoutConst);

        layoutConst = new GridBagConstraints();
        layoutConst.insets = new Insets(10, 1, 5, 10);
        layoutConst.fill = GridBagConstraints.HORIZONTAL;
        layoutConst.gridx = 1;
        layoutConst.gridy = 0;
        add(inputField, layoutConst);

        layoutConst = new GridBagConstraints();
        layoutConst.insets = new Insets(0, 5, 0, 10);
        layoutConst.fill = GridBagConstraints.BOTH;
        layoutConst.gridx = 2;
        layoutConst.gridy = 0;
        add(refreshButton, layoutConst);

        layoutConst = new GridBagConstraints();
        layoutConst.insets = new Insets(10, 10, 1, 10);
        layoutConst.fill = GridBagConstraints.HORIZONTAL;
        layoutConst.gridx = 0;
        layoutConst.gridy = 2;
        add(outputLabel, layoutConst);

        layoutConst = new GridBagConstraints();
        layoutConst.insets = new Insets(1, 10, 10, 10);
        layoutConst.fill = GridBagConstraints.HORIZONTAL;
        layoutConst.gridx = 0;
        layoutConst.gridy = 4;
        layoutConst.gridwidth = 9; // 9 cells wide
        add(scrollPane, layoutConst);
    }

    @Override
    public void actionPerformed(ActionEvent event) {
        String userInput = inputField.getText();

        try {
            outputArea.setText(runSqlStuff(userInput));
        } catch (SQLException e) {
            throw new RuntimeException(e);
        } catch (ClassNotFoundException e) {
            throw new RuntimeException(e);
        }
    }

    /* Creates a AutoInfoFrame and makes it visible */
    public static void main(String[] args) {

        // Creates AutoInfoFrame and its components
        AutoFrame myFrame = new AutoFrame();
        myFrame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        myFrame.pack();
        myFrame.setVisible(true);

    }

    public static String runSqlStuff(String uInput) throws SQLException, ClassNotFoundException{
        StringBuilder autoStream = new StringBuilder();

        // Load the JDBC driver
        Class.forName("com.mysql.cj.jdbc.Driver");
        System.out.println("Driver loaded");

        Connection connection = DriverManager.getConnection
                ("jdbc:mysql://localhost/Auto","testuser","Pa$$word");
        System.out.println("Database connected");

        // Create a statement
        Statement statement = connection.createStatement();

        // Execute a statement
        ResultSet resultSet = statement.executeQuery
                ("select * from AutoData where name like '%"+ uInput+"%';");
        // Iterate through the result and print the vehicle info
        while (resultSet.next())
            autoStream.append(resultSet.getString(1)).append("    ")
                    .append(resultSet.getString(2)).append("    ").append(resultSet.getString(3))
                    .append("    ").append(resultSet.getString(4)).append("    ")
                    .append(resultSet.getString(5)).append("    ").append(resultSet.getString(6))
                    .append("    ").append(resultSet.getString(7)).append("    ")
                    .append(resultSet.getString(8)).append(" ").append(resultSet.getString(9)).append("\n");
        // Close the connection
        connection.close();

        String autoOut = autoStream.toString();
        return autoOut;
    }
}
```
### GUI with sliders (Part 3)
![2024-05-13 (1)](https://github.com/suddy00/CISC_191_Int_Java/assets/17439019/0c85284e-045e-449b-8ac0-490678cfb2d0)

### Code:
import java.awt.GridBagConstraints;
import java.awt.GridBagLayout;
import java.awt.Insets;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import javax.swing.JButton;
import javax.swing.JFormattedTextField;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JScrollPane;
import javax.swing.JTextArea;
import javax.swing.JSlider;
import javax.swing.event.ChangeEvent;
import javax.swing.event.ChangeListener;
import java.sql.*;

public class AutoFrame extends JFrame implements ActionListener, ChangeListener {
    private JTextArea outputArea;                       // Displays Database info
    private JButton refreshButton;                      // Triggers query
    private JFormattedTextField inputField;             // Input
    private JSlider mpgSlider;    // Slider for mpg input
    private JSlider hpSlider;     // Slider for horsepower input


    /* Constructor creates GUI components and adds GUI components
       using a GridBagLayout. */
    AutoFrame() {
        GridBagConstraints layoutConst = null; // Used to specify GUI component layout
        JScrollPane scrollPane = null;         // Container that adds a scroll bar
        JLabel inputLabel = null;               // Label for input field
        JLabel outputLabel = null;             // Label output
        JLabel mpgLabel = null;             // Label output
        JLabel hpLabel = null;             // Label output

        //Slider Values
        int mpgMin = 0;
        int mpgMax = 40;
        int mpgInit = 20;
        int hpMin = 0;
        int hpMax = 150;
        int hpInit = 75;

        mpgSlider = new JSlider(mpgMin, mpgMax, mpgInit);
        mpgSlider.addChangeListener(this);
        mpgSlider.setMajorTickSpacing(10);
        mpgSlider.setMinorTickSpacing(2);
        mpgSlider.setPaintTicks(true);
        mpgSlider.setPaintLabels(true);

        hpSlider = new JSlider(hpMin, hpMax, hpInit);
        hpSlider.addChangeListener(this);
        hpSlider.setMajorTickSpacing(25);
        hpSlider.setMinorTickSpacing(5);
        hpSlider.setPaintTicks(true);
        hpSlider.setPaintLabels(true);

        // Set frame's title
        setTitle("Auto Program");

        // Create labels
        inputLabel = new JLabel("User Input:");
        outputLabel = new JLabel("Auto Info:");
        mpgLabel = new JLabel("MPG");
        hpLabel = new JLabel("H-Pwr");

        // Create output area and add it to scroll pane
        outputArea = new JTextArea(10, 52);
        scrollPane = new JScrollPane(outputArea);
        outputArea.setEditable(false);

        refreshButton = new JButton("Refresh");
        refreshButton.addActionListener(this);

        // Create savings field and specify the currency format
        inputField = new JFormattedTextField();
        inputField.setEditable(true);
        inputField.setColumns(10); // Initial width of 10 units
        inputField.setValue("");
        inputField.addActionListener(this);


        // Use a GridBagLayout
        setLayout(new GridBagLayout());

        layoutConst = new GridBagConstraints();
        layoutConst.insets = new Insets(10, 10, 5, 10);
        layoutConst.anchor = GridBagConstraints.LINE_START;
        layoutConst.gridx = 0;
        layoutConst.gridy = 0;
        add(inputLabel, layoutConst);

        layoutConst = new GridBagConstraints();
        layoutConst.insets = new Insets(10, 10, 5, 10);
        layoutConst.fill = GridBagConstraints.BOTH;
        layoutConst.gridx = 0;
        layoutConst.gridy = 1;
        add(inputField, layoutConst);

        layoutConst = new GridBagConstraints();
        layoutConst.insets = new Insets(0, 5, 0, 10);
        layoutConst.fill = GridBagConstraints.CENTER;
        layoutConst.gridx = 2;
        layoutConst.gridy = 1;
        add(refreshButton, layoutConst);

        layoutConst = new GridBagConstraints();
        layoutConst.insets = new Insets(10, 10, 1, 10);
        layoutConst.fill = GridBagConstraints.CENTER;
        layoutConst.gridx = 0;
        layoutConst.gridy = 3;
        add(mpgLabel, layoutConst);

        layoutConst = new GridBagConstraints();
        layoutConst.insets = new Insets(10, 10, 1, 10);
        layoutConst.fill = GridBagConstraints.CENTER;
        layoutConst.gridx = 2;
        layoutConst.gridy = 3;
        add(hpLabel, layoutConst);

        layoutConst = new GridBagConstraints();
        layoutConst.insets = new Insets(10, 10, 1, 10);
        layoutConst.fill = GridBagConstraints.HORIZONTAL;
        layoutConst.gridx = 0;
        layoutConst.gridy = 4;
        add(mpgSlider, layoutConst);

        layoutConst = new GridBagConstraints();
        layoutConst.insets = new Insets(10, 10, 1, 10);
        layoutConst.fill = GridBagConstraints.HORIZONTAL;
        layoutConst.gridx = 2;
        layoutConst.gridy = 4;
        add(hpSlider, layoutConst);

        layoutConst = new GridBagConstraints();
        layoutConst.insets = new Insets(10, 10, 1, 10);
        layoutConst.fill = GridBagConstraints.HORIZONTAL;
        layoutConst.gridx = 0;
        layoutConst.gridy = 5;
        add(outputLabel, layoutConst);

        layoutConst = new GridBagConstraints();
        layoutConst.insets = new Insets(1, 10, 10, 10);
        layoutConst.fill = GridBagConstraints.HORIZONTAL;
        layoutConst.gridx = 0;
        layoutConst.gridy = 6;
        layoutConst.gridwidth = 9; // 9 cells wide
        add(scrollPane, layoutConst);
    }

    /* Called as slider value changes. Updates fields to display
      the numerical representation of the slider settings. */
    @Override
    public void stateChanged(ChangeEvent event) {
        int mpgValue = mpgSlider.getValue();
        int hpValue = hpSlider.getValue();

        try {
            outputArea.setText(runSqlStuff(inputField.getText(), mpgValue, hpValue));
        } catch (SQLException e) {
            throw new RuntimeException(e);
        } catch (ClassNotFoundException e) {
            throw new RuntimeException(e);
        }

    }

    @Override
    public void actionPerformed(ActionEvent event) {
        String userInput = inputField.getText();

        try {
            outputArea.setText(runSqlStuff(userInput, mpgSlider.getValue(), hpSlider.getValue()));
        } catch (SQLException e) {
            throw new RuntimeException(e);
        } catch (ClassNotFoundException e) {
            throw new RuntimeException(e);
        }
    }

    /* Creates a AutoInfoFrame and makes it visible */
    public static void main(String[] args) {

        // Creates AutoInfoFrame and its components
        AutoFrame myFrame = new AutoFrame();
        myFrame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        myFrame.pack();
        myFrame.setVisible(true);

    }

    public static String runSqlStuff(String uInput, int mpg, int hp) throws SQLException, ClassNotFoundException{
        StringBuilder autoStream = new StringBuilder();

        // Load the JDBC driver
        Class.forName("com.mysql.cj.jdbc.Driver");
        System.out.println("Driver loaded");

        Connection connection = DriverManager.getConnection
                ("jdbc:mysql://localhost/Auto","testuser","Pa$$word");
        System.out.println("Database connected");

        // Create a statement
        Statement statement = connection.createStatement();

        // Execute a statement
        ResultSet resultSet = statement.executeQuery
                ("select * from AutoData where name like '%"+ uInput+"%' " +
                        " and mpg >= " +mpg+ " " +
                        " and horsepower >= " +hp+ ";");
        // Iterate through the result and print the vehicle info
        while (resultSet.next())
            autoStream.append(resultSet.getString(1)).append("    ")
                    .append(resultSet.getString(2)).append("    ").append(resultSet.getString(3))
                    .append("    ").append(resultSet.getString(4)).append("    ")
                    .append(resultSet.getString(5)).append("    ").append(resultSet.getString(6))
                    .append("    ").append(resultSet.getString(7)).append("    ")
                    .append(resultSet.getString(8)).append(" ").append(resultSet.getString(9)).append("\n");
        // Close the connection
        connection.close();

        String autoOut = autoStream.toString();
        return autoOut;
    }
}

### Challenges throughout:
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
  - Gui output bad/hard to read
    Tried:
      Creating labels for all fields
      Removing and resizing labels and output
      Implementing a table
      Deleted labels and individually spaced elements on the text field.
  Using user input to query name info. "All" does not work do display all records. But an empty input achieves the same result.
No other issues to report.
