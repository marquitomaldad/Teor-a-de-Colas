import java.util.Scanner;

public class LineasDeEsperaSimple {

    public static void main(String[] args) {

        Scanner sc = new Scanner(System.in);
        int opcion;

        do {
            System.out.println("\n===== MENÚ =====");
            System.out.println("1. Modelo M/M/1");
            System.out.println("2. Modelo M/M/C");
            System.out.println("3. Modelo M/M/1/K");
            System.out.println("4. Salir");
            System.out.print("Opción: ");
            opcion = sc.nextInt();

            if (opcion == 1) {
                System.out.print("Lambda (λ): ");
                double lambda = sc.nextDouble();
                System.out.print("Mu (μ): ");
                double mu = sc.nextDouble();
                mm1(lambda, mu);
            }

            else if (opcion == 2) {
                System.out.print("Lambda (λ): ");
                double lambda = sc.nextDouble();
                System.out.print("Mu (μ): ");
                double mu = sc.nextDouble();
                System.out.print("Número de servidores (c): ");
                int c = sc.nextInt();
                mmc(lambda, mu, c);
            }

            else if (opcion == 3) {
                System.out.print("Lambda (λ): ");
                double lambda = sc.nextDouble();
                System.out.print("Mu (μ): ");
                double mu = sc.nextDouble();
                System.out.print("Capacidad (K): ");
                int k = sc.nextInt();
                mm1k(lambda, mu, k);
            }

        } while (opcion != 4);

        System.out.println("Programa terminado.");
        sc.close();
    }

    // ============================
    //    M/M/1
    // ============================
    public static void mm1(double lambda, double mu) {

        if (lambda >= mu) {
            System.out.println("El sistema NO es estable (λ >= μ).");
            return;
        }

        double p = lambda / mu;
        double Lq = (lambda * lambda) / (mu * (mu - lambda));
        double Wq = Lq / lambda;
        double W = Wq + 1.0 / mu;
        double L = lambda * W;

        System.out.println("\n--- Resultados M/M/1 ---");
        System.out.println("ρ (utilización): " + p);
        System.out.println("Lq: " + Lq);
        System.out.println("Wq: " + Wq);
        System.out.println("W: " + W);
        System.out.println("L: " + L);
    }

    // ============================
    //    M/M/C
    // ============================
    public static void mmc(double lambda, double mu, int c) {

        double a = lambda / mu;
        double p = a / c;

        if (p >= 1) {
            System.out.println("El sistema NO es estable (ρ >= 1).");
            return;
        }

        // Cálculo de P0 (simplificado)
        double suma = 0;
        for (int i = 0; i < c; i++) {
            suma += Math.pow(a, i) / factorial(i);
        }
        double parte2 = Math.pow(a, c) / (factorial(c) * (1 - p));
        double P0 = 1 / (suma + parte2);

        // Lq (fórmula estándar)
        double Lq = (P0 * Math.pow(a, c) * p) /
                    (factorial(c) * Math.pow(1 - p, 2));

        double Wq = Lq / lambda;
        double W = Wq + 1.0 / mu;

        System.out.println("\n--- Resultados M/M/C ---");
        System.out.println("ρ: " + p);
        System.out.println("P0: " + P0);
        System.out.println("Lq: " + Lq);
        System.out.println("Wq: " + Wq);
        System.out.println("W: " + W);
    }

    // ============================
    //    M/M/1/K
    // ============================
    public static void mm1k(double lambda, double mu, int K) {

        double p = lambda / mu;

        double P0 = (1 - p) / (1 - Math.pow(p, K + 1));
        double PK = Math.pow(p, K) * P0;
        double lambdaE = lambda * (1 - PK);

        double L = (p * (1 - (K + 1) * Math.pow(p, K) + K * Math.pow(p, K + 1)))
                   / ((1 - p) * (1 - Math.pow(p, K + 1)));

        double W = L / lambdaE;

        System.out.println("\n--- Resultados M/M/1/K ---");
        System.out.println("ρ: " + p);
        System.out.println("P0: " + P0);
        System.out.println("PK: " + PK);
        System.out.println("λ efectivo: " + lambdaE);
        System.out.println("L: " + L);
        System.out.println("W: " + W);
    }

    // Factorial sencillo
    public static int factorial(int n) {
        int f = 1;
        for (int i = 1; i <= n; i++) {
            f *= i;
        }
        return f;
    }
}
