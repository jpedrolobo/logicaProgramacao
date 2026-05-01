-----Calendario----


static void main(String[] args) {
    Scanner leitor = new Scanner(System.in);
    int dia;

    System.out.println("qual dia da semana voce deseja descobrir?");
    dia = leitor.nextInt();

    switch (dia)  {
        case 1:
            System.out.println("segunda-feira");
            break;
        case 2:
            System.out.println("Terça-feira");
            break;
        case 3:
            System.out.println("Quarta-feira");
            break;
        case 4:
            System.out.println("Quinta-feira");
            break;
        case 5:
            System.out.println("Sexta-feira");
            break;
        case 6:
            System.out.println("Sabado");
        case 7:
            System.out.println("Domingo");
            break;
    }
    }
}
