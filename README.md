# PAP (Padrões de Projeto)

## Resume
**Padrões de projeto** são soluções típicas para problemas comuns em projeto de software.

### Categoria
- **Padrões de Criação**: fornecem mecanismos de criação de objetos que aumentam a flexibilidade e a reutilização de código.
  
- **Padrões Estruturais:** explicam como montar objetos e classes em estruturas maiores, enquanto ainda mantém as estruturas flexíveis e eficientes.
  
- **Padrões Comportamentais:**  cuidam da comunicação eficiente e da assinalação de responsabilidades entre objetos.
  
<p align="center">
  <img width="550" height="500" src="padroesdeprojeto.png">
</p>

### Do que consiste um padrão?
A maioria dos padrões são descritos formalmente para que as pessoas possam reproduzi-los em diferentes contextos. Aqui estão algumas seções que são geralmente presentes em uma descrição de um padrão:
 - O **Propósito** do padrão descreve brevemente o problema e a solução.
 - A **Motivação** explica a fundo o problema e a solução que o padrão torna possível.
 - As **Estruturas** de classes mostram cada parte do padrão e como se relacionam.
 - **Exemplos de código** em uma das linguagens de programação populares tornam mais fácil compreender a ideia por trás do padrão.

## Strategy
O **Strategy** é um padrão de projeto comportamental que permite que você defina uma família de algoritmos, coloque-os em classes separadas, e faça os objetos deles intercambiáveis.

- Como implementar

    1.Na classe contexto, identifique um algoritmo que é sujeito a frequentes mudanças. Pode ser também uma condicional enorme que seleciona e executa uma variante do mesmo algoritmo durante a execução do programa.

    2.Declare a interface da estratégia comum para todas as variantes do algoritmo.

    3.Um por um, extraia todos os algoritmos para suas próprias classes. Elas devem todas implementar a interface estratégia.

    4.Na classe contexto, adicione um campo para armazenar uma referência a um objeto estratégia. Forneça um setter para substituir valores daquele campo. O contexto deve trabalhar com o objeto estratégia somente através da interface estratégia. O contexto pode definir uma interface que deixa a estratégia acessar seus dados.

    5.Os Clientes do contexto devem associá-lo com uma estratégia apropriada que coincide com a maneira que esperam que o contexto atue em seu trabalho primário.

### Prós
  - Você pode trocar algoritmos usados dentro de um objeto durante a execução.
  - Você pode isolar os detalhes de implementação de um algoritmo do código que usa ele.
  - Você pode substituir a herança por composição.
  - Princípio aberto/fechado. Você pode introduzir novas estratégias sem mudar o contexto.

### Contras
  - Se você só tem um par de algoritmos e eles raramente mudam, não há motivo real para deixar o programa mais complicado com novas classes e interfaces que vêm junto com o padrão.
  - Os Clientes devem estar cientes das diferenças entre as estratégias para serem capazes de selecionar a adequada.
  - Muitas linguagens de programação modernas tem suporte do tipo funcional que permite que você implemente diferentes versões de um algoritmo dentro de um conjunto de funções anônimas. Então você poderia usar essas funções exatamente como se estivesse usando objetos estratégia, mas sem inchar seu código com classes e interfaces adicionais.

## Observer
O **Observer** é um padrão de projeto comportamental que permite que você defina um mecanismo de assinatura para notificar múltiplos objetos sobre quaisquer eventos que aconteçam com o objeto que eles estão observando.

- Como implementar

    1.Olhe para sua lógica do negócio e tente quebrá-la em duas partes: a funcionalidade principal, independente de outros códigos, irá agir como publicadora; o resto será transformado em um conjunto de classes assinantes.

    2.Declare a interface do assinante. No mínimo, ela deve declarar um único método atualizar.

    3.Declare a interface da publicadora e descreva um par de métodos para adicionar um objeto assinante e removê-lo da lista. Lembre-se que publicadoras somente devem trabalhar com assinantes através da interface do assinante.

    4.Decida onde colocar a lista atual de assinantes e a implementação dos métodos de inscrição. Geralmente este código se parece o mesmo para todos os tipos de publicadoras, então o lugar óbvio para colocá-lo é dentro de uma classe abstrata derivada diretamente da interface da publicadora. Publicadoras concretas estendem aquela classe, herdando o comportamento de inscrição.

    Contudo, se você está aplicando o padrão para uma hierarquia de classe já existente, considere uma abordagem baseada na composição: coloque a lógica da inscrição dentro de um objeto separado, e faça todos as publicadoras reais usá-la.

    5.Crie as classes publicadoras concretas. A cada vez que algo importante acontece dentro de uma publicadora, ela deve notificar seus assinantes.

    6.Implemente os métodos de notificação de atualização nas classes assinantes concretas. A maioria dos assinantes precisarão de dados contextuais sobre o evento. Eles podem ser passados como argumentos do método de notificação.

   Mas há outra opção. Ao receber uma notificação, o assinante pode recuperar os dados diretamente da notificação. Neste caso, a publicadora deve passar a si mesma através do método de atualização. A opção menos flexível é ligar uma publicadora ao assinante permanentemente através do construtor.

    7.O cliente deve criar todas os assinantes necessários e registrá-los com suas publicadoras apropriadas.

### Prós
  - Princípio aberto/fechado. Você pode introduzir novas classes assinantes sem ter que mudar o código da publicadora (e vice versa se existe uma interface publicadora).
  - Você pode estabelecer relações entre objetos durante a execução.

### Contras
  - Assinantes são notificados em ordem aleatória

