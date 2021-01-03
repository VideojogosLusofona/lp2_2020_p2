<!--
Projeto 2 de Linguagens de Programação II 2020/2021 (c) by Nuno Fachada

Projeto 2 de Linguagens de Programação II 2020/2021 is licensed under a
Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License.

You should have received a copy of the license along with this
work. If not, see <http://creativecommons.org/licenses/by-nc-sa/4.0/>.
-->

# Projeto 2 de Linguagens de Programação II 2020/2021

## Descrição do problema

Os grupos devem implementar um jogo em C# usando os principais *design patterns*
para jogos, bem como *design patterns* mais gerais quando apropriado, tendo
sempre em conta os diferentes princípios de design de classes, como por exemplo
os princípios [SOLID].

### O jogo a desenvolver

O jogo deve ser desenvolvido em modo de consola, mais especificamente como uma
aplicação .NET Core 3.1 multi-plataforma, devendo também funcionar e ser testado
em Mac e/ou Linux (devem ser evitadas classes ou métodos específicos para
Windows). Uma das limitações do C# para jogos de consola em tempo real é a
falta de suporte para deteção de teclas continuamente pressionadas. Desta forma,
apenas é possível implementar jogos em que funcionem com um pressionar repetido
das teclas. Aceitam-se propostas de jogos, mas ficam algumas sugestões:

* [Tetris]
* [Snake]
* [Frogger]
* [Moon Buggy]
* [Tron]
* [Pac-Man]
* Qualquer jogo de tabuleiro ou _turn-based_ simples (neste caso é obrigatório
  que o jogo tenha algum tipo de animações a decorrer enquanto os jogadores
  decidem a jogada a efetuar)

Cada grupo deve implementar um jogo diferente, sendo que os primeiros a
indicar a escolha via email ou Moodle terão direito a desenvolver o respetivo
jogo. A lista de jogos atribuídas será colocada e atualizada no Moodle. Alguns
jogos poderão ter dificuldades específicas, pelo que se tiverem dúvidas entrem
em contacto para analisarmos a situação.

Não é necessário (e na maior parte dos casos, nem sequer é possível) que o jogo
seja uma réplica exata do original, bastando implementar as mecânicas básicas,
ser jogável e ter algum tipo de pontuação. É também necessário indicar, antes
do jogo começar, as regras e controlos do mesmo. Naturalmente serão bonificadas
soluções mais completas, com menu, lista de *high scores* persistente entre
jogos, vários níveis, animações dinâmicas, etc. Não é necessário o uso de cores
na consola nem de som.

### Requisitos técnicos mínimos

O jogo deve no mínimo fazer uso das seguintes técnicas:

* Ter como base de implementação o [Game Loop] e o [Update Method]. O
  [Component Pattern] poderá ser essencial para uma boa organização do código.
* Ter (pelo menos) duas *threads*: a *thread* principal do jogo (que executa
  o *game loop*) e uma *thread* para ler *input* do utilizador.

O jogo deve ainda:

* Implementar as mecânicas base do jogo original.
* Ser jogável e ter algum tipo de pontuação.
* Ter algum tipo de ecrã inicial ou opção no menu onde sejam explicadas as
  regras e indicados os controlos do jogo. Atenção que os menus devem ser
  implementados usando o vosso modelo de _game engine_ (ou seja, dentro do
  _game loop_), podendo ser, por exemplo, uma cena (_scene_) específica.

### Organização do projeto e estrutura de classes

O projeto deve estar devidamente organizado, fazendo uso de classes, `struct`s
e/ou enumerações, consoante seja mais apropriado. Cada tipo (i.e., classe,
`struct` ou enumeração) deve ser colocado num ficheiro com o mesmo nome. Por
exemplo, uma classe chamada `Game` deve ser colocada no ficheiro `Game.cs`. Por
sua vez, a escolha da coleções e *design patterns* também deve ser adequada a
cada situação. Serão previligiadas soluções que tenham em consideração bons
princípios de design de classes, como é o caso dos princípios [SOLID]. Estes
*patterns* e princípios devem ser balanceados com o princípio [KISS], crucial
no desenvolvimento de qualquer sistema.

