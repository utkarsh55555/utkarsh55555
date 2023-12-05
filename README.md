#student management system using csv files
import csv
student_fields=['rollno','name','age','email','phone']
student_database='students.csv'
def display_menu():
    print("----------------------------------------")
    print("welcome to student management system")
    print("----------------------------------------")
    print("1 add new student")
    print("2 view students")
    print("3 search student")
    print("4 update student")
    print("5 delete student")
    print("6 quit")
def add_student():
    print("--------------------------")
    print("Add Student Information")
    print("--------------------------")
    global student_fields
    global student_database
    
    student_data=[]
    for field in student_fields:
        value=input("enter "+field+" :")
        student_data.append(value)
    with open(student_database,"a",encoding="utf-8") as f:
        writer=csv.writer(f)
        writer.writerows([student_data])
    print("data saved successfully")
    input("press any key to continue")
    return
def view_students():
    global student_fields
    global student_database

    print("-------student records-------")

    with open(student_database,"r",encoding="utf-8") as f:
        reader=csv.reader(f)
        for x in student_fields:
            print(x,end='\t |')
        print("\n--------------------------------------")
        for row in reader:
            for item in row:
                print(item,end='\t |')
            print("\n")          
    input("press any key to continue")
def search_student():
    global student_fields
    global student_database

    print("----Search student----")
    roll=input("enter rollno to be searched :")
    with open(student_database,"r",encoding="utf-8") as f:
        reader=csv.reader(f)
        for row in reader:
            if len(row)>0:
                if roll==row[0]:
                    print("-----student found-----")
                    print("Rollno:",row[0])
                    print("Name:",row[1])
                    print("Age;",row[2])
                    print("Email:",row[3])
                    print("phone:",row[4])
                    break
        else:
            print("Rollno not found in the database")
        input("press any key to continue")
def update_student():
    global student_fields
    global student_database
    
    print("----Update student----")
    roll=input("enter roll no that is to be updated:")
    index_student=None
    update_data=[]
    with open(student_database,"r",encoding="utf-8") as f:
        reader=csv.reader(f)
        counter=0
        for row in reader:
            if len(row)>0:
                if roll==row[0]:
                    index_statement=counter
                    print("student found at index:",index_statement)
                    student_data=[]
                    for field in student_fields:
                        value=input("enter"+field+":")
                        student_data.append(value)
                    update_data.append(student_data)
                else:
                    update_data.append(row)
                counter+=1
                if index_student is not None:
                    with open(student_database,"w",encoding="utf-8") as f:
                              writer=writer.csv(f)
                              writer.writerows(updated_data)
                else:
                    print("Rollno not found in our database")
                input("press any key to continue")
def delete_student():
    global student_fields
    global student_database

    print("-----Delete student-----")
    roll=input("enter roll no to delete:")
    student_found= False
    updated_data=[]
    with open(student_database,"r",encoding="utf-8") as f:
        reader=csv.reader(f)
        counter=0
        for row in reader:
            if len(row)>0:
                if roll!=row[0]:
                    updated_data.append(row)
                    counter+=1
                else:
                    student_found=True
    if student_found is True:
         with open(student_database,"w",encoding="utf-8") as f:
             writer=csv.writer(f)
             writer.writerows(updated_data)
         print("Rollno:",roll,"deleted successfully")
    else:
         print("roll no not found in our database")
    input("press any key to continue")
while True:
    display_menu()
    choice=input("enter your choice 1-6")
    if choice=='1':
        add_student()
    elif choice=='2':
        view_students()
    elif choice=='3':
        search_student()
    elif choice=='4':
        update_student()
    elif choice=='5':
        delete_student()
    else:
        break
print("--------------------------------")
print("Thank you for using our system")
print("--------------------------------")
                

