# Code-Asm-final
import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;
import java.util.Comparator;

public class Main {

    static List<Student> studentList = new ArrayList<>();

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int choice;

        do {
            System.out.println("MENU:");
            System.out.println("1. Nhập/Chèn mới thông tin sinh viên");
            System.out.println("2. In danh sách sinh viên ra màn hình");
            System.out.println("3. Xóa sinh viên theo mã code");
            System.out.println("4. Sắp xếp sinh viên theo thứ tự điểm giảm dần");
            System.out.println("5. Tìm kiếm sinh viên theo mã sinh viên hoặc tên sinh viên");
            System.out.println("6. Tìm kiếm sinh viên có điểm >= x");
            System.out.println("7. Thoát");
            System.out.print("Chọn chức năng: ");
            choice = scanner.nextInt();

            switch (choice) {
                case 1:
                    input(scanner);
                    break;
                case 2:
                    output();
                    break;
                case 3:
                    System.out.print("Nhập mã sinh viên cần xóa: ");
                    String codeToRemove = scanner.next();
                    removeByCode(codeToRemove);
                    break;
                case 4:
                    sortByGradeDesc();
                    System.out.println("Danh sách sinh viên sau khi sắp xếp:");
                    output();
                    break;
                case 5:
                    System.out.print("Nhập mã sinh viên hoặc tên sinh viên cần tìm: ");
                    scanner.nextLine(); // Consume newline
                    String keyword = scanner.nextLine();
                    Student student = findByCodeOrName(keyword);
                    if (student != null) {
                        System.out.println("Sinh viên được tìm thấy:");
                        System.out.println(student);
                    } else {
                        System.out.println("Không tìm thấy sinh viên.");
                    }
                    break;
                case 6:
                    System.out.print("Nhập giá trị x: ");
                    float x = scanner.nextFloat();
                    List<Student> filteredStudents = filterByGrade(x);
                    System.out.println("Danh sách sinh viên có điểm >= " + x + ":");
                    for (Student s : filteredStudents) {
                        System.out.println(s);
                    }
                    break;
                case 7:
                    System.out.println("Thoát chương trình.");
                    break;
                default:
                    System.out.println("Chọn sai chức năng! Vui lòng chọn lại.");
                    break;
            }
        } while (choice != 7);

        scanner.close();
    }

    // Nhap moi 1 sinh vien
    public static void input(Scanner scanner) {
        System.out.println("Nhap vao thong tin sinh vien:");

        System.out.println("Nhap ten sv:");
        scanner.nextLine(); // Consume newline
        String name = scanner.nextLine();

        System.out.println("Nhap tuoi sv:");
        int age = scanner.nextInt();

        System.out.println("Nhap email sv:");
        scanner.nextLine(); // Consume newline
        String email = scanner.nextLine();

        System.out.println("Nhap so dien thoai sv:");
        String phone = scanner.nextLine();

        System.out.println("Nhap ma sv:");
        String code = scanner.nextLine();

        System.out.println("Nhap gioi tinh sv (1 - Nam, 0 - Nu):");
        int gender = scanner.nextInt();

        System.out.println("Nhap diem:");
        float grade = scanner.nextFloat();

        Student student = new Student(name, age, email, phone, code, gender, grade);
        studentList.add(student);
    }

    // In danh sach sinh vien
    public static void output() {
        for (Student student : studentList) {
            System.out.println(student.toString());
        }
    }

    // Remove student by code
    public static void removeByCode(String code) {
        studentList.removeIf(student -> student.getCode().equals(code));
        System.out.println("Đã xóa sinh viên có mã " + code);
    }

    // Sort students by grade in descending order
    public static void sortByGradeDesc() {
        studentList.sort(Comparator.comparing(Student::getGrade).reversed());
    }

    // Find student by code or name
    public static Student findByCodeOrName(String keyword) {
        for (Student student : studentList) {
            if (student.getCode().equalsIgnoreCase(keyword) || student.getName().equalsIgnoreCase(keyword)) {
                return student;
            }
        }
        return null;
    }

    // Filter students by grade
    public static List<Student> filterByGrade(float x) {
        List<Student> filteredList = new ArrayList<>();
        for (Student student : studentList) {
            if (student.getGrade() >= x) {
                filteredList.add(student);
            }
        }
        return filteredList;
    }
}

class Student {
    private String name;
    private int age;
    private String email;
    private String phone;
    private String code;
    private int gender; // 1 - Male, 0 - Female
    private float grade;

    public Student(String name, int age, String email, String phone, String code, int gender, float grade) {
        this.name = name;
        this.age = age;
        this.email = email;
        this.phone = phone;
        this.code = code;
        this.gender = gender;
        this.grade = grade;
    }

    public String getName() {
        return name;
    }

    public int getAge() {
        return age;
    }

    public String getEmail() {
        return email;
    }

    public String getPhone() {
        return phone;
    }

    public String getCode() {
        return code;
    }

    public int getGender() {
        return gender;
    }

    public float getGrade() {
        return grade;
    }

    @Override
    public String toString() {
        return "Student{" +
                "name='" + name + '\'' +
                ", age=" + age +
                ", email='" + email + '\'' +
                ", phone='" + phone + '\'' +
                ", code='" + code + '\'' +
                ", gender=" + (gender == 1 ? "Male" : "Female") +
                ", grade=" + grade +
                '}';
    }
}
