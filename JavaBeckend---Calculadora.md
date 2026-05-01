--CALCULADORA--


    int opcao = 1;
    double num1 = 0;
    double num2 = 0;
    double resultado = 0;

    while (opcao != 0) {

        System.out.println("=== CALCULADORA ===");
        System.out.println("1 - Soma");
        System.out.println("2 - Subtração");
        System.out.println("3 - Multiplicação");
        System.out.println("4 - Divisão");
        System.out.println("0 - Sair");

        opcao = leitor.nextInt();

        if (opcao != 0) {

            System.out.println("Digite o primeiro número:");
            num1 = leitor.nextDouble();

            System.out.println("Digite o segundo número:");
            num2 = leitor.nextDouble();

            if (opcao == 1) {
                resultado = num1 + num2;
                System.out.println("Resultado da soma: " + resultado);

            } else if (opcao == 2) {
                resultado = num1 - num2;
                System.out.println("Resultado da subtração: " + resultado);

            } else if (opcao == 3) {
                resultado = num1 * num2;
                System.out.println("Resultado da multiplicação: " + resultado);

            } else if (opcao == 4) {
                if (num2 != 0) {
                    resultado = num1 / num2;
                    System.out.println("Resultado da divisão: " + resultado);
                } else {
                    System.out.println("Não é possível dividir por zero!");
                }
            } else {
                System.out.println("Opção inválida!");
            }
        }
    }

    System.out.println("Programa encerrado.");
}
}
