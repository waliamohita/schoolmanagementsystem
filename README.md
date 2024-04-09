# schoolmanagementsystem
import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

class Student {
    private String name;
    private int rollNumber;
    private List<Integer> testScores;

    public Student(String name, int rollNumber) {
        this.name = name;
        this.rollNumber = rollNumber;
        this.testScores = new ArrayList<>();
    }

    public String getName() {
        return name;
    }

    public int getRollNumber() {
        return rollNumber;
    }

    public List<Integer> getTestScores() {
        return testScores;
    }

    public void addTestScore(int score) {
        testScores.add(score);
    }

    public double calculateAverageScore() {
        if (testScores.isEmpty()) {
            return 0.0;
        }
        int sum = 0;
        for (int score : testScores) {
            sum += score;
        }
        return (double) sum / testScores.size();
    }
}

class SchoolManagementSystem {
    private List<Student> students;

    public SchoolManagementSystem() {
        students = new ArrayList<>();
    }

    public void addStudent(Student student) {
        students.add(student);
    }

    public void displayAllStudents() {
        System.out.println("List of Students:");
        for (Student student : students) {
            System.out.println("Name: " + student.getName() + ", Roll Number: " + student.getRollNumber() + ", Average Score: " + student.calculateAverageScore());
        }
    }

    public void addTestScore(int rollNumber, int score) {
        for (Student student : students) {
            if (student.getRollNumber() == rollNumber) {
                student.addTestScore(score);
                System.out.println("Test score added successfully for " + student.getName());
                return;
            }
        }
        System.out.println("Student with roll number " + rollNumber + " not found.");
    }
}

public class SchoolManagement {
    public static void main(String[] args) {
        SchoolManagementSystem schoolManagement = new SchoolManagementSystem();

        // Adding some sample students
        schoolManagement.addStudent(new Student("Alice", 101));
        schoolManagement.addStudent(new Student("Bob", 102));

        Scanner scanner = new Scanner(System.in);

        while (true) {
            System.out.println("1. Display All Students");
            System.out.println("2. Add Test Scores for a Student");
            System.out.println("3. Exit");
            System.out.print("Enter your choice: ");
            int choice = scanner.nextInt();

            if (choice == 3) {
                System.out.println("Thank you for using School Management System.");
                break;
            }

            switch (choice) {
                case 1:
                    schoolManagement.displayAllStudents();
                    break;
                case 2:
                    System.out.print("Enter Roll Number of the Student: ");
                    int rollNumber = scanner.nextInt();
                    System.out.print("Enter Test Score: ");
                    int score = scanner.nextInt();
                    schoolManagement.addTestScore(rollNumber, score);
                    break;
                default:
                    System.out.println("Invalid choice!");
            }
        }

        scanner.close();
    }
}

