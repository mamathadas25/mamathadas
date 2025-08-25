import csv
from datetime import datetime

def mark_attendance(student_name, status="Present"):
    """Records attendance for a student."""
    with open('attendance.csv', 'a', newline='') as file:
        writer = csv.writer(file)
        # Write header if file is empty
        if file.tell() == 0:
            writer.writerow(['Date', 'Time', 'Student Name', 'Status'])
        writer.writerow([datetime.now().strftime('%Y-%m-%d'), 
                         datetime.now().strftime('%H:%M:%S'), 
                         student_name, 
                         status])
    print(f"Attendance marked for {student_name} as {status}.")

def view_attendance():
    """Displays all recorded attendance."""
    try:
        with open('attendance.csv', 'r') as file:
            reader = csv.reader(file)
            for row in reader:
                print(', '.join(row))
    except FileNotFoundError:
        print("No attendance records found.")

# Example Usage:
if __name__ == "__main__":
    mark_attendance("Alice", "Present")
    mark_attendance("Bob", "Late")
    print("\n--- All Attendance Records ---")
    view_attendance()
