
Imports System
Public Class Student
   
    Public Property Name As String
    Public Property Age As Integer
    Public Property Grade As String


    Public Sub New(ByVal Optional name As String = "", ByVal Optional age As Integer = 0, ByVal Optional grade As String = "")
        Me.Name = name
        Me.Age = age
        Me.Grade = grade
    End Sub


    Public Sub DisplayDetails()
        Console.WriteLine("Name: " & Name)
        Console.WriteLine("Age: " & Age)
        Console.WriteLine("Grade: " & Grade)
    End Sub
End Class

Module Program
    Dim students As New List(Of Student)()

    Sub Main(args As String())
        Dim choice As Integer
        Do
            Console.WriteLine("Menu:")
            Console.WriteLine("1. Add Student")
            Console.WriteLine("2. Display Student Details")
            Console.WriteLine("3. Update Student Details")
            Console.WriteLine("4. Delete Student")
            Console.WriteLine("5. Exit")
            Console.Write("Enter your choice: ")
            choice = Convert.ToInt32(Console.ReadLine())

            Select Case choice
                Case 1
                    AddStudent()
                Case 2
                    DisplayStudentDetails()
                Case 3
                    UpdateStudentDetails()
                Case 4
                    DeleteStudent()
                Case 5
                    Console.WriteLine("Exiting the program...")
                Case Else
                    Console.WriteLine("Invalid choice. Please enter a valid option.")
            End Select
            Console.WriteLine()
        Loop While choice <> 5

        Console.ReadLine()
    End Sub

    Sub AddStudent()
        Console.Write("Enter student name: ")
        Dim name As String = Console.ReadLine()
        Console.Write("Enter student age: ")
        Dim age As Integer = Convert.ToInt32(Console.ReadLine())
        Console.Write("Enter student grade: ")
        Dim grade As String = Console.ReadLine()
        Dim newStudent As New Student(name, age, grade)
        students.Add(newStudent)
        Console.WriteLine("Student added successfully!")
    End Sub


    Sub DisplayStudentDetails()
        If students.Count > 0 Then
            For Each student In students
                Console.WriteLine("Student Details:")
                student.DisplayDetails()
                Console.WriteLine()
            Next
        Else
            Console.WriteLine("No students added yet.")
        End If
    End Sub


    Sub UpdateStudentDetails()
        If students.Count > 0 Then
            Console.Write("Enter student name to update details: ")
            Dim searchName As String = Console.ReadLine()
            Dim found As Boolean = False
            For Each student In students
                If student.Name = searchName Then
                    Console.Write("Enter new age for " & student.Name & ": ")
                    student.Age = Convert.ToInt32(Console.ReadLine())
                    Console.Write("Enter new grade for " & student.Name & ": ")
                    student.Grade = Console.ReadLine()
                    found = True
                    Console.WriteLine("Student details updated successfully!")
                    Exit Sub
                End If
            Next
            If Not found Then
                Console.WriteLine("Student not found.")
            End If
        Else
            Console.WriteLine("No students added yet.")
        End If
    End Sub


    Sub DeleteStudent()
        If students.Count > 0 Then
            Console.Write("Enter student name to delete: ")
            Dim searchName As String = Console.ReadLine()
            Dim foundIndex As Integer = -1
            For i = 0 To students.Count - 1
                If students(i).Name = searchName Then
                    foundIndex = i
                    Exit For
                End If
            Next
            If foundIndex <> -1 Then
                students.RemoveAt(foundIndex)
                Console.WriteLine("Student deleted successfully!")
            Else
                Console.WriteLine("Student not found.")
            End If
        Else
            Console.WriteLine("No students added yet.")
        End If
    End Sub
    
