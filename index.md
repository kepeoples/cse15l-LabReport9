# Lab Report 5

*STUDENT:*

Hi everyone,    
I'm having trouble running my Java program. I'm trying to run the Main class, but I keep getting the following error message:    
*Exception in thread "main" java.lang.NullPointerException at Main.readInput(Main.java:12) at Main.main(Main.java:6)"*  
I think the issue might be with the input file, but I'm not sure. Can anyone help me out?    

*TA:*

Hello there,  
I appreciate you getting in touch. Could you try executing the following command and report back to me with your findings?
```java -cp . Main input.txt```

*STUDENT:*
  
 Hey, I tried the command and this was my outcome:

*TA:*
  
Hi,  
So, this result reveals that the issue is a NullPointerException of the readInput method. The software is crashing as a result of the input variable being null.     
We must initialize the input variable to a non-null value in order to resolve this problem. This is how the code ought to appear:   
```import java.io.File;
import java.io.FileNotFoundException;
import java.util.Scanner;

public class Main {
    private static final String INPUT_FILE = "input.txt";

    public static void main(String[] args) {
        String input = readInput(INPUT_FILE);
        System.out.println("Input: " + input);
    }

    private static String readInput(String filename) {
        try {
            Scanner scanner = new Scanner(new File(filename));
            return scanner.nextLine();
        } catch (FileNotFoundException e) {
            System.err.println("File not found: " + filename);
            System.exit(1);
            return null;
        }
    }
}
```   

Also, following is the file and directory structure you might need:
```.
├── Main.java
├── input.txt
└── run.sh
```

**Contents of every file prior to bug fixation:**
1) Main.java:  
```import java.io.File;
import java.io.FileNotFoundException;
import java.util.Scanner;

public class Main {
    private static final String INPUT_FILE = "input.txt";

    public static void main(String[] args) {
        String input = readInput(INPUT_FILE);
        System.out.println("Input: " + input);
    }

    private static String readInput(String filename) {
        try {
            Scanner scanner = new Scanner(new File(filename));
            return scanner.nextLine();
        } catch (FileNotFoundException e) {
            System.err.println("File not found: " + filename);
            System.exit(1);
        }
        return null;
    }
}
```
2) input.txt:      
```Hello, world!```
3) run.sh:
``` 
#!/bin/bash  
javac Main.java  
java -cp . Main  
```

**Description of what to edit to fix the bug:     
In the readInput method, initialize the input variable to a non-null value**
```private static String readInput(String filename) {
    String input = null;
    try {
        Scanner scanner = new Scanner(new File(filename));
        input = scanner.nextLine();
    } catch (FileNotFoundException e) {
        System.err.println("File not found: " + filename);
        System.exit(1);
    }
    return input;
}
```
