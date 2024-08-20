package banco;
import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

public class TarjetaValidador {

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        List<String> tarjetas = new ArrayList<>();

        while (tarjetas.size() < 5) {
            System.out.print("Ingrese el número de tarjeta: ");
            String tarjeta = scanner.nextLine();

            if (tarjeta.length() == 16) {
                tarjetas.add(tarjeta);
            } else {
                System.out.println("El número de tarjeta debe tener 16 dígitos. Intente de nuevo.");
            }
        }
        
        for (String tarjeta : tarjetas) {
            if (esTarjetaValida(tarjeta)) {
                System.out.println(tarjeta + " es válida.");
            } else {
                System.out.println(tarjeta + " no es válida.");
            }
        }

        scanner.close();
    }

    public static boolean esTarjetaValida(String numeroTarjeta) {
        int sumaTotal = 0;

        for (int i = 0; i < numeroTarjeta.length(); i++) {
            int digito = Character.getNumericValue(numeroTarjeta.charAt(i));

            if (i % 2 == 0) {
                digito *= 2;

                if (digito > 9) {
                    digito = digito / 10 + digito % 10;
                }
            }

            sumaTotal += digito;
        }

        return sumaTotal > 70;
    }
}
