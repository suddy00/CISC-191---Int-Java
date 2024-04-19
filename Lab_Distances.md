# Challenges
    Becoming familiar with GUI.
    Still working on figuring out alignment for the labels
    
# Output
![2024-04-19](https://github.com/suddy00/CISC_191_Int_Java/assets/17439019/2a20d554-0f59-450f-a9ea-18cca7d449b8)


```java
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.text.NumberFormat;
import javax.swing.*;

public class Main extends JFrame implements ActionListener {

    private static JFormattedTextField  tMiles;
    private  JTextField tKilometers;
    private  JTextField tMeters;
    private  JTextField tFeet;

    Main() {

        GridBagConstraints positionConst;

        // Set frame's title
        setTitle("Distances");

        // Label for input miles
        JLabel lMiles = new JLabel("Input Miles: ");

        //Conversion labels
        JLabel lKilometers = new JLabel("Kilometers: ");
        JLabel lMeters = new JLabel("Meters: ");
        JLabel lFeet = new JLabel("Feet: ");
        JButton convButton = new JButton("Convert");
        convButton.addActionListener(this);

        tMiles = new JFormattedTextField(NumberFormat.getNumberInstance());
        tMiles.setEditable(true);
        tMiles.setText("10");
        tMiles.setColumns(15); // Initial miles are 10

        tKilometers = new JTextField(15);
        tKilometers.setEditable(false);
        tKilometers.setText("");

        tMeters = new JTextField(15);
        tMeters.setEditable(false);
        tMeters.setText("");

        tFeet = new JTextField(15);
        tFeet.setEditable(false);
        tFeet.setText("");

        setLayout(new GridBagLayout());

        positionConst = new GridBagConstraints();
        positionConst.insets = new Insets(10, 10, 5, 1);
        positionConst.gridx = 0;
        positionConst.gridy = 0;
        add(lMiles, positionConst);

        positionConst = new GridBagConstraints();
        positionConst.insets = new Insets(5, 10, 20, 1);
        positionConst.gridx = 0;
        positionConst.gridy = 1;
        add(tMiles, positionConst);

        positionConst = new GridBagConstraints();
        positionConst.insets = new Insets(0, 10, 10, 10);
        positionConst.gridx = 1;
        positionConst.gridy = 1;
        add(convButton, positionConst);

        positionConst = new GridBagConstraints();
        positionConst.insets = new Insets(10, 10, 10, 1);
        positionConst.gridx = 0;
        positionConst.gridy = 2;
        add(lKilometers, positionConst);

        positionConst = new GridBagConstraints();
        positionConst.insets = new Insets(10, 10, 10, 1);
        positionConst.gridx = 1;
        positionConst.gridy = 2;
        add(tKilometers, positionConst);

        positionConst = new GridBagConstraints();
        positionConst.insets = new Insets(10, 10, 10, 1);
        positionConst.gridx = 0;
        positionConst.gridy = 3;
        add(lMeters, positionConst);

        positionConst = new GridBagConstraints();
        positionConst.insets = new Insets(10, 10, 10, 1);
        positionConst.gridx = 1;
        positionConst.gridy = 3;
        add(tMeters, positionConst);

        positionConst = new GridBagConstraints();
        positionConst.insets = new Insets(10, 10, 10, 1);
        positionConst.gridx = 0;
        positionConst.gridy = 4;
        add(lFeet, positionConst);

        positionConst = new GridBagConstraints();
        positionConst.insets = new Insets(10, 10, 10, 1);
        positionConst.gridx = 1;
        positionConst.gridy = 4;
        add(tFeet, positionConst);

    }
        public static void main(String[] args) {
        Main mainFrame = new Main();

        mainFrame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        mainFrame.pack();
        mainFrame.setVisible(true);
    }

    @Override
    public void actionPerformed(ActionEvent e) {
        double miles;
        double meters;
        double kilometers;
        double feet;

        miles = ((Number) tMiles.getValue()).doubleValue();
        kilometers = (miles * 1.609344);
        meters = (miles * 1609.344);
        feet = (miles * 5280);

        tKilometers.setText(Double.toString(kilometers));
        tMeters.setText(Double.toString(meters));
        tFeet.setText(Double.toString(feet));
    }
}
```
