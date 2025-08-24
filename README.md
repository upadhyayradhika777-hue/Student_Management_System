import java.util.*;

// Student class
class Student {
    private String name;
    private int rollNumber;
    private String grade;
    private String email;

    public Student(String name, int rollNumber, String grade, String email) {
        this.name = name;
        this.rollNumber = rollNumber;
        this.grade = grade;
        this.email = email;
    }

    public int getRollNumber() { return rollNumber; }
    public String getName() { return name; }
    public String getGrade() { return grade; }
    public String getEmail() { return email; }

    public void setName(String name) { this.name = name; }
    public void setGrade(String grade) { this.grade = grade; }
    public void setEmail(String email) { this.email = email; }

    @Override
    public String toString() {
        return "Roll No: " + rollNumber +
                ", Name: " + name +
                ", Grade: " + grade +
                ", Email: " + email;
    }
}

// Student Management System
class StudentManagementSystem {
    private List<Student> students;

    public StudentManagementSystem() {
        students = new ArrayList<>();
    }

    public void addStudent(Student student) {
        students.add(student);
    }

    public void removeStudent(int rollNumber) {
        students.removeIf(s -> s.getRollNumber() == rollNumber);
    }

    public Student searchStudent(int rollNumber) {
        for (Student s : students) {
            if (s.getRollNumber() == rollNumber) return s;
        }
        return null;
    }

    public void displayAllStudents() {
        if (students.isEmpty()) {
            System.out.println("No students found.");
        } else {
            for (Student s : students) {
                System.out.println(s);
            }
        }
    }
}

// Main class with UI
public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        StudentManagementSystem sms = new StudentManagementSystem();

        while (true) {
            System.out.println("\n--- Student Management System ---");
            System.out.println("1. Add Student");
            System.out.println("2. Remove Student");
            System.out.println("3. Search Student");
            System.out.println("4. Display All Students");
            System.out.println("5. Exit");
            System.out.print("Choose an option: ");

            int choice = sc.nextInt();
            sc.nextLine(); // consume newline

            switch (choice) {
                case 1:
                    System.out.print("Enter Roll Number: ");
                    int roll = sc.nextInt();
                    sc.nextLine();

                    if (sms.searchStudent(roll) != null) {
                        System.out.println("Student with this roll number already exists!");
                        break;
                    }

                    System.out.print("Enter Name: ");
                    String name = sc.nextLine().trim();

                    System.out.print("Enter Grade: ");
                    String grade = sc.nextLine().trim();

                    System.out.print("Enter Email: ");
                    String email = sc.nextLine().trim();

                    sms.addStudent(new Student(name, roll, grade, email));
                    System.out.println("Student added successfully!");
                    break;

                case 2:
                    System.out.print("Enter Roll Number to Remove: ");
                    int removeRoll = sc.nextInt();
                    sms.removeStudent(removeRoll);
                    System.out.println("Student removed if existed.");
                    break;

                case 3:
                    System.out.print("Enter Roll Number to Search: ");
                    int searchRoll = sc.nextInt();
                    Student s = sms.searchStudent(searchRoll);
                    if (s != null) {
                        System.out.println("Student Found: " + s);
                    } else {
                        System.out.println("Student not found.");
                    }
                    break;

                case 4:
                    sms.displayAllStudents();
                    break;

                case 5:
                    System.out.println("Exiting... Goodbye!");
                    sc.close();
                    return;

                default:
                    System.out.println("Invalid choice! Try again.");
            }
        }
    }
}
