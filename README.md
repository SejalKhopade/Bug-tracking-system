# Bug-tracking-system
import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

class Bug {
    private String id;
    private String description;
    private boolean resolved;

    public Bug(String id, String description) {
        this.id = id;
        this.description = description;
        this.resolved = false;
    }

    public String getId() {
        return id;
    }

    public String getDescription() {
        return description;
    }

    public boolean isResolved() {
        return resolved;
    }

    public void resolve() {
        resolved = true;
    }
}

class BugTracker {
    private List<Bug> bugs;

    public BugTracker() {
        bugs = new ArrayList<>();
    }

    public void addBug(Bug bug) {
        bugs.add(bug);
    }

    public List<Bug> getBugs() {
        return bugs;
    }

    public Bug findBugById(String id) {
        for (Bug bug : bugs) {
            if (bug.getId().equals(id)) {
                return bug;
            }
        }
        return null;
    }

    public void resolveBug(String id) {
        Bug bug = findBugById(id);
        if (bug != null) {
            bug.resolve();
        } else {
            System.out.println("Bug not found.");
        }
    }
}

public class Main {
    public static void main(String[] args) {
        BugTracker bugTracker = new BugTracker();
        Scanner scanner = new Scanner(System.in);

        boolean exit = false;
        while (!exit) {
            System.out.println("\nBug Tracking System Menu:");
            System.out.println("1. Add a Bug");
            System.out.println("2. Resolve a Bug");
            System.out.println("3. List all Bugs");
            System.out.println("4. Exit");
            System.out.print("Enter your choice: ");
            int choice = scanner.nextInt();
            scanner.nextLine(); // Consume newline character

            switch (choice) {
                case 1:
                    System.out.print("Enter bug ID: ");
                    String id = scanner.nextLine();
                    System.out.print("Enter bug description: ");
                    String description = scanner.nextLine();
                    Bug newBug = new Bug(id, description);
                    bugTracker.addBug(newBug);
                    System.out.println("Bug added successfully.");
                    break;
                case 2:
                    System.out.print("Enter bug ID to resolve: ");
                    String resolveId = scanner.nextLine();
                    bugTracker.resolveBug(resolveId);
                    break;
                case 3:
                    List<Bug> allBugs = bugTracker.getBugs();
                    System.out.println("\nList of Bugs:");
                    for (Bug bug : allBugs) {
                        System.out.println("Bug ID: " + bug.getId());
                        System.out.println("Description: " + bug.getDescription());
                        System.out.println("Resolved: " + (bug.isResolved() ? "Yes" : "No"));
                        System.out.println("---------------------------");
                    }
                    break;
                case 4:
                    exit = true;
                    System.out.println("Exiting Bug Tracking System. Goodbye!");
                    break;
                default:
                    System.out.println("Invalid choice. Please enter a number between 1 and 4.");
                    break;
            }
        }
        scanner.close();
    }
}
