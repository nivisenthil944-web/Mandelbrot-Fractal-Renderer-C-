# Mandelbrot-Fractal-Renderer-C-
#include <stdio.h>
#include <complex.h>

#define WIDTH 100     // Number of columns
#define HEIGHT 40     // Number of rows
#define MAX_ITER 1000 // Iteration limit for escape time

int main(void) {
    // Bounds of the complex plane
    double xmin = -2.0, xmax = 1.0;
    double ymin = -1.0, ymax = 1.0;

    // Character palette for visualization
    const char *palette = " .:-=+*#%@";
    int palette_size = 10;

    for (int y = 0; y < HEIGHT; y++) {
        for (int x = 0; x < WIDTH; x++) {
            // Map pixel to complex plane
            double real = xmin + (xmax - xmin) * x / WIDTH;
            double imag = ymin + (ymax - ymin) * y / HEIGHT;
            double complex c = real + imag * I;
            double complex z = 0;

            int iter = 0;
            while (cabs(z) <= 2.0 && iter < MAX_ITER) {
                z = z * z + c;
                iter++;
            }

            // Choose character based on escape time
            char ch = palette[(iter * palette_size) / MAX_ITER];
            printf("%c", ch);
        }
        printf("\n");
    }

    return 0;
}
