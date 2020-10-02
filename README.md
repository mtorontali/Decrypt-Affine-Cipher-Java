# Decrypt-Affine-Cipher-Java
A java program that decrypts affine cipher ciphertext.

```java
// Matthew Torontali
// 8/27/20
// Decrypt affine cipher in Java

import java.util.Scanner;

public class Affine {

    // find the multiplicative inverse of a within the group of integers between 0-26
    // if (a * i) % 26 == 1 then we have found the multiplicative inverse of a
    static int multiInverse(int a)
    {
        // declare variables
        int bool;
        int inverseOfA = 0;
        // find the multiplicative inverse of a within 0-26
        for (int i = 0; i < 26; i++)
        {
            bool = (a * i) % 26;
            if (bool == 1)
            {
                inverseOfA = i;
            }

        }
        return inverseOfA;
    }

    // Main method
    public static void main(String []args)
    {
        // initialize scanner object and variables
        Scanner scanner = new Scanner(System.in);
        String message;
        int a;
        int b;
        int m;
        int inverseOfA;
        int length;

        // get message and variables from user input
        System.out.println("Enter an encrypted message to decrypt: ");
        message = scanner.nextLine();
        // make sure message is all uppercase
        message = message.toUpperCase();
        System.out.println("Enter a key for a (must be coprime with m): ");
        a = scanner.nextInt();
        System.out.println("Enter a key for b (must be between 0 and m): ");
        b = scanner.nextInt();
        System.out.println("Enter a number for m: ");
        m = scanner.nextInt();

        // get length of message
        length = message.length();

        // Find the multiplicative inverse of a
        inverseOfA = (multiInverse(a));

        // Decrypt cipher text using decryption formula D(x) = a^-1(x-b)modm
        // We add 'A' here to get back to the correct ascii values
        // This iterates through the message character by character and decrypts it
        // We convert the ascii values back to readable text with the Character.toString method
        for (int i = 0; i < length; i++)
        {
            System.out.print(Character.toString(((inverseOfA * ((message.charAt(i) + 'A' - b)) % m)) + 'A'));
        }
        System.out.println("\n");
    }
}
```
