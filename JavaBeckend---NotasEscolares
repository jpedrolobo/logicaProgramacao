----Notas Escolares---

static void main(String[] args) {
    Scanner leitor = new Scanner(System.in);

    int quantidadeAlunos = 1;
    int Aprovados = 0;
    int Reprovados = 0;
    double nota = 0;
    double soma = 0;

    while (quantidadeAlunos != 0) {


    System.out.println("quantos alunos tem na turma?");
        System.out.println("Digite 0 para sair do programa");
    quantidadeAlunos = leitor.nextInt();

    for (int i = 1; i <= quantidadeAlunos; i++){
        System.out.println("qual a nota do Aluno?" +i);
        nota = leitor.nextDouble();

        soma = soma + nota;
        if (nota >= 6){
            Aprovados++;
        } else {
            Reprovados++;
        }
    }
    if(quantidadeAlunos != 0){

    System.out.println("Media da turma:" +soma/quantidadeAlunos);
    System.out.println("Alunos aprovados: "+Aprovados);
    System.out.println("Alunos reprovados: "+Reprovados);

    soma = 0;
    Reprovados = 0;
    Aprovados = 0;


    }
    }

    }
    }
