# **Seminário CLP - DART**
##### Davi Medeiros, João Victor Ottoni, Rafael Carvalho
---
## **Para compilar:**
```linux
    dart run lib/main.dart
```
---
## **História**
- `Dart`, originalmente chamada de `Dash`, é uma linguagem de script voltada à web desenvolvida pela google;
- Foi lançada em `2011` na GOTO conference;
- Tinha o objetivo de substituir `JavaScript` como linguagem principal embutida nos navegadores;

---
## **Características Gerais**
- Baseada em compilaçoes de códigos de JavaScript
- Baseada em classes;
- Comporta análises estáticas;
- Tem suporte a JS, HTML e CSS
- Suporta Variedade de recursos, como interfaces, classes abstratas e coleções;
- É flexível, podendo ser executada em ambientes nativos e em ambientes web(tanto em aplicações móveis,quanto em aplicações online que utilizam frameworks);
- Programas em Dart podem tanto serem executados em VM`s quanto compilados para JS;
- Otimizada para interface de usuário;


---
## **Funcionalidades**

### **Inferência de Tipo**
- Dart permite que o compilador infira o tipo da variável sem precisar declará-lo explicitamente, enquanto no código em java a tipagem é sempre explícita;

**Java**

```java
private List<E> dados;

public DAO() {
    dados = new ArrayList<>();
}
```

**Dart**
[Dart -> DAO](lib/data/dao.dart)
- Compilador de Dart infere automaticamente que _dados é uma List\<E>;
- Não há necessidade de \<E> após [ ], pois Dart deduz isso com base no tipo da variável;
- O getter dados retorna _dados, e Dart mantém o tipo inferido automaticamente;

---
### **Null Safety (?, ??, ??=)**
- A linguagem possui suporte nativo para null safety, evitando erros de acesso a valores null.
-Java, por outro lado, pode lançar **NullPointerException** se tentarmos acessar um objeto **null**.

**Java**
```java
public Produto buscar(String nome) {
    for (Produto p : dao.getDados()) {
        if (p.getNome().equals(nome)) {
            return p;
        }
    }
    return null;
}
```
**Dart**
[Dart -> DAO_PROTUDO](/lib/data/dao_produto.dart)

---
### **Funções Anônimas (=>)**
- Dart Permite definir **Funções Anônimas** e **Funções de Seta (=>)** , que simplificam expressões de uma única linha. Em Java, lambda são usados para isso.

**Exemplo**
```dart
    _dados.removeWhere((e) {
    return e.id == id;
        //se e.id == id retorna true e o elemento é removido da lista
    });
```

**Dart** [Dart -> DAO](/lib/data/dao.dart)

---
### **Tratamento de Exceções (try-catch)**
- Não é necessário declarar exceções que um método pode lançar `(throws)`, enquanto em Java isso é obrigatório.

**Exemplo Utilizado**
```dart
    try {
            stdout.write("\nDigite o nome do produto: ");
            String nomeProduto = stdin.readLineSync()!;
            Produto? produto = daoProduto.buscarPorNome(nomeProduto);

            //usuario pode digitar valor não numérico, como "abc", gerando erro de conversão com int.parse(), caso aconteça, uma exceção do tipo FormatException será lançada.
            stdout.write("Digite a quantidade: ");
            int qtd = int.parse(stdin.readLineSync()!);

            //verifica se produto == null e quantidade maior que zero
            if (produto == null || qtd <= 0) {
            throw Exception("\nFavor informar os dados corretamente.\n");
            }

            venda.adicionarItem(produto, qtd);

            stdout.write("\nDeseja adicionar outro produto à venda (1-SIM/0-NAO)? ");
            int continuar = int.parse(stdin.readLineSync()!);
            if (continuar != 1) break;
        } catch (e) {
            //se qualquer erro for lançado dentro do try, ele será capturado pro catch(e)
            print(e);
        }
```


**Dart** [Dart -> MENU_VENDA](/lib/ui/menu_venda.dart)

---
### **Iteração sobre Coleções (for-in e forEach)**
- Dart facilita a iteração sobre listas com `for-in` e `forEach`. Java usa forEach, mas não tem forEach nativo em listas antes do Java 8.

### **For-in**
**Formato em Java**
```java
    for (Tipo elemento : exemplo) {
        // Código executado para cada elemento
    }
```

**Formato em Dart**
```dart
    // para cada i presente em
    for (var elemento in exemplo)
        //codigo executado para cada elemento
    }
```

**Dart** [Dart -> VENDA](/lib/entidades/venda.dart)

### **For-each**

**Java**
```java 
    List<String> frutas = ["Maçã", "Banana", "Laranja"];
    for (var fruta in frutas) {
    print("Fruta: $fruta");
    }
```


**Java 8+**
```java 
    frutas.forEach(fruta -> System.out.println("Fruta: " + fruta));
```
**Dart**
```dart
    frutas.forEach((fruta) => print("Fruta: $fruta"));
