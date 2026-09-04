
POO "Programação orientada a objetos" é um paradigma baseado na modelagem do mundo real através de Classes (os moldes/projetos) e Objetos (as instâncias desses moldes na memória).

## 1. **Classes, Atributos, Métodos e Construtores**
- **Classe:** Define as caracteristicas (atributos) e comportamentos (métodos).
- **Construtor:** Método especial chamado na criação do objeto com *"new"*.

```
public class ContaBancaria {
	// Atributos
	String titular;
	double saldo;
	
	// Construtor
	public ContaBancaria(String titular, double saldoInicial) {
		this.titular = titular;
		this.saldo = saldoInicial
	}
	
	// Método
	public void depositar(double valor) {
		if (valor > 0){
			this.saldo += valor;
		}
	}
}
```


## 2. **Os 4 pilares da POO**
- **Encapsulamento:** Esconde os detalhes internos da classe e protege os dados contra acesso desordenado usando modificadores de acesso (private, public, protected).

- **Herança (extends):** Permite que uma classe filha herde atributos e métodos de uma classe pai, promovendo o reuso de código.


```
// Classe Pai
public class Funcionario {
	protected String nome;
	protected double salario;
	
	public Funcionario(String nome, double salario) {
		this.nome = nome;
		this.salario = salario;
	}
	
	public double getBonificacao() {
		return this.salario * 0.10;
	}
}

// Classe filha
public class Gerente extends Funcionario {
	public Gerente(String nome, double salario) {
		super(nome, salario); // Chama o construtor da classe pai
	}
}
```


- **Polimorfismo:** Permite tratar objetos de classes filhas como se fosem da classe pai,
- mudando o comportamento através da sobrescrita (*@Override*).


```
public class Gerente extends Funcionario {
	public Gerente(String nome, double salario) {
		super(nome, salario);
	}
	
	@Override
	public double getBonificacao() {
		// Gerente recebe uma bonificação maior
		return this.salario * 0.20; 
	}
}
```

- **Abstração (abstract e interface):** Define o que deve ser feito, deixando para as classes filhas decidirem como fazer.

```
// Interface: contrato de métodos sem implementação
public interface Autenticavel {
	boolen autenticar(String senha);
}

// Classe Abstrata: não pode ser instanciada diretamente
public abstract class Notificacao {
	public abstract void enviar(String menssagem);
}
```

## 3. Recursos Modernos: Records e Sealed Classes

- **Records:** Trazidos no Java 14+ , são classes imutáveis prontas para transporte de dados (DTOs) com construtor, getters, equals, hashCode e toString gerados automaticamente.

```
public record UsuarioDTO(String nome, String email) {}
```

- **Sealed Classes:** Permitem restringir quais classes podem herdar de uma classe pai.

```
public sealed class Forma permits Circulo, Quadrado {}

public final class Circulo extends Forma {}
public final class Quadrado extends Forma {}
```

**Exercicio :** 


#### Interface `MeioDePagamento`

Define o contrato obrigatório.

```
public interface MeioDePagamento {
    void processarPagamento(double valor); // Métodos em interface são public por padrão
}
```

#### Classe `CartaoCredito`

Implementa a interface e valida o limite antes de aprovar.

```
public class CartaoCredito implements MeioDePagamento {
    private double limite;

    public CartaoCredito(double limite) {
        this.limite = limite;
    }

    @Override
    public void processarPagamento(double valor) {
        if (valor <= this.limite) {
            this.limite -= valor; // Deduz do limite disponível
            System.out.println("Pagamento de R$ " + valor + " aprovado no Cartão de Crédito. Limite restante: R$ " + this.limite);
        } else {
            System.out.println("Pagamento recusado! Valor R$ " + valor + " excede o limite disponível de R$ " + this.limite);
        }
    }

    public double getLimite() {
        return limite;
    }
}
```

#### Classe `Pix`

Implementa a mesma interface com regras próprias.

```
public class Pix implements MeioDePagamento {
    private String chavePix;

    public Pix(String chavePix) {
        this.chavePix = chavePix;
    }

    @Override
    public void processarPagamento(double valor) {
        System.out.println("Pagamento de R$ " + valor + " realizado instantaneamente via Pix para a chave: " + this.chavePix);
    }
}
```

#### Execução (Polimorfismo em Ação)

Como ambas as classes implementam `MeioDePagamento`, você pode tratá-las de forma genérica:

```
public class Main {
    public static void main(String[] args) {
        MeioDePagamento pagamento1 = new CartaoCredito(500.0);
        MeioDePagamento pagamento2 = new Pix("usuario@email.com");

        pagamento1.processarPagamento(200.0); // Aprovado
        pagamento1.processarPagamento(400.0); // Recusado (limite sobrou 300)
        
        pagamento2.processarPagamento(150.0); // Pix realizado
    }
}
```