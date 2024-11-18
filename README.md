# lab-5-complete

**lab task 1**

**1.	Write a program for Selection sort that sorts an array containing numbers, prints all the sort values of array each followed by its location.**

package com.mycompany.lab5labtask1;
import java.util.*;
public class Lab5labtask1 {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter the number of elements in the array: ");
        int n = scanner.nextInt();
        int[] arr = new int[n];
        System.out.println("Enter " + n + " elements:");
        for (int i = 0; i < n; i++) {
            arr[i] = scanner.nextInt();
        }
        System.out.println("\nSorting Process:");
        for (int i = 0; i < n - 1; i++) {
            int minIndex = i;
            for (int j = i + 1; j < n; j++) {
                if (arr[j] < arr[minIndex]) {
                    minIndex = j;
                }
            }
            int temp = arr[minIndex];
            arr[minIndex] = arr[i];
            arr[i] = temp;
            System.out.println("Step " + (i + 1) + ":");
            for (int k = 0; k < n; k++) {
                System.out.print("Value: " + arr[k] + " (Index: " + k + ") ");
            }
            System.out.println();
        }
        System.out.println("\nSorted Array:");
        for (int i = 0; i < n; i++) {
            System.out.println("Value: " + arr[i] + " (Index: " + i + ")");
        }
    }
}


**lab task 2**

**2.	Write a program that takes 10 numbers as input in an array. Sort the elements of array by using Bubble sort. Print each iteration of the sorting process.**

package com.mycompany.lab5labtask2;
import java.util.*;
public class Lab5labtask2 {
 public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int[] numbers = new int[10];
        System.out.println("Enter 10 numbers:");
        for (int i = 0; i < numbers.length; i++) {
            numbers[i] = scanner.nextInt();
        }
        System.out.println("Sorting process:");
        for (int i = 0; i < numbers.length - 1; i++) {
            for (int j = 0; j < numbers.length - 1 - i; j++) {
                if (numbers[j] > numbers[j + 1]) {
                    int temp = numbers[j];
                    numbers[j] = numbers[j + 1];
                    numbers[j + 1] = temp;
                }
            }
            System.out.print("Iteration " + (i + 1) + ": ");
            for (int num : numbers) {
                System.out.print(num + " ");
            }
            System.out.println();
        }
        System.out.println("Sorted array:");
        for (int num : numbers) {
            System.out.print(num + " ");
        }
    }
}


**lab task 3**

**3.	Write a program that takes 10 random numbers in an array. Sort the elements of array by using Merge sort applying recursive technique. Print each iteration of the sorting process.**

package com.mycompany.lab5labtask3;
import java.util.*;
public class Lab5labtask3 {
    private static void merge(int[] array, int left, int mid, int right) {
        int n1 = mid - left + 1;
        int n2 = right - mid;
        int[] leftArray = new int[n1];
        int[] rightArray = new int[n2];
        for (int i = 0; i < n1; i++) {
            leftArray[i] = array[left + i];
        }
        for (int j = 0; j < n2; j++) {
            rightArray[j] = array[mid + 1 + j];
        }
        int i = 0, j = 0, k = left;
        while (i < n1 && j < n2) {
            if (leftArray[i] <= rightArray[j]) {
                array[k] = leftArray[i];
                i++;
            } else {
                array[k] = rightArray[j];
                j++;
            }
            k++;
        }
        while (i < n1) {
            array[k] = leftArray[i];
            i++;
            k++;
        }
        while (j < n2) {
            array[k] = rightArray[j];
            j++;
            k++;
        }
    }
    private static void mergeSort(int[] array, int left, int right) {
        if (left < right) {
            int mid = left + (right - left) / 2;
            mergeSort(array, left, mid);
            mergeSort(array, mid + 1, right);
            merge(array, left, mid, right);
            System.out.println("After merging: " + Arrays.toString(array));
        }
    }
    public static void main(String[] args) {
        int[] array = {55, 87, 24, 17,78, 543, 58,7, 75, 24};
        System.out.println("Original array: " + Arrays.toString(array));
        mergeSort(array, 0, array.length - 1);
        System.out.println("Sorted array: " + Arrays.toString(array));
    }
}


**Home task 1**

**1.	Declare an array of size n to store account balances. Initialize with values 0 to 100000 and sort Account No’s according to highest balance values by using Quick sort, For e.g.: 
   Account No. 3547 Balance 28000 
   Account No. 1245 Balance 12000.**

package com.mycompany.lab5hometask1;
import java.util.*;
public class Lab5hometask1 {
static class Account {
        int accountNo;
        int balance;
        public Account(int accountNo, int balance) {
            this.accountNo = accountNo;
            this.balance = balance;
        }
        @Override
        public String toString() {
            return "Account No: " + accountNo + " Balance: " + balance;
        }
    }
    public static void quickSort(Account[] accounts, int low, int high) {
        if (low < high) {
            int pivotIndex = partition(accounts, low, high);
            quickSort(accounts, low, pivotIndex - 1);
            quickSort(accounts, pivotIndex + 1, high);
        }
    }
    private static int partition(Account[] accounts, int low, int high) {
        Account pivot = accounts[high];
        int i = low - 1;
        for (int j = low; j < high; j++) {
            if (accounts[j].balance > pivot.balance) {
                i++;
                Account temp = accounts[i];
                accounts[i] = accounts[j];
                accounts[j] = temp;
            }
        }
        Account temp = accounts[i + 1];
        accounts[i + 1] = accounts[high];
        accounts[high] = temp;
        return i + 1;
    }
    public static void main(String[] args) {
        Account[] accounts = {
            new Account(9857, 280008),
            new Account(3578, 1207500),
            new Account(1598, 5012879),
            new Account(1122, 75000),
            new Account(1000, 30044550)
        };
        System.out.println("Before sorting:");
        Arrays.stream(accounts).forEach(System.out::println);
        quickSort(accounts, 0, accounts.length - 1);
        System.out.println("\nAfter sorting (by balance in descending order):");
        Arrays.stream(accounts).forEach(System.out::println);
    }
}


