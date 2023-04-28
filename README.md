# assignment
#include <stdio.h>
#include <math.h>

#define NUM_TOWERS 3 // example number of towers

struct Tower {
    int x;
    int y;
    int quality;
};

int main() {
    struct Tower towers[NUM_TOWERS] = { // example towers data
        {1, 2, 5},
        {2, 1, 7},
        {3, 1, 9},
    };

    int radius = 2; // example radius

    int max_quality = 0;
    int cx = 0;
    int cy = 0;

    for (int x = 0; x <= 3; x++) { // range of x coordinates
        for (int y = 0; y <= 3; y++) { // range of y coordinates
            int network_quality = 0;
            for (int i = 0; i < NUM_TOWERS; i++) {
                int dx = towers[i].x - x;
                int dy = towers[i].y - y;
                int distance = sqrt(pow(dx, 2) + pow(dy, 2));
                if (distance <= radius) {
                    int signal_quality = towers[i].quality / (1 + distance);
                    network_quality += signal_quality;
                }
            }
            if (network_quality > max_quality) {
                max_quality = network_quality;
                cx = x;
                cy = y;
            } else if (network_quality == max_quality) {
                if (x < cx) {
                    cx = x;
                    cy = y;
                } else if (x == cx && y < cy) {
                    cy = y;
                }
            }
        }
    }

    printf("The integral coordinate with the maximum network quality is (%d, %d) with a network quality of %d.\n", cx, cy, max_quality);

    return 0;
}
