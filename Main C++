#include <iostream>
#include <vector>
#include <string>
#include <map>
#include <fstream>   // ✅ Added

using namespace std;

class Student {
public:
    string indexNumber;
    string name;

    Student(string idx, string n) : indexNumber(idx), name(n) {}

    void display() {
        cout << "Index: " << indexNumber << ", Name: " << name << endl;
    }
};

class AttendanceSession {
public:
    string courseCode;
    string date;
    map<string, string> attendance;

    AttendanceSession(string cc, string d) : courseCode(cc), date(d) {}

    void markAttendance(string index, string status) {
        attendance[index] = status;
    }
};

// ✅ Save function OUTSIDE main
void saveStudents(const vector<Student>& students) {
    ofstream file("students.txt");
    for (const auto& s : students) {
        file << s.indexNumber << "," << s.name << "\n";
    }
    file.close();
}

// ✅ Load function OUTSIDE main
vector<Student> loadStudents() {
    vector<Student> students;
    ifstream file("students.txt");
    string line;

    while (getline(file, line)) {
        size_t comma = line.find(',');
        if (comma != string::npos) {
            string idx = line.substr(0, comma);
            string name = line.substr(comma + 1);
            students.push_back(Student(idx, name));
        }
    }
    file.close();
    return students;
}

int main() {
    vector<Student> students = loadStudents(); // ✅ Load at start
    vector<AttendanceSession> sessions;
    int choice;

    do {
        cout << "\n--- MENU ---\n";
        cout << "1. Register student\n";
        cout << "2. Create Attendance Session\n";
        cout << "3. View students\n";
        cout << "4. Mark Attendance\n";
        cout << "5. Save Students\n";
        cout << "6. Exit\n";
        cout << "Enter choice: ";
        cin >> choice;
        cin.ignore();

        switch (choice) {
            case 1: {
                string idx, name;
                cout << "Enter index: ";
                cin >> idx;
                cin.ignore();
                cout << "Enter name: ";
                getline(cin, name);
                students.push_back(Student(idx, name));
                break;
            }

            case 2: {
                sessions.push_back(AttendanceSession("EE201", "2026-02-20"));
                cout << "Session created!\n";
                break;
            }

            case 3: {
                for (auto& s : students)
                    s.display();
                break;
            }

            case 4: {
                if (students.empty()) {
                    cout << "No students available.\n";
                } else {
                    cout << "Enter student index (0 to " 
                         << students.size() - 1 << "): ";
                    int idx;
                    cin >> idx;

                    if (idx >= 0 && idx < students.size()) {
                        cout << "Status (P/A/L): ";
                        string status;
                        cin >> status;

                        if (!sessions.empty())
                            sessions[0].markAttendance(
                                students[idx].indexNumber, status);
                    }
                }
                break;
            }

            case 5: {
                saveStudents(students);
                cout << "Students saved successfully!\n";
                break;
            }

            case 6:
                cout << "Exiting program...\n";
                break;

            default:
                cout << "Invalid choice!\n";
        }

    } while (choice != 6);

    return 0;
}