**Home task 2**

   **2.	Write a program which takes an unordered list of integers (or any other objects e.g. String), you have to rearrange the list in their natural order using merge sort.**

package com.mycompany.lab5hometask2;
import java.util.*;
public class Lab5hometask2 {
    public static void main(String[] args) {
        Integer[] intArray = {65, 78, 24, 122, 54, 563, 78, 1};
        System.out.println("Unordered Integers: " + Arrays.toString(intArray));
        mergeSort(intArray);
        System.out.println("Sorted Integers: " + Arrays.toString(intArray));
        String[] stringArray = {"Aijaz", "Mobariz", "Hassam", "Wasay", "Khurram"};
        System.out.println("\nUnordered Strings: " + Arrays.toString(stringArray));
        mergeSort(stringArray);
        System.out.println("Sorted Strings: " + Arrays.toString(stringArray));
    }
    public static <T extends Comparable<T>> void mergeSort(T[] array) {
        if (array.length < 2) {
            return;
        } 
        int mid = array.length / 2;
        T[] left = Arrays.copyOfRange(array, 0, mid);
        T[] right = Arrays.copyOfRange(array, mid, array.length);  
        mergeSort(left); 
        mergeSort(right); 
        
        merge(array, left, right);
    }
    private static <T extends Comparable<T>> void merge(T[] array, T[] left, T[] right) {
        int i = 0, j = 0, k = 0;
        while (i < left.length && j < right.length) {
            if (left[i].compareTo(right[j]) <= 0) {
                array[k++] = left[i++];
            } else {
                array[k++] = right[j++];
            }
        }
        while (i < left.length) {
            array[k++] = left[i++];
        }
        while (j < right.length) {
            array[k++] = right[j++];
        }
    }
}


**Home task 3**

**3.	You are given an unordered list of integers or strings. Write a program to Take this list as input. Sort it in natural order using Merge Sort. For integers, this means ascending order. For strings, this means alphabetical order. Print the sorted list**

package com.mycompany.lab5hometask3;
import java.util.*;
public class Lab5hometask3 {
public static void merge(String[] array, String[] left, String[] right) {
        int i = 0, j = 0, k = 0;
        while (i < left.length && j < right.length) {
            if (left[i].compareTo(right[j]) <= 0) {
                array[k++] = left[i++];
            } else {
                array[k++] = right[j++];
            }
        }
        while (i < left.length) {
            array[k++] = left[i++];
        }
        while (j < right.length) {
            array[k++] = right[j++]; }}
    public static void mergeSort(String[] array) {
        if (array.length <= 1) return;
        int mid = array.length / 2;
        String[] left = Arrays.copyOfRange(array, 0, mid);
        String[] right = Arrays.copyOfRange(array, mid, array.length);
        mergeSort(left);
        mergeSort(right);
        merge(array, left, right);}
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("Input a list of elements separated by spaces, including both numbers and words:");
        String input = scanner.nextLine();
        String[] inputArray = input.split(" ");
        boolean isNumeric = true;
        for (String s : inputArray) {
            if (!s.matches("-?\\d+")) {
                isNumeric = false;
                break;  } }
        if (isNumeric) {
            Arrays.sort(inputArray, Comparator.comparingInt(Integer::parseInt));
        } else {
            mergeSort(inputArray);
        }
        System.out.println("Sorted list: " + String.join(" ", inputArray));
    }
}


**Home task 4**

**4.	You are given a set of bank accounts, each with a unique account number and a balance. Write a Java program to Declare an array of size n to store account balances. Initialize each balance randomly with values between 0 and 100,000. Sort the accounts in descending order of their balances using Quick Sort. Print the sorted list in the format.**

package com.mycompany.lab5hometask4;
import java.util.*;
public class Lab5hometask4 {
    public static void main(String[] args) {
        int n = 10;
        Account[] accounts = new Account[n];
        Random rand = new Random();
        for (int i = 0; i < n; i++) {
            accounts[i] = new Account("ACC" + (i + 1), rand.nextInt(100001));
        }
        System.out.println("Accounts before sorting:");
        printAccounts(accounts);
        quickSort(accounts, 0, n - 1);
        System.out.println("\nAccounts after sorting:");
        printAccounts(accounts);
    }
    public static void quickSort(Account[] arr, int low, int high) {
        if (low < high) {
            int pi = partition(arr, low, high);
            quickSort(arr, low, pi - 1);
            quickSort(arr, pi + 1, high);
        }
    }
    public static int partition(Account[] arr, int low, int high) {
        int pivot = arr[high].balance;
        int i = low - 1;
        for (int j = low; j < high; j++) {
            if (arr[j].balance >= pivot) { 
                i++;
                swap(arr, i, j);
            }
        }
        swap(arr, i + 1, high);
        return i + 1;
    }
    public static void swap(Account[] arr, int i, int j) {
        Account temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }
    public static void printAccounts(Account[] accounts) {
        for (Account account : accounts) {
            System.out.println("Account Number: " + account.accountNumber + ", Balance: " + account.balance);
        }
    }
}
class Account {
    String accountNumber;
    int balance;
    public Account(String accountNumber, int balance) {
        this.accountNumber = accountNumber;
        this.balance = balance;
    }
}
