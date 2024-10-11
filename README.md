#include <stdio.h>
#include <string.h>

int main() {
    int num_device_user, num_screentime;
    float time_spent, total_time, avg_time;
    char rating[100];

    // Asking the user for the number of device users with validation
    do {
        printf("Enter the number of device users: ");
        scanf("%d", &num_device_user);
        if (num_device_user <= 0) {
            printf("Invalid input! Number of device users must be greater than 0. Please try again.\n");
        }
    } while (num_device_user <= 0);  // Keep asking until valid input is provided

    // Asking the user for the number of apps with validation
    do {
        printf("Enter the number of apps you used today: ");
        scanf("%d", &num_screentime);
        if (num_screentime <= 0) {
            printf("Invalid input! Number of apps must be greater than 0. Please try again.\n");
        }
    } while (num_screentime <= 0);  // Keep asking until valid input is provided

    for (int i = 1; i <= num_device_user; i++) {
        total_time = 0;  // Reset total time for each user

        printf("\nPerson %d:\n", i);
        for (int j = 1; j <= num_screentime; j++) {
            // Get time spent on each app and check for invalid input
            do {
                printf("Enter time spent on APP %d (in hours): ", j);
                scanf("%f", &time_spent);

                if (time_spent < 0) {
                    printf("Invalid input! Time cannot be negative. Please try again.\n");
                }
            } while (time_spent < 0);  // Keep asking until valid input is provided

            total_time += time_spent;  // Accumulate total time
        }

        // Calculate average time spent on device
        avg_time = total_time / num_screentime;

        // Determine the rating based on the average time
        if (avg_time <= 1) {
            strcpy(rating, "Outstanding");
        } else if (avg_time <= 2) {
            strcpy(rating, "Good");
        } else if (avg_time <= 4) {
            strcpy(rating, "Spending too much time; it could affect your health");
        } else if (avg_time <= 5) {
            strcpy(rating, "You're crossing your limits, it may become an addiction");
        } else if (avg_time <= 6) {
            strcpy(rating, "Bad");
        } else {
            strcpy(rating, "Severely unhealthy screen time");
        }

        // Output the result
        printf("Person %d - Average Time Spent: %.2f hours, Rating: %s\n", i, avg_time, rating);
    }

    return 0;
}
