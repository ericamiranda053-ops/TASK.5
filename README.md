using System;

class ReportCardApp
{
    static void Main()
    {
        Console.Write("Enter Total Students: ");
        int totalStudents;
        while (!int.TryParse(Console.ReadLine(), out totalStudents) || totalStudents <= 0)
        {
            Console.WriteLine("Invalid input. Enter a positive number.");
            Console.Write("Enter Total Students: ");
        }

        // Each student: [Name, English, Math, Computer, Total]
        string[,] studentData = new string[totalStudents, 5];

        for (int i = 0; i < totalStudents; i++)
        {
            Console.WriteLine($"Enter Student #{i + 1} Details:");

            // Input student name
            Console.Write("Enter Student Name: ");
            string name = Console.ReadLine();
            studentData[i, 0] = name;

            // Input English Marks
            studentData[i, 1] = GetValidatedMark("English");

            // Input Math Marks
            studentData[i, 2] = GetValidatedMark("Math");

            // Input Computer Marks
            studentData[i, 3] = GetValidatedMark("Computer");

            // Calculate total marks
            int total = int.Parse(studentData[i, 1]) + int.Parse(studentData[i, 2]) + int.Parse(studentData[i, 3]);
            studentData[i, 4] = total.ToString();

            Console.WriteLine("*********************************************");
        }

        // Sort students by total marks descending
        SortStudentsByTotal(studentData, totalStudents);

        // Display Report Card
        Console.WriteLine("****************Report Card*******************");
        Console.WriteLine("*********************************************");

        for (int i = 0; i < totalStudents; i++)
        {
            Console.WriteLine($"Student Name: {studentData[i, 0]}, Position: {i + 1}, Total: {studentData[i, 4]}/300");
            Console.WriteLine("*********************************************");
        }

        Console.WriteLine("Press any key to exit...");
        Console.ReadKey();
    }

    // Function to validate marks input
    static string GetValidatedMark(string subject)
    {
        int mark;
        Console.Write($"Enter {subject} Marks (Out Of 100): ");
        while (!int.TryParse(Console.ReadLine(), out mark) || mark < 0 || mark > 100)
        {
            Console.WriteLine("Invalid input. Enter a number between 0 and 100.");
            Console.Write($"Enter {subject} Marks (Out Of 100): ");
        }
        return mark.ToString();
    }

    // Function to sort students by total marks (descending)
    static void SortStudentsByTotal(string[,] data, int totalStudents)
    {
        for (int i = 0; i < totalStudents - 1; i++)
        {