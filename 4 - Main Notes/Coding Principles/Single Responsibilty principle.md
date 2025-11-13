
2024-09-12 21:10

Status:

Tags: #Backend

# Single Responsibility Principle (SRP)

## Overview
The **Single Responsibility Principle (SRP)** is one of the five SOLID principles of object-oriented design. It states that:

> A class should have one and only one reason to change, meaning that a class should only have one job or responsibility.

In other words, every class should be responsible for a single part of the functionality provided by the software, and that responsibility should be entirely encapsulated by the class. All of its services should be narrowly aligned with that responsibility.

## Key Concepts
- **Responsibility**: A responsibility is considered to be a reason for change. If a class has more than one responsibility, it has more than one reason to change.
- **Cohesion**: SRP promotes high cohesion within a class by keeping related functionality together and unrelated functionality out.
- **Separation of concerns**: SRP helps to divide software into distinct sections, each responsible for a specific piece of functionality. This makes the software easier to understand and maintain.

## Benefits
1. **Improved Readability**: When a class has a single responsibility, its purpose is clear, making it easier for developers to understand.
2. **Easier Maintenance**: Changes to one responsibility will only affect the classes related to that responsibility, reducing the risk of unintended side effects.
3. **Better Reusability**: Classes that adhere to SRP tend to be more modular and can often be reused in different contexts.
4. **Simpler Testing**: Unit testing becomes more straightforward since each class has a focused role with fewer dependencies.

## Example

### Bad Example: Violation of SRP
```cpp
class ReportGenerator {
    public:
        void generateReport() {
            // Generates a report
        }

        void saveToDatabase() {
            // Code to save the report to a database
        }

        void sendEmail() {
            // Code to send the report via email
        }
};
```