```

---
### **Parâmetros Nomeados e Opcionais**
- Dart permite definir parâmetros nomeados e opcionais sem precisar de `sobrecarga`, enquanto Java exige múltiplos métodos para suportar diferentes parâmetros.


**Dart**
```java
    void exibirProduto({String nome = "Produto Genérico", double valor = 0.0}) {
    print("Nome: $nome, Valor: R\$ $valor");
    }

    void main() {
    exibirProduto(); // Usa os valores padrão
    exibirProduto(nome: "Coca-Cola"); // Define apenas o nome
    exibirProduto(nome: "Refrigerante", valor: 5.50); // Define nome e valor
    }
```


---
### **Execução Assíncrona (async e await)**
- Dart suporta `async` e `await` para chamadas assíncronas, sem precisar de `Threads` como em Java.

**Java**
```java
    new Thread(() -> {
        try {
            Thread.sleep(2000);
            System.out.println("Dados carregados.");
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }).start();

    System.out.println("Executando outras tarefas...");
```
**Dart**
```dart
    Future<void> carregarDados() async {
    await Future.delayed(Duration(seconds: 2));
    print("Dados carregados.");
    }

    void main() {
    carregarDados();
    print("Executando outras tarefas...");
    }
```

---
## **Características da Linguagem**
---


### **Precedência e Antecedência**
A precedência dos operadores em Dart segue uma hierarquia definida, semelhante a outras linguagens:

- **Maior precedência:** `()` (parênteses), `[]` (acesso a listas e mapas), `.` (acesso a propriedades e métodos)
- **Alta precedência:** `!`, `-` (unário), `++`, `--`
- **Multiplicação e divisão:** `*`, `/`, `~/`, `%`
- **Adição e subtração:** `+`, `-`
- **Operadores relacionais:** `>`, `>=`, `<`, `<=`
- **Igualdade:** `==`, `!=`
- **Operadores lógicos:** `&&`, `||`
- **Atribuição:** `=`, `+=`, `-=`, `*=`, `/=`, `%=`

---
### **Compilador**
Dart pode ser compilado de duas formas:

- **JIT (Just-In-Time):** Usado para desenvolvimento, permitindo execução rápida sem compilação completa.
```linux
    dart run <arquivo>.dart
```
- **AOT (Ahead-Of-Time):** Usado para compilar aplicativos em código nativo, melhorando a performance.
```linux
   dart compile exe <arquivo>.dart
   ./teste.exe
```

---
### **Módulos e Importação de Código**
Dart permite modularização do código através de `import`:
```dart
import 'package:meu_pacote/minha_classe.dart';
```
Também permite importar partes específicas:
```dart
import 'minha_classe.dart' show ClasseA, ClasseB;
```

---

### **Conversão de Variáveis**
Dart permite conversão entre tipos:
```dart
//string para inteiro
int numero = int.parse("42");
//string para decimal
double decimal = double.parse("3.14");
//numero para string
String texto = numero.toString();
```
---
### **Classes, Herança, Polimorfismo e Abstração**
Dart segue o paradigma de orientação a objetos:
```dart
class Animal {
  void fazerSom() {
    print("Som genérico");
  }
}

class Cachorro extends Animal {
  @override
  void fazerSom() {
    print("Latido");
  }
}
```

---
### **Sobrecarga, Sobreposição e Sobrescrita**
- **Sobrecarga:** Dart não suporta diretamente, mas é possível simular com parâmetros opcionais.
- **Sobreposição:** `@override` permite modificar métodos de uma superclasse.
- **Sobrescrita:** Acontece em interfaces e classes abstratas.

---
### **Estruturas de Controle**
Dart possui:

- `if`, `else`, `switch`
- `for`, `for-in`, `for-each` `while`, `do-while`
- Expressões ternárias `condicao ? verdadeiro : falso`

---
### **Curto Circuito**
Dart aplica curto circuito em operadores lógicos:
```dart
bool resultado = false && funcaoPesada(); // funcaoPesada() não será executada
```

---
### **Efeitos Colaterais**
Funções puras evitam efeitos colaterais:
```dart
int soma(int a, int b) => a + b; // Sem alterações externas
```

---

### **Coletor de Lixo**
O Dart utiliza um Coletor de Lixo baseado em rastreamento `(Tracing Garbage Collector - GC)`, especificamente um Garbage Collector incremental e generacional.
#### **Como Funciona**
1- Coletor de Lixo Geracional:

    - Objetos recém-nascidos são alocados na Geração Jovem
    - Objetos que sobrevivem várias coletas são promovidos para a Geração Velha (Old Generation).
    - Objetos na Old Generation são coletados com menos frequência para reduzir impacto na performance.

2- Coletor de lixo incremental:

    - Executa a coleta de forma parcial e distribuída, evitando pausas longas na execução da aplicação.

3- Tracing GC (Técnica de Rastreamento)

    - Baseado no Marcar e Varrer, onde objetos ão marcados e removidos da memória.

4- Coleta Automática:

    - O desenvolvedor não precisa gerenciar manualmente a memória, pois o GC cuida da liberação automática de objetos não referenciados.

---


