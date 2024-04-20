
# Output
![2024-04-20 (1)](https://github.com/suddy00/CISC_191_Int_Java/assets/17439019/11867d4f-82b5-4f15-8c06-c1a0e2969d28)


```java
import java.awt.GridBagConstraints;
import java.awt.GridBagLayout;
import java.awt.Insets;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JSpinner;
import javax.swing.JTextField;
import javax.swing.SpinnerNumberModel;
import javax.swing.event.ChangeEvent;
import javax.swing.event.ChangeListener;

public class Main extends JFrame implements ChangeListener {
    private JSpinner milesSpinner;    // Triggers travel time calculation
    private JTextField kilometersField; // Displays dog's age in human years
    private JLabel milesLabel;        // Label for dog years
    private JLabel kilometersLabel;     // Label for human years

    /* Constructor creates GUI components and adds GUI components
       using a GridBagLayout. */
    Main() {
        int startM;     // Spinner initial value display
        int minM;      // Spinner min value
        int maxM;      // Spinner max value
        int stepVal;      // Spinner step

        startM = 0;
        minM = 0;
        maxM = 15;
        stepVal = 1;

        // Used to specify GUI component layout
        GridBagConstraints layoutConst = null;

        // Specifies the types of values displayed in spinner
        SpinnerNumberModel spinnerModel = null;

        // Set frame's title
        setTitle("Distance");

        // Create labels
        milesLabel = new JLabel("Miles");
        kilometersLabel = new JLabel("Kilometers");

        // Create a spinner model, the spinner, and set the change listener
        spinnerModel = new SpinnerNumberModel(startM, minM, maxM, stepVal);
        milesSpinner = new JSpinner(spinnerModel);
        milesSpinner.addChangeListener(this);

        // Create field
        kilometersField = new JTextField(15);
        kilometersField.setEditable(false);
        kilometersField.setText("0 - 15");

        // Use a GridBagLayout
        setLayout(new GridBagLayout());

        // Specify component's grid location
        layoutConst = new GridBagConstraints();
        layoutConst.insets = new Insets(10, 10, 10, 1);
        layoutConst.anchor = GridBagConstraints.LINE_END;
        layoutConst.gridx = 0;
        layoutConst.gridy = 0;
        add(milesLabel, layoutConst);

        layoutConst = new GridBagConstraints();
        layoutConst.insets = new Insets(10, 1, 10, 10);
        layoutConst.fill = GridBagConstraints.HORIZONTAL;
        layoutConst.gridx = 1;
        layoutConst.gridy = 0;
        add(milesSpinner, layoutConst);

        layoutConst = new GridBagConstraints();
        layoutConst.insets = new Insets(10, 10, 10, 1);
        layoutConst.anchor = GridBagConstraints.LINE_END;
        layoutConst.gridx = 0;
        layoutConst.gridy = 1;
        add(kilometersLabel, layoutConst);

        layoutConst = new GridBagConstraints();
        layoutConst.insets = new Insets(10, 1, 10, 10);
        layoutConst.fill = GridBagConstraints.HORIZONTAL;
        layoutConst.gridx = 1;
        layoutConst.gridy = 1;
        add(kilometersField, layoutConst);
    }

    @Override
    public void stateChanged(ChangeEvent event) {
        Integer miles;     // Dog age input
        //double kilometers;
        miles = (Integer) milesSpinner.getValue();

        // Choose output based on dog's age component
        switch (miles) {

            case 0:
                kilometersField.setText(String.valueOf(0*0.6214));
                break;

            case 1:
                kilometersField.setText(String.valueOf(1*0.6214));
                break;

            case 2:
                kilometersField.setText(String.valueOf(2*0.6214));
                break;

            case 3:
                kilometersField.setText(String.valueOf(3*0.6214));
                break;

            case 4:
                kilometersField.setText(String.valueOf(4*0.6214));
                break;

            case 5:
                kilometersField.setText(String.valueOf(5*0.6214));
                break;

            case 6:
                kilometersField.setText(String.valueOf(6*0.6214));
                break;

            case 7:
                kilometersField.setText(String.valueOf(7*0.6214));
                break;

            case 8:
                kilometersField.setText(String.valueOf(8*0.6214));
                break;

            case 9:
                kilometersField.setText(String.valueOf(9*0.6214));
                break;

            case 10:
                kilometersField.setText(String.valueOf(10*0.6214));
                break;

            case 11:
                kilometersField.setText(String.valueOf(11*0.6214));
                break;

            case 12:
                kilometersField.setText(String.valueOf(12*0.6214));
                break;

            case 13:
                kilometersField.setText(String.valueOf(13*0.6214));
                break;

            case 14:
                kilometersField.setText(String.valueOf(14*0.6214));
                break;

            case 15:
                kilometersField.setText(String.valueOf(15*0.6214));
                break;
        }
    }

    /* Creates a DogYearsFrame and makes it visible */
    public static void main(String[] args) {
        // Creates DogYearsFrame and its components
        Main myFrame = new Main();

        myFrame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        myFrame.pack();
        myFrame.setVisible(true);
    }
}
```
