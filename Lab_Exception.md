## Thought Process

![Lab_Exception drawio](https://github.com/suddy00/CISC_191_Int_Java/assets/17439019/e56c4c15-def2-4c51-bd9d-8720cd096873)


## Challenges
- Exceptions have to be nested in particular ways to get the desired result

## Code
```java
import java.util.Scanner;
import java.util.InputMismatchException;

public class Main {
    public static int MILE_LENGTH = 2000;
    public static void main(String[] args) {
        int stepsWalked;
        double milesWalked;
        Scanner input = new Scanner(System.in);

        boolean needInput = true;

        //Exception handling to only take 0 or a positive number
        while (needInput) { //Will loop until correct input is provided
                //Using nested "try" statements to catch different errors
            try {
                System.out.println("Please input the number of steps taken: ");
                try{stepsWalked = input.nextInt();

                    //No negative numbers allowed
                    if (stepsWalked < 0) {
                        throw new Exception("Exception: Negative step count entered. \n");
                    }
                    milesWalked = stepsToMiles(stepsWalked);
                    System.out.printf("You have walked %.2f miles", milesWalked);
                    needInput = false;
                }

                //No letters or other characters allowed
                catch(InputMismatchException e){
                    input.nextLine();
                    needInput = true;
                }

            } catch (Exception e) {
                System.out.println(e.getMessage());
            }
        }
    }

    //Calculates the amount of miles walked (steps/MILE_LENGTH) returns a double
    public static double stepsToMiles(int w){
        double miles = 0;
            if (w > 0) {
                miles = (double) w /MILE_LENGTH;
            }
        return miles;
    }
}
```
