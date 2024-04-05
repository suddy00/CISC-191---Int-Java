#Challenges
- I completed this project using two different methods.
   1. Deque allows my to both evaluate and remove each end of a word.
   2. Using a for loop I can store a string backwards into another string and compare the two.

  
```Java
import java.util.ArrayDeque;
import java.util.Deque;
import java.util.Scanner;

public class Main {

    public static void main(String[] args) {
        Scanner input = new Scanner(System.in);
        System.out.println("Input a word: ");

        String word = input.next();
        int width = word.length();

        Deque<Character> deque = new ArrayDeque<Character>();

        for(int i = 0; i < word.length(); i++){
            deque.add(Character.toLowerCase(word.charAt(i)));
        }

        while(width>1){
            if (deque.getFirst().equals(deque.getLast())) {
                deque.removeFirst();
                deque.removeLast();
                width -= 2;
            }
            else{width = -1;}
        }
        if (width == -1){
            System.out.println("No, " + word + " is not a palindrome.");
        }
        else{
            System.out.println("Yes, " + word + " is a palindrome." );
        }
    }
}
```
  
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
