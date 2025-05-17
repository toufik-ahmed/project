class StudentDatabase:
    student_list = []

    def add_student(self, student):
        self.student_list.append(student)


class Student(StudentDatabase):
    def __init__(self, student_id, name, department, is_enrolled):
        self.__student_id = student_id
        self.__name = name
        self.__department = department
        self.__is_enrolled = is_enrolled
        self.student_list.append(self)

    def enroll_student(self):
        if not self.__is_enrolled:
            self.__is_enrolled = True
            print(f"{self.__name} has been enrolled.")
        else:
            print(f"{self.__name} is already enrolled.")

    def drop_student(self):
        if self.__is_enrolled:
            self.__is_enrolled = False
            print(f"{self.__name} has been dropped.")
        else:
            print(f"{self.__name} is already not enrolled.")

    def view_student_info(self):
        print('---- Here is your Student’s details -------')
        print(f'Student name: {self.__name}')
        print(f'Student id: {self.__student_id}')
        print(f'Student department: {self.__department}')
        print(f'Enrollment status: {"Enrolled" if self.__is_enrolled else "Not Enrolled"}')

    def get_student_id(self):
        return self.__student_id



s1 = Student("101", "Toufik", "CSE", False)
s2 = Student("102", "Shimon", "EEE", True)
s3 = Student("103", "Touki", "BBA", False)



def menu():
    while True:
        print("\n---------- Student Management System --------")
        print("1. View All Students")
        print("2. Enroll Student")
        print("3. Drop Student")
        print("4. Exit")
        choice = input("Enter your choice: ")

        if choice == '1':
            for student in Student.student_list:
                student.view_student_info()

        elif choice == '2':
            s_id = input("Enter Student ID : ")
            found = False
            for student in Student.student_list:
                if student.get_student_id() == s_id:
                    student.enroll_student()
                    found = True
                    break
            if not found:
                print("Student ID not found!")

        elif choice == '3':
            s_id = input("Enter Student ID to drop: ")
            found = False
            for student in Student.student_list:
                if student.get_student_id() == s_id:
                    student.drop_student()
                    found = True
                    break
            if not found:
                print("Student ID not found!")

        elif choice == '4':
            print("Tata bye bye")
            break

        else:
            print("Invalid choice. Please try again.")



menu()