### Verificação automática de erros e _warnings_

Na pasta do vosso projeto (ou seja, na pasta que contém o vosso ficheiro
`.csproj`), devem colocar o ficheiro [`StyleCop.ruleset`](StyleCop.ruleset),
sendo que o ficheiro `.csproj` do vosso projeto deve ter o seguinte formato:

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>netcoreapp3.1</TargetFramework>
    <AnalysisMode>AllEnabledByDefault</AnalysisMode>
    <EnforceCodeStyleInBuild>true</EnforceCodeStyleInBuild>
    <DocumentationFile>$(OutputPath)$(AssemblyName).xml</DocumentationFile>
    <CodeAnalysisRuleSet>StyleCop.ruleset</CodeAnalysisRuleSet>
    <EnableNETAnalyzers>true</EnableNETAnalyzers>
  </PropertyGroup>

  <ItemGroup>
    <PackageReference Include="SonarAnalyzer.CSharp" Version="8.16.0.25740">
      <IncludeAssets>runtime; build; native; contentfiles; analyzers; buildtransitive</IncludeAssets>
      <PrivateAssets>all</PrivateAssets>
    </PackageReference>
    <PackageReference Include="Roslynator.Analyzers" Version="3.0.0">
      <IncludeAssets>runtime; build; native; contentfiles; analyzers; buildtransitive</IncludeAssets>
      <PrivateAssets>all</PrivateAssets>
    </PackageReference>
    <PackageReference Include="Roslynator.Formatting.Analyzers" Version="1.0.0">
      <IncludeAssets>runtime; build; native; contentfiles; analyzers; buildtransitive</IncludeAssets>
      <PrivateAssets>all</PrivateAssets>
    </PackageReference>
    <PackageReference Include="StyleCop.Analyzers" Version="1.1.118">
      <IncludeAssets>runtime; build; native; contentfiles; analyzers; buildtransitive</IncludeAssets>
      <PrivateAssets>all</PrivateAssets>
    </PackageReference>
  </ItemGroup>

