#include <iostream>
#include <iomanip>
#include <cmath>
using namespace std;

// Fungsi 1
double f1(double x) {
    return pow(x, 2) - 2*x + 1;
}

// Fungsi 2
double f2(double x) {
    return pow(x, 3) - (x + 2) * exp(-2*x) + 1;
}

// Fungsi selisih (f2 - f1)
double f(double x) {
    return f2(x) - f1(x);
}

// Metode Biseksi
void bisection(double a, double b, double tol, int max_iter) {
    double fa = f(a), fb = f(b);

    if (fa * fb > 0) {
        cout << "Tidak ada akar di interval [" << a << ", " << b << "]" << endl;
        return;
    }

    cout << "\n=========== PENYELESAIAN PERSAMAAN NON-LINEAR METODE BISEKSI ===========\n";
    cout << left << setw(8) << "Iter"
         << setw(12) << "a"
         << setw(12) << "b"
         << setw(12) << "x"
         << setw(15) << "f(x)"
         << setw(15) << "f(a)"
         << setw(15) << "|b-a|" << endl;
    cout << string(80, '-') << endl;

    int i = 1;
    double x = 0, fx = 0;
    double error = b - a;

    while ((b - a) / 2 > tol && i <= max_iter) {
        x = (a + b) / 2;
        fx = f(x);

        cout << left << setw(8) << i
             << setw(12) << a
             << setw(12) << b
             << setw(12) << x
             << setw(15) << fx
             << setw(15) << fa
             << setw(15) << fabs(b-a)
             << endl;

        if (fabs(fx) < tol) break; // akar ketemu

        if (fa * fx < 0) {
            b = x;
            fb = fx;
        } else {
            a = x;
            fa = fx;
        }

        error = fabs(b - a); // update error
        i++;
    }

    cout << "\n=========== KESIMPULAN ===========\n";
    cout << "Akar ditemukan pada x = " << x << endl;
    cout << "Error akhir = " << error << endl;
    cout << "Berhenti pada iterasi ke-" << i << endl;
    cout << "=================================\n";
}

int main() {
    double a, b, tol;
    int max_iter;

    cout << "Input nilai a : "; cin >> a;
    cout << "Input nilai b : "; cin >> b;
    cout << "Input toleransi error : "; cin >> tol;
    cout << "Input iterasi maksimal N : "; cin >> max_iter;

    bisection(a, b, tol, max_iter);

    return 0;
}

