#Challenges
- I found using Strings (character arrays) allows a shorter and less complicated approach to completing this project.
  
```Java
import java.util.Scanner;

public class Main {

    public static void main(String[] args) {
        Scanner input = new Scanner(System.in);
        System.out.println("Input a word: ");

        String word = input.next();
        String backWord="";

        //This for loop goes backwards to store word into backWord
        for(int i = word.length(); i>0; i--){
            backWord +=  word.charAt(i-1);
        }

        //Printing out both words just for giggles
        //System.out.print(word + " " + backWord);

        //Compares word and backWord (ignoring case) and prints out if they are equal
        if (word.equalsIgnoreCase(backWord)){
            System.out.println("\nYes," + word + " is a palindrome." );
        }
        else{
            System.out.println(("\nNo, " + word + " is not a palindrome."));
        }

    }
}
```