</Project>
```

Em vez de executarem o vosso projeto com o comando `dotnet run`, compilem-no
primeiro com a seguinte sequência de comandos na pasta do vosso projeto (ou
seja, na pasta que contém o vosso ficheiro `.csproj`):

```
$ dotnet clean
$ dotnet build
```

Vão ter agora vários _warnings_ que anteriormente não tinham. Este _warnings_
são relativos a tudo, desde o uso de más práticas (e.g. variáveis de instância
públicas) até esquecimentos e erros de documentação e indentação mal feita.

Estes erros e _warning_ vão aparecer automaticamente no Visual Studio 2019. No
Visual Studio Code devem instalar a extensão [Roslynator] para visualizarem
estes erros no editor. Em qualquer dos casos, pode ser necessário reiniciar o
Visual Studio para que os erros apareçam após alterarem o ficheiro `.csproj`.

Atenção que os projetos entregues **não devem conter qualquer _warning_**, caso
contrário **não serão avaliados**.

Esta abordagem vai criar um novo ficheiro `NomeDoProjeto.xml`, que deve ser
ignorado através do `.gitignore`.

## Objetivos e critério de avaliação

Este projeto tem os seguintes objetivos:

* **O1** - Projeto deve cumprir os [requisitos
  mínimos](#requisitos-técnicos-mínimos).
* **O2** - Projeto e código bem organizados, nomeadamente:
  * Estrutura de classes bem pensada (ver secção
  [Organização do projeto e estrutura de
  classes](#organização-do-projeto-e-estrutura-de-classes)).
  * Código devidamente comentado e indentado.
  * Inexistência de código "morto", que não faz nada, como por exemplo
    variáveis, propriedades ou métodos nunca usados.
  * Projeto compila e executa sem erros e/ou *warnings*, tal como referido na
    secção [Verificação automática de erros e
    _warnings_](#verificação-automática-de-erros-e-warnings).
* **O3** - Projeto adequadamente documentado. Documentação deve ser feita com
  [comentários de documentação XML][XML], e a documentação (gerada em formato
  HTML ou CHM com [Doxygen], [DocFX] ou ferramenta similar) deve estar incluída
  no ZIP do projeto, mas **não** integrada no repositório Git.
* **O4** - Repositório Git deve refletir boa utilização do mesmo, com
  *commits* de todos os elementos do grupo e mensagens de *commit* que sigam
  as melhores práticas para o efeito (como indicado
  [aqui](https://chris.beams.io/posts/git-commit/),
  [aqui](https://gist.github.com/robertpainsi/b632364184e70900af4ab688decf6f53),
  [aqui](https://github.com/erlang/otp/wiki/writing-good-commit-messages) e
  [aqui](https://stackoverflow.com/questions/2290016/git-commit-messages-50-72-formatting)).
  Quaisquer *assets* binários, tais como imagens, devem ser integrados
  no repositório em modo Git LFS.
* **O5** - Relatório em formato [Markdown] (ficheiro `README.md`),
  organizado da seguinte forma:
  * Título do projeto.
  * Autoria:
    * Nome dos autores (primeiro e último) e respetivos números de aluno.
    * Informação de quem fez o quê no projeto. Esta informação é
      **obrigatória** e deve refletir os *commits* feitos no Git.
    * Indicação do repositório público Git utilizado. Esta indicação é
      opcional, pois podem preferir desenvolver o projeto num repositório
      privado.
  * Arquitetura da solução:
    * Descrição da solução, com breve explicação de como o programa foi
      organizado, indicação dos *design patterns* utilizados e a razão do
      seu uso, bem como dos algoritmos implementados (e.g., para deteção
      de colisões, cálculo de ângulos e trajetórias, etc).
    * Um diagrama UML de classes simples (i.e., sem indicação dos
      membros da classe) descrevendo a estrutura de classes.
    * Um fluxograma mostrando o funcionamento do programa.
  * Referências, incluindo trocas de ideias com colegas, código aberto
    reutilizado (e.g., do StackOverflow) e bibliotecas de terceiros
    utilizadas. Devem ser o mais detalhados possível.
  * **Nota:** o relatório deve ser simples e breve, com informação mínima e
    suficiente para que seja possível ter uma boa ideia do que foi feito.
    Atenção aos erros ortográficos e à correta formatação [Markdown], pois
    ambos serão tidos em conta na nota final.

O projeto tem um peso de 3 valores na nota final da disciplina e será avaliado
de forma qualitativa. Isto significa que todos os objetivos têm de ser
parcialmente ou totalmente cumpridos. A cada objetivo, O1 a O5, será atribuída
uma nota entre 0 e 1. A nota do projeto será dada pela seguinte fórmula:

*N = 3 x O1 x O2 x O3 x O4 x O5 x D*

Em que *D* corresponde à nota da discussão e percentagem equitativa de
realização do projeto, também entre 0 e 1. Isto significa que se os alunos
ignorarem completamente um dos objetivos, não tenham feito nada no projeto ou
não comparecerem na discussão, a nota final será zero.

## Entrega

O projeto deve ser entregue por **grupos de 2 a 3 alunos** via Moodle até às
23h de 4 de janeiro de 2021. Deve ser submetido um ficheiro `zip` com a
solução completa do projeto, nomeadamente:

* Pasta escondida `.git` com o repositório Git local do projeto.
* Documentação HTML ou CHM gerada com [Doxygen], [DocFX] ou ferramenta
  similar.
* Ficheiro `README.md` contendo o relatório do projeto em formato [Markdown].
* Ficheiros de imagens, contendo o diagrama UML de classes, o fluxograma, e
  outras figuras que considerem úteis. Estes ficheiros devem ser incluídos no
  repositório em modo Git LFS.

## Honestidade académica

Nesta disciplina, espera-se que cada aluno siga os mais altos padrões de
honestidade académica. Isto significa que cada ideia que não seja do
aluno deve ser claramente indicada, com devida referência ao respetivo
autor. O não cumprimento desta regra constitui plágio.

O plágio inclui a utilização de ideias, código ou conjuntos de soluções
de outros alunos ou indivíduos, ou quaisquer outras fontes para além
dos textos de apoio à disciplina, sem dar o respetivo crédito a essas
fontes. Os alunos são encorajados a discutir os problemas com outros
alunos e devem mencionar essa discussão quando submetem os projetos.
Essa menção **não** influenciará a nota. Os alunos não deverão, no
entanto, copiar códigos, documentação e relatórios de outros alunos, ou dar os
seus próprios códigos, documentação e relatórios a outros em qualquer
circunstância. De facto, não devem sequer deixar códigos, documentação e
relatórios em computadores de uso partilhado.

Nesta disciplina, a desonestidade académica é considerada fraude, com
todas as consequências legais que daí advêm. Qualquer fraude terá como
consequência imediata a anulação dos projetos de todos os alunos envolvidos
(incluindo os que possibilitaram a ocorrência). Qualquer suspeita de
desonestidade académica será relatada aos órgãos superiores da escola
para possível instauração de um processo disciplinar. Este poderá
resultar em reprovação à disciplina, reprovação de ano ou mesmo suspensão
temporária ou definitiva da ULHT.

*Texto adaptado da disciplina de [Algoritmos e
Estruturas de Dados][aed] do [Instituto Superior Técnico][ist]*

## Referências

* \[1\] Whitaker, R. B. (2016). **The C# Player's Guide** (3rd Edition).
  Starbound Software.
* \[2\] Albahari, J. (2017). **C# 7.0 in a Nutshell**. O’Reilly Media.
* \[3\] Nystrom, R. (2014). **Game Programming Patterns**. Genever Benning.
  Retrieved from <http://gameprogrammingpatterns.com/>.
* \[4\] Freeman, E., Robson, E., Bates, B., & Sierra, K. (2004). **Head First
  Design Patterns**. O'Reilly Media.
* \[5\] Dorsey, T. (2017). **Doing Visual Studio and .NET Code Documentation
  Right**. Visual Studio Magazine. Retrieved from
  <https://visualstudiomagazine.com/articles/2017/02/21/vs-dotnet-code-documentation-tools-roundup.aspx>.

## Licenças

Este enunciado é disponibilizado através da licença [CC BY-NC-SA 4.0].

## Metadados

* Autor: [Nuno Fachada]
* Curso:  [Licenciatura em Videojogos][lamv]
* Instituição: [Universidade Lusófona de Humanidades e Tecnologias][ULHT]

[CC BY-NC-SA 4.0]:https://creativecommons.org/licenses/by-nc-sa/4.0/
[lamv]:https://www.ulusofona.pt/licenciatura/videojogos
[Nuno Fachada]:https://github.com/fakenmc
[ULHT]:https://www.ulusofona.pt/
[aed]:https://fenix.tecnico.ulisboa.pt/disciplinas/AED-2/2009-2010/2-semestre/honestidade-academica
[ist]:https://tecnico.ulisboa.pt/pt/
[Markdown]:https://guides.github.com/features/mastering-markdown/
[Doxygen]:https://www.stack.nl/~dimitri/doxygen/
[DocFX]:https://dotnet.github.io/docfx/
[KISS]:https://en.wikipedia.org/wiki/KISS_principle
[XML]:https://docs.microsoft.com/dotnet/csharp/codedoc
[SOLID]:https://en.wikipedia.org/wiki/SOLID
[Snake]:https://en.wikipedia.org/wiki/Snake_(video_game_genre)
[Frogger]:https://en.wikipedia.org/wiki/Frogger
[Moon buggy]:https://www.seehuhn.de/pages/moon-buggy
[Tron]:https://en.wikipedia.org/wiki/Tron_(video_game)
[Pac-Man]:https://en.wikipedia.org/wiki/Pac-Man
[Tetris]:https://en.wikipedia.org/wiki/Tetris
[Game Loop]:http://gameprogrammingpatterns.com/game-loop.html
[Update Method]:http://gameprogrammingpatterns.com/update-method.html
[Component Pattern]:https://gameprogrammingpatterns.com/component.html
[Roslynator]:https://marketplace.visualstudio.com/items?itemName=josefpihrt-vscode.roslynator