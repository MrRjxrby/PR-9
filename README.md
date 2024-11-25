// 9.1
```
class Student {
    private String name;
    private int iDNumber;

    public Student(String name, int iDNumber) {
        this.name = name;
        this.iDNumber = iDNumber;
    }

    public int getiDNumber() {
        return iDNumber;
    }

    public String getName() {
        return name;
    }

    @Override
    public String toString() {
        return "Студент{Имя='" + name + "', iD=" + iDNumber + '}';
    }
}

public class Main { 
    public static void insertionSort(Student[] students) {
        for (int i = 1; i < students.length; i++) {
            Student key = students[i];
            int j = i - 1;
            while (j >= 0 && students[j].getiDNumber() > key.getiDNumber()) {
                students[j + 1] = students[j];
                j--;
            }
            students[j + 1] = key;
        }
    }

    public static void main(String[] args) {
        Student[] students = {
            new Student("Паша", 103),
            new Student("Влад", 101),
            new Student("Сергей", 104),
            new Student("Аркаша", 102)
        };

        System.out.println("До сортировки:");
        for (Student student : students) {
            System.out.println(student);
        }

        // Сортируем массив методом вставок
        insertionSort(students);

        System.out.println("\nПосле сортировки:");
        for (Student student : students) {
            System.out.println(student);
        }
    }
}
```
// 9.2
```
import java.util.Arrays;
import java.util.Comparator;


class Student {
    private String name;
    private int gpa; 

    public Student(String name, int gpa) {
        this.name = name;
        this.gpa = gpa;
    }

    public String getName() {
        return name;
    }

    public int getGPA() {
        return gpa;
    }

    @Override
    public String toString() {
        return "Студент - {Имя='" + name + "', Баллы=" + gpa + '}';
    }
}

class SortingStudentsByGPA implements Comparator<Student> {
    @Override
    public int compare(Student s1, Student s2) {
        return Integer.compare(s2.getGPA(), s1.getGPA());
    }

    public void quickSort(Student[] students, int low, int high) {
        if (low < high) {
            int partitionIndex = partition(students, low, high);

            quickSort(students, low, partitionIndex - 1);
            quickSort(students, partitionIndex + 1, high);
        }
    }

    private int partition(Student[] students, int low, int high) {
        Student pivot = students[high];
        int i = low - 1;

        for (int j = low; j < high; j++) {
            if (compare(students[j], pivot) < 0) {
                i++;
                Student temp = students[i];
                students[i] = students[j];
                students[j] = temp;
            }
        }

        Student temp = students[i + 1];
        students[i + 1] = students[high];
        students[high] = temp;

        return i + 1;
    }
}
```
// 9.3
```
import java.util.ArrayList;
import java.util.List;

class Student implements Comparable<Student> {
    private String name;
    private int gpa; 

    public Student(String name, int gpa) {
        this.name = name;
        this.gpa = gpa;
    }

    public String getName() {
        return name;
    }

    public int getGPA() {
        return gpa;
    }

    @Override
    public String toString() {
        return "Студент - {Имя='" + name + "', Баллы=" + gpa + '}';
    }

    @Override
    public int compareTo(Student other) {
        return Integer.compare(this.gpa, other.gpa); // Сравнение по Баллам
    }
}

class MergeSortStudents {

    public static List<Student> mergeSort(List<Student> students) {
        if (students.size() <= 1) {
            return students; 
        }
        int mid = students.size() / 2;
        List<Student> left = students.subList(0, mid);
        List<Student> right = students.subList(mid, students.size());
        left = mergeSort(new ArrayList<>(left));
        right = mergeSort(new ArrayList<>(right));
        return merge(left, right);
    }

    private static List<Student> merge(List<Student> left, List<Student> right) {
        List<Student> merged = new ArrayList<>();
        int i = 0, j = 0;

        while (i < left.size() && j < right.size()) {
            if (left.get(i).compareTo(right.get(j)) <= 0) {
                merged.add(left.get(i));
                i++;
            } else {
                merged.add(right.get(j));
                j++;
            }
        }

        while (i < left.size()) {
            merged.add(left.get(i));
            i++;
        }

        while (j < right.size()) {
            merged.add(right.get(j));
            j++;
        }

        return merged;
    }
}

public class Main {
    public static void main(String[] args) {
        // Первый список
        List<Student> list1 = new ArrayList<>();
        list1.add(new Student("Паша", 85));
        list1.add(new Student("Влад", 90));
        list1.add(new Student("Сергей", 100));

        // Второй список 
        List<Student> list2 = new ArrayList<>();
        list2.add(new Student("Евгений", 88));
        list2.add(new Student("Вова", 95));
        list2.add(new Student("Глеб", 80));

        System.out.println("Список 1:");
        for (Student student : list1) {
            System.out.println(student);
        }

        System.out.println("\nСписок 2:");
        for (Student student : list2) {
            System.out.println(student);
        }

        List<Student> mergedList = new ArrayList<>();
        mergedList.addAll(list1);
        mergedList.addAll(list2);

        List<Student> sortedList = MergeSortStudents.mergeSort(mergedList);

        System.out.println("\nОбъединенный и отсортированный список:");
        System.out.println("\nКВБО-05-23:");
        for (Student student : sortedList) {
            System.out.println(student);
        }
    }
}
```
//9.4
```
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;

class Student implements Comparable<Student> {
    private String name;
    private int gpa; 

    public Student(String name, int gpa) {
        this.name = name;
        this.gpa = gpa;
    }

    public String getName() {
        return name;
    }

    public int getGPA() {
        return gpa;
    }

    @Override
    public String toString() {
        return "Студент - {Имя ='" + name + "', Баллы =" + gpa + '}';
    }

    @Override
    public int compareTo(Student other) {
        return this.name.compareTo(other.name);
    }
}
// Сортировка идет по Имени
public class Main {
    public static void main(String[] args) {
        List<Student> students = new ArrayList<>();
        students.add(new Student("Сергей", 85));
        students.add(new Student("Влад", 65));
        students.add(new Student("Павел", 75));

        System.out.println("Список до сортировки:");
        for (Student student : students) {
            System.out.println(student);
        }
        Collections.sort(students);

        System.out.println("\nСписок после сортировки:");
        for (Student student : students) {
            System.out.println(student);
        }
    }
}
```
