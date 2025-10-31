# ASSIGNMENT-WEEK-SEVEN
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

// Function prototypes
void weeklyRevenueTracker();
void roomOccupancySingleBranch();
void multipleBranchesOccupancy();

int main() {
    int choice;
    
    printf("=== Hotel Management System ===\n\n");
    
    do {
        printf("1. Weekly Revenue Tracker (1D Array)\n");
        printf("2. Room Occupancy - Single Branch (2D Array)\n");
        printf("3. Multiple Branches Occupancy (3D Array)\n");
        printf("4. Exit\n");
        printf("Enter your choice (1-4): ");
        scanf("%d", &choice);
        
        switch(choice) {
            case 1:
                weeklyRevenueTracker();
                break;
            case 2:
                roomOccupancySingleBranch();
                break;
            case 3:
                multipleBranchesOccupancy();
                break;
            case 4:
                printf("Exiting program. Goodbye!\n");
                break;
            default:
                printf("Invalid choice! Please try again.\n");
        }
        printf("\n");
    } while(choice != 4);
    
    return 0;
}

// 1D Array - Weekly Revenue Tracker
void weeklyRevenueTracker() {
    float revenue[7];
    char *days[] = {"Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday", "Sunday"};
    float total = 0, average;
    int i;
    
    printf("\n=== Weekly Revenue Tracker ===\n");
    
    // Input revenue for each day
    for(i = 0; i < 7; i++) {
        printf("Enter revenue for %s: $", days[i]);
        scanf("%f", &revenue[i]);
        total += revenue[i];
    }
    
    // Calculate average
    average = total / 7;
    
    // Display results
    printf("\n--- Weekly Revenue Report ---\n");
    for(i = 0; i < 7; i++) {
        printf("%s: $%.2f\n", days[i], revenue[i]);
    }
    printf("\nTotal Weekly Revenue: $%.2f\n", total);
    printf("Average Daily Revenue: $%.2f\n", average);
}

// 2D Array - Room Occupancy (Single Branch)
void roomOccupancySingleBranch() {
    int occupancy[5][10];  // 5 floors, 10 rooms per floor
    int floor, room;
    int occupied, vacant;
    
    printf("\n=== Room Occupancy - Single Branch ===\n");
    
    // Initialize random number generator
    srand(time(NULL));
    
    // Assign random occupancy (0 or 1)
    for(floor = 0; floor < 5; floor++) {
        for(room = 0; room < 10; room++) {
            occupancy[floor][room] = rand() % 2;  // Random 0 or 1
        }
    }
    
    // Display occupancy grid and calculate statistics
    printf("\n--- Occupancy Grid ---\n");
    printf("(1 = Occupied, 0 = Vacant)\n\n");
    
    for(floor = 0; floor < 5; floor++) {
        printf("Floor %d: ", floor + 1);
        for(room = 0; room < 10; room++) {
            printf("%d ", occupancy[floor][room]);
        }
        printf("\n");
    }
    
    // Calculate and display statistics per floor
    printf("\n--- Floor-wise Occupancy Report ---\n");
    for(floor = 0; floor < 5; floor++) {
        occupied = 0;
        vacant = 0;
        
        for(room = 0; room < 10; room++) {
            if(occupancy[floor][room] == 1) {
                occupied++;
            } else {
                vacant++;
            }
        }
        
        printf("Floor %d: Occupied = %d, Vacant = %d\n", floor + 1, occupied, vacant);
    }
    
    // Calculate total statistics
    int totalOccupied = 0, totalVacant = 0;
    for(floor = 0; floor < 5; floor++) {
        for(room = 0; room < 10; room++) {
            if(occupancy[floor][room] == 1) {
                totalOccupied++;
            } else {
                totalVacant++;
            }
        }
    }
    
    printf("\n--- Branch Summary ---\n");
    printf("Total Occupied Rooms: %d\n", totalOccupied);
    printf("Total Vacant Rooms: %d\n", totalVacant);
    printf("Occupancy Rate: %.2f%%\n", (float)totalOccupied / 50 * 100);
}

// 3D Array - Multiple Branches Occupancy
void multipleBranchesOccupancy() {
    int chain[3][5][10];  // 3 branches, 5 floors each, 10 rooms per floor
    int branch, floor, room;
    int totalOccupied = 0;
    
    printf("\n=== Multiple Branches Occupancy ===\n");
    
    // Initialize random number generator
    srand(time(NULL));
    
    // Assign random occupancy to all rooms across all branches
    for(branch = 0; branch < 3; branch++) {
        for(floor = 0; floor < 5; floor++) {
            for(room = 0; room < 10; room++) {
                chain[branch][floor][room] = rand() % 2;  // Random 0 or 1
            }
        }
    }
    
    // Display occupancy summary for each branch
    printf("\n--- Branch-wise Occupancy Summary ---\n");
    for(branch = 0; branch < 3; branch++) {
        int branchOccupied = 0;
        
        for(floor = 0; floor < 5; floor++) {
            for(room = 0; room < 10; room++) {
                if(chain[branch][floor][room] == 1) {
                    branchOccupied++;
                    totalOccupied++;
                }
            }
        }
        
        printf("Branch %d: %d occupied rooms out of 50\n", branch + 1, branchOccupied);
    }
    
    // Display detailed floor-wise occupancy for each branch
    printf("\n--- Detailed Floor-wise Report ---\n");
    for(branch = 0; branch < 3; branch++) {
        printf("\nBranch %d:\n", branch + 1);
        for(floor = 0; floor < 5; floor++) {
            int floorOccupied = 0;
            
            for(room = 0; room < 10; room++) {
                if(chain[branch][floor][room] == 1) {
                    floorOccupied++;
                }
            }
            
            printf("  Floor %d: %d occupied, %d vacant\n", floor + 1, floorOccupied, 10 - floorOccupied);
        }
    }
    
    // Display overall statistics
    int totalRooms = 3 * 5 * 10;  // 3 branches × 5 floors × 10 rooms
    printf("\n=== Overall Chain Summary ===\n");
    printf("Total Rooms across all branches: %d\n", totalRooms);
    printf("Total Occupied Rooms: %d\n", totalOccupied);
    printf("Total Vacant Rooms: %d\n", totalRooms - totalOccupied);
    printf("Overall Occupancy Rate: %.2f%%\n", (float)totalOccupied / totalRooms * 100);
}
