
# Challenges
  The Action Listener (calculate) used applies to the entire page. This seems an unusual method of operation, but works well due to the simplicity of the program.

# Output

![2024-04-11](https://github.com/suddy00/CISC_191_Int_Java/assets/17439019/a9c98309-69a7-4938-91f2-0b8d24400518)

# Program
```Java
import java.awt.GridBagConstraints;
import java.awt.GridBagLayout;
import java.awt.Insets;
import javax.swing.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

public class Main extends JFrame implements ActionListener {
    private JLabel wageLabel;     // Label for hourly salary
    private JLabel hoursLabel;    //Label for hours worked per week
    private JLabel salLabel;      // Label for yearly salary
    private JTextField wageField; // Displays yearly salary
    private JTextField hoursField;
    private JTextField salField;  // Displays hourly salary
    private JButton calcButton;   // Triggers salary calculation
    private JButton resetButton;   //Clears fields

    /* Constructor creates GUI components and adds GUI components
       using a GridBagLayout. */
    Main() {
        // Used to specify GUI component layout
        GridBagConstraints positionConst = null;

        // Set frame's title
        setTitle("Salary");

        // Set hourly and yearly salary labels
        wageLabel = new JLabel("Hourly wage:");
        hoursLabel = new JLabel("Hours / week: ");
        salLabel = new JLabel("Yearly salary:");

        wageField = new JTextField(15);
        wageField.setEditable(true);
        wageField.setText("0");

        hoursField = new JTextField(15);
        hoursField.setEditable(true);
        hoursField.setText("0");

        salField = new JTextField(15);
        salField.setEditable(false);

        // Create a "Calculate" button
        calcButton = new JButton("Calculate");

        // Use "this" class to handle button presses
        calcButton.addActionListener(this);

        // Create a "Calculate" button
        resetButton = new JButton("Reset");

        // Use "this" class to handle button presses
        resetButton.addActionListener(this::setResetButton);

        // Use a GridBagLayout
        setLayout(new GridBagLayout());
        positionConst = new GridBagConstraints();

        // Specify component's grid location
        positionConst.gridx = 0;
        positionConst.gridy = 0;

        // 10 pixels of padding around component
        positionConst.insets = new Insets(10, 10, 10, 10);

        // Add component using the specified constraints
        add(wageLabel, positionConst);

        positionConst.gridx = 1;
        positionConst.gridy = 0;
        positionConst.insets = new Insets(10, 10, 10, 10);
        add(wageField, positionConst);

        // Use a GridBagLayout
        setLayout(new GridBagLayout());
        positionConst = new GridBagConstraints();

        // Specify component's grid location
        positionConst.gridx = 0;
        positionConst.gridy = 1;

        // 10 pixels of padding around component
        positionConst.insets = new Insets(10, 10, 10, 10);

        // Add component using the specified constraints
        add(hoursLabel, positionConst);

        positionConst.gridx = 1;
        positionConst.gridy = 1;
        positionConst.insets = new Insets(10, 10, 10, 10);
        add(hoursField, positionConst);

        positionConst.gridx = 0;
        positionConst.gridy = 2;
        positionConst.insets = new Insets(10, 10, 10, 10);
        add(salLabel, positionConst);

        positionConst.gridx = 1;
        positionConst.gridy = 2;
        positionConst.insets = new Insets(10, 10, 10, 10);
        add(salField, positionConst);

        positionConst.gridx = 0;
        positionConst.gridy = 3;
        positionConst.insets = new Insets(10, 10, 10, 10);
        add(calcButton, positionConst);

        positionConst.gridx = 1;
        positionConst.gridy = 3;
        positionConst.insets = new Insets(10, 10, 10, 10);
        add(resetButton, positionConst);
    }
    /* Method is automatically called when an event
       occurs (e.g, button is pressed) */
    @Override
    public void actionPerformed(ActionEvent event) {
        String wageInput, hoursInput;      // User specified hourly wage
        int hourlyWage;        // Hourly wage
        int hoursPerWeek;

        // Get user's wage input
        wageInput = wageField.getText();
        hoursInput = hoursField.getText();

        // Convert from String to an integer
        hourlyWage = Integer.parseInt(wageInput);
        hoursPerWeek= Integer.parseInt(hoursInput);

        // Display calculated salary
        salField.setText(Integer.toString(hourlyWage * hoursPerWeek * 50));
    }
    public void setResetButton(ActionEvent event){
        salField.setText("");
        wageField.setText("");
        hoursField.setText("");
    }

    public static void main(String[] args) {
        // Creates SalaryLabelFrame and its components
        Main myFrame = new Main();

        myFrame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        myFrame.pack();
        myFrame.setVisible(true);
    }
}
```
