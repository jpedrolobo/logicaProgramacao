# ☕ Java Backend

Java no Backend é responsável por toda a lógica do servidor: processar requisições, acessar banco de dados e retornar respostas ao usuário.

---

## 🧠 O que ele faz

* Processa requisições HTTP
* Aplica regras de negócio
* Conecta com banco de dados
* Retorna dados (JSON/XML)

---

## 🔧 Tecnologias comuns

* Spring Boot
* Hibernate / JPA
* APIs REST

---

## 🖼️ Arquitetura básica

![Arquitetura Backend](https://raw.githubusercontent.com/mermaid-js/mermaid/main/docs/public/syntax/flowchart.svg)

---

## 🖼️ Fluxo de requisição

![Fluxo Backend](https://raw.githubusercontent.com/mermaid-js/mermaid/main/docs/public/syntax/sequenceDiagram.svg)

---

## ⚙️ Exemplo simples (Spring Boot)

```java
@RestController
public class HelloController {

    @GetMapping("/hello")
    public String hello() {
        return "Olá, mundo!";
    }
}
```

---

## 💡 Resumo

Java Backend = **Servidor + Lógica + Banco de Dados**

---
