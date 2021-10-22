import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.FileReader;
import java.io.FileWriter;
import java.io.IOException;
import java.util.ArrayList;
import java.util.Collections;
import java.util.Comparator;
import java.util.*;
import java.io.*;
/**
 *
 * @author 
 */
public class Radix {
    public static void main(String[] s) {
        ArrayList al = new ArrayList();
            try {
                BufferedReader br = new BufferedReader(new FileReader("C:\\Users\\aidee\\Desktop\\Java\\Archivo.txt"));
                String line = br.readLine();
                while( line != null ) {
                    StringTokenizer parte = new StringTokenizer(line,",");
                    al.add(new estudiante(parte.nextToken().trim(),parte.nextToken().trim(),parte.nextToken().trim()));
                    line = br.readLine();
                }
            } catch(Exception e) {
                e.printStackTrace();
            }
        Object[] fields = al.toArray();
        System.out.println("Data before sorting");
        printAL(fields);
        Arrays.sort(fields,new radix());
        System.out.println("***************************************");
        System.out.println("Data after sorting");
        printAL(fields);
    }
    public static void printAL(Object[] fields) {
        for(int i=0; i < fields.length; i++) {
            System.out.println(fields[i]);
        }
    }
}

class radix{
    public static void radixSort(int[] arr) {
        int digit = getMaxDigit (arr); 
        for (int i = 0; i < digit; i++) {
            bucketSort (arr, i); 
        }
    }
 
    public static int getMaxDigit(int[] arr) {            
        int digit = 1; 
        int base = 10; 
        for (int i : arr) {
            while (i > base) {
                digit++;
                base *= 10;
            }
        }
        return digit;
    }
 
    public static void bucketSort(int[] arr, int digit) {
        int base = (int) Math.pow(10, digit);
        ArrayList<ArrayList<Integer>> buckets = new ArrayList<ArrayList<Integer>>();
        for (int i = 0; i <10; i ++) {
            buckets.add(new ArrayList<Integer>());
        }
        for (int i : arr) {
            int index = i / base % 10;
            buckets.get(index).add(i);
        }
        int index = 0;
        for (ArrayList<Integer> bucket : buckets) {
            for (int i : bucket) {
                arr[index++] = i;
            }
        }
    }    
}
    
class estudiante {
    String apellido;
    String nombre;
    String cuenta;
    estudiante(String apellido,String nombre,String cuenta) {
        this.apellido = apellido;
        this.nombre = nombre;
        this.cuenta = cuenta;
    }
    String getApellido() { return apellido; }
    String getNombre() { return nombre; }
    String getCuenta() { return cuenta; }
    public String toString() {
        return nombre+","+apellido+","+apellido+","+cuenta;
    }
}
